### Nome: Vinícius Pires de Souza  Data: 01/08/2024 
 # Tópicos Estudados:
 ### Principais comandos do Git, Componentes principais do GitFlow, Branches de suporte e o que é Git, GitHub e GitFlow

# O que é GitHub: 
### O GitHub é um lugar para você guardar seus projetos . Além de você guardar seu códigos ele serve para você conhecer outros programadores e outros projetos. O GitHub serve também para você trabalhar em equipe com os seus amigos, pois eles conseguem mexer no seu código e atualizar a versão dele. Eles instalam o seu projeto no computador deles e mexem localmente e depois mandam para o GitHub uma versão nova. 
 
# O que é Git: 
### O Git é um Software que vai manter versões do seu código dentro do seu computador localmente, ele rastreia qualquer alteração que você fizer em seus arquivos ao longo do tempo e se o seu computador acabar estragando você vai perder tudo que está salvo nele. 
 
## Principais comandos do Git: 
 
### 1. Repositório: É onde o Git mantém todo o histórico de alterações de um projeto, incluindo todos os arquivos e diretórios. 
 
### 2. Commit: É um instantâneo do projeto em um determinado momento. Cada commit possui um código identificador exclusivo (hash). 
 
### 3. Branch: É uma linha de desenvolvimento independente que permite trabalhar em diferentes versões do mesmo projeto simultaneamente. A ramificação primária também pode ser chamada de “main” ou “master”. 
 
### 4. Merge: O processo de combinar alterações de diferentes ramos em um único ramo. 
  
### 5. Pull: A operação de buscar as alterações mais recentes de um repositório remoto para um repositório local. 
  
### 6. Push: O ato de propagar commits locais para um repositório remoto. 
 
### 7. Add: adiciona arquivos ao índice para serem confirmados. 
 
### 8. status: mostra o estado dos arquivos no índice e no diretório de trabalho. 
 
### 9. Clone: Você consegue clonar o repositório de outra pessoa  
 

# O que é GitFlow: 
### É um modelo de utilização de versionamento você usa o GitFlow para ter uma ideia de como você pode utilizar as branches para ajudar no desenvolvimento.  
 
 
## Componentes principais do GitFlow: 
### main: Este branch armazena código que já está em produção e estável. Cada commit feito aqui representa uma nova versão publicada. 
### Develop: Este branch contém código em desenvolvimento, incluindo as últimas alterações aprovadas. É a base para o desenvolvimento de novos recursos e integrações. 

## Branches de suporte: 
 
### Feature: usado para desenvolver novos recursos. Ele é criado a partir da branch Develop e, quando o recurso é concluído, ele é mesclado novamente para a Develop. 
### RELEASE: Criado quando uma nova versão está pronta para ser lançada. Ele se origina na Develop e, após ajustes e testes finais, é mesclado na Main e na Develop. 
### hotfix: usado para corrigir problemas críticos na produção. Este branch é criado a partir da Main e, após corrigi-lo, é mesclado de volta a Main e a Develop. 




# Desafios Encontrados:
### Tive dificuldade em aprender os comandos, criar branches e subir para main sem querer.
# Próximos Passos:
### Pretendo me aprofundar mais no Git, GitHub e GitFlow. O meu próximo estudo é Linux/Shell.
