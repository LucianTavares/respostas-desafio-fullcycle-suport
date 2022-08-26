<h1 align="center"> Desafio Full Cycle - Respostas Suporte </h1>

## Questão 1 - 

Olá Gabriel,

Tudo bem com você?

Acontece que dentro do seu arquivo docker-compose.yaml você estava expondo a porta 8080 pelo nginx que é o correto e recebendo do graphql na porta 80, e se entrarmos em seu arquivo server.go a porta que está servindo o playground do graphql está a porta 8080 por padrão também.

```
version: "3"

services:
  app:
    build: .
    container_name: go_graphql
    ports:
      - "8080:80" <--------- Aqui está
    volumes:
      - .:/go/src/
      
 O correto seria:
 
 
version: "3"

services:
  app:
    build: .
    container_name: go_graphql
    ports:
      - "8080:8080"
    volumes:
      - .:/go/src/
```

Qualquer dúvida estou a disposição.


***

## Questão 2 -

Olá Gabriel,

Tudo bem?

Você recebia o erro 502 da aplicação, pois o app não havia sido iniciado com o comando node index.js, você até insere o comando pelo Dockerfile do app mas este comando dentro do Dockerfile só é executado quando o Dockerfile é montado pelo docker-compose, e temos que esperar o database iniciar para depois iniciarmos o app.
Com isso o correto seria iniciar dentro do docker-compose um exemplo seria dentro do entrypoint como abaixo:
 
 ```
 - entrypoint: dockerize -wait tcp://database:3306 node index.js
``` 
Quando o database já estiver rodando na porta 3306 como o exemplo acima, então o node index.js é executado e como o nginx depende do app a ordem de execução ficaria correta.

Qualquer dúvida estamos à disposição.


***

## Questão 3 - 

Olá Renata,

Tudo bem com você?

Para podermos avaliar melhor o que está acontecendo por favor nos envie o repositório, assim conseguimos analisar o ocorrido.

Obrigado.

***

## Questão 4 -

Olá João,

Tudo bem?

Na verdade, o uso de volumes é recomendado tanto para desenvolvimento quanto para o de produção.
É uma boa prática usar volume em produção, na própria documentação (dica de pesquisa) do Docker temos uma área completa falando sobre isso.
Vou citar alguns pontos que são importantes para esclarecer sua dúvida:

- Os volumes podem ser executados em contêineres Linux e Windows.
- Podemos compartilhar os volumes com mais segurança entre diversos 	 containers.
- Drivers de volumes nos permitem armazenar volumes em hosts remotos ou provedores de nuvem, podendo assim criptografar o conteúdo de volumes ou até mesmo adicionar outras funcionalidades.
- Devemos remover qualquer ligação de volume com o código do aplicativo, com isso o código deve permanecer apenas dentro do contêiner e não havendo possibilidade de alterações externas.

Qualquer dúvida estou à disposição.

***

## Questão 5 - 

Olá José,

Tudo bem com você?

Provavelmente pode ser erro de permissão dentro do diretório em que está tentando montar, tente a opção de mudar de diretório e se possível nos envie o repositório do Github, assim podemos avaliar melhor o código.

Estamos sempre a disposição.

Obrigado.