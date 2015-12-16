# MongoDb - Projeto Final
**Autor:** Franklin Dias
**Data** Date.now()

## Para qual sistema você usaria o MogoDB (diferente desse)?
Bancos de dados não relacionais em geral podem ser utilizados pra qualquer tipo de sistema, entretato é indicado àqueles que necessitam de uma interação mais rápida entre os dados e a aplicação não importante a replicação de dado, o que acontece normalmente em aplicações 'real time' e nas aplicações que demadam muita quantidade de dado. Sendo assim, além de várias outras aplicações, eu poderia usar o MongoDB tranquilamente em um sistema de E-commerce, por exemplo. Um outro exemplo que poderíamos utilizar banco de dados NoSql são as redes socias, porém para estes é indicado utilizar um banco baseado em Grafos, como o Neo4j.


## Qual a modelagem da sua coleção de 'users'?

## Qual a modelagem da sua coleção de 'projects'?


## Create - cadastro

1. Cadastre 10 usuários diferentes.
2. Cadastre 5 projetos diferentes.
    - cada um com 5 membros, sempre diferentes dentro dos projetos;
    - cada um com pelo menos 3 tags diferentes;
        - escolha 1 *tag* onde deva ficar em 2 projetos;
        - escolha 1 *tag* onde deva ficar em 3 projetos;
    - cada projeto com pelo menos 1 *goal*;
        - cada *goal* com pelo menos 3 *tags*;
        - cada *goal* com pelo menos 2 atividades, deixe 1 projeto sem.

## Retrieve - busca

1. Liste as informações dos membros de 1 projeto específico que deve ser buscado pelo seu nome de forma a não ligar para maiúsculas e minúsculas.
2. Liste todos os projetos com a tag que você escolheu para os 3 projetos em comum.
3. Liste apenas os nomes de todas as atividades para todos os projetos.
4. Liste todos os projetos que não possuam uma tag.
5. Liste todos os usuários que não fazem parte do primeiro projeto cadastrado.


## Update - alteração

1. Adicione para todos os projetos o campo `views: 0`.
2. Adicione 1 tag diferente para cada projeto.
3. Adicione 2 membros diferentes para cada projeto.
4. Adicione 1 comentário em cada atividade, deixe apenas 1 projeto sem.
5. Adicione 1 projeto inteiro com **UPSERT**.

## Delete - remoção

1. Apague todos os projetos que não possuam *tags*.
2. Apague todos os projetos que não possuam comentários nas atividades.
3. Apague todos os projetos que não possuam atividades.
4. Escolha 2 usuário e apague todos os projetos em que os 2 fazem parte.
5. Apague todos os projetos que possuam uma determinada *tag* em *goal*.

## Sharding
// coloque aqui todos os comandos que você executou

## Replica
// coloque aqui todos os comandos que você executou