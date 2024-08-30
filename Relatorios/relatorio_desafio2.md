## Relatório - Script SQL 

**Nome: Vinícius Pires de Souza**

**Data:30/08/2024**

***

<br>

 **1. Criando as tabelas** 

~~~
%hive

CREATE TABLE campaigns (
    lines BIGINT,
    id_campaign STRING,
    type_campaign STRING,
    days_valid STRING,
    data_campaign STRING,
    channel STRING,
    return_status STRING,
    return_date STRING,
    client_id STRING
) ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION 's3a://desafio2/campaign_data/'
TBLPROPERTIES ("skip.header.line.count"="1")
~~~

~~~
%hive

CREATE TABLE purchases (
    purchase_id STRING,
    product_name STRING,
    product_id STRING,
    amount INT,
    price DECIMAL(10, 2),
    discount_applied DOUBLE,
    payment_method STRING,
    purchase_datetime TIMESTAMP,
    purchase_location STRING,
    client_id STRING
) ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION 's3a://desafio2/purcashe_data/'
TBLPROPERTIES ("skip.header.line.count"="1")
~~~

<br>

**Carregando os arquivos**
~~~
%hive

LOAD DATA INPATH 's3a://desafio2/campaigns_2023_hist.csv' INTO TABLE campaigns
~~~

~~~
%hive

LOAD DATA INPATH 's3a://desafio2/purchases_2023.csv' INTO TABLE purchases
~~~

**Escolher tabelas para análise**

~~~
%hive
SELECT * FROM campaigns
~~~

~~~
%hive
SELECT * FROM purchases
~~~

**Normalização dos dados conforme as especificações fornecidas**

~~~
%hive

SELECT
    client_id,
    ROUND(SUM(price * amount * discount_applied), 2) AS total_price,
    MAX(purchase_location) AS most_purchase_location,
    DATE_FORMAT(MIN(purchase_datetime), 'yyyy-MM-dd HH:mm') AS first_purchase,
    DATE_FORMAT(MAX(purchase_datetime), 'yyyy-MM-dd HH:mm') AS last_purchase
FROM purchases
GROUP BY client_id
~~~

**Query para most campaign**
~~~
%hive

SELECT 
    client_id, 
    SUM(CASE WHEN return_status != 'error' THEN 1 ELSE 0 END) AS most_campaign,
        SUM(CASE WHEN return_status = 'error' THEN 1 ELSE 0 END) AS quantity_error
FROM 
    campaigns
GROUP BY 
    client_id
~~~

**Query para quantity error**

~~~
%hive

SELECT
    id_campaign,
    COUNT(*) AS quantity_error
FROM
    campaigns
WHERE
    return_status = 'sms'
GROUP BY
    id_campaign
~~~

**Código**

~~~
%hive

SELECT
    p.client_id,
    ROUND(SUM(p.price * p.amount * p.discount_applied), 2) AS total_price,
    MAX(p.purchase_location) AS most_purchase_location,
    DATE_FORMAT(MIN(p.purchase_datetime), 'yyyy-MM-dd HH:mm') AS first_purchase,
    DATE_FORMAT(MAX(p.purchase_datetime), 'yyyy-MM-dd HH:mm') AS last_purchase,
    COALESCE(MAX(c.most_campaign), 0) AS most_campaign,
    COALESCE(MAX(c.quantity_error), 0) AS quantity_error
FROM 
    purchases p
LEFT JOIN (
    SELECT 
        client_id, 
        SUM(CASE WHEN return_status != 'error' THEN 1 ELSE 0 END) AS most_campaign,
        SUM(CASE WHEN return_status = 'error' THEN 1 ELSE 0 END) AS quantity_error
    FROM 
        campaigns
    GROUP BY 
        client_id
) c
ON p.client_id = c.client_id
GROUP BY 
    p.client_id
~~~