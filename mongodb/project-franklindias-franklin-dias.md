# MongoDB - Projeto Final
- **Autor:** Franklin Dias
- **Data:** 16/12/2015

## Para qual sistema você usaria o MogoDB (diferente desse)?
Bancos de dados não relacionais em geral podem ser utilizados pra qualquer tipo de sistema, entretato é indicado àqueles que necessitam de uma interação mais rápida entre os dados e a aplicação não importando a replicação de dado, o que acontece normalmente em aplicações 'real time' e nas aplicações que demadam muito fluxo de dados. Sendo assim, além de várias outras aplicações, eu poderia usar o MongoDB tranquilamente em um sistema de E-commerce, por exemplo. Um outro exemplo que poderíamos utilizar banco de dados NoSql são as redes socias, porém para estes é indicado utilizar um banco baseado em Grafos, como o Neo4j.


## Qual a modelagem da sua coleção de 'users'?

[USERS - Em Andamento] (https://github.com/franklindias/be-mean-instagram-projects/blob/master/mongodb/model_users.md)

## Qual a modelagem da sua coleção de 'projects'?

[PROJECTS - Em Andamento] (https://github.com/franklindias/be-mean-instagram-projects/blob/master/mongodb/model_projects.md)

## Qual a modelagem da sua coleção retirada de 'projects'?

[ACTIVITIES - Em Andamento] (https://github.com/franklindias/be-mean-instagram-projects/blob/master/mongodb/model_activities.md)

## Create - cadastro

> 1 - Cadastre 10 usuários diferentes.

Inserindo um usuário manualmente:

```js
localhost(mongod-2.6.11) project> var user = {  
	"name":"Franklin Dias",  
	"bio":"bio de franklin",  
	"email":"franklindias99@gmail.com",  
	"date_register":ISODate(),  
	"avatar_path":"",
    "auth": {  
		"username":"franklindias",  
		"password":"123",  
		"last_access":ISODate(),  
		"online":false,  
		"disable":false,  
		"hash_token":"202cb962ac59075b964b07152d234b70"  
	}
}
```
Salvando objeto user.

```js
localhost(mongod-2.6.11) project> db.users.save(user)
Inserted 1 record(s) in 529ms
WriteResult({
  "nInserted": 1
})
```

Listando usuário cadastrado.

```js
localhost(mongod-2.6.11) project> db.users.find()
{
  "_id": ObjectId("567db311db60e19fa4f7f2bd"),
  "name": "Franklin Dias",
  "bio": "bio de franklin",
  "email": "franklindias99@gmail.com",
  "date_register": ISODate("2015-12-25T21:16:44.716Z"),
  "avatar_path": "",
  "auth": {
    "username": "franklindias",
    "password": "123",
    "last_access": ISODate("2015-12-25T21:16:44.716Z"),
    "online": false,
    "disable": false,
    "hash_token": "202cb962ac59075b964b07152d234b70"
  }
}
Fetched 1 record(s) in 3ms
```

Em seguida criei um arquivo json contendo os outros 9 usuários necessários e fiz a importação: [users_insert.json](https://github.com/franklindias/be-mean-instagram-projects/blob/master/mongodb/data/users_insert.json).



```js
mongoimport --db project --collection users --file users_insert.json
connected to: 127.0.0.1
2015-12-25T20:18:59.199-0200 imported 9 objects
```

> 2 - Cadastre 5 projetos diferentes.

Para facilitar, didaticamente, a inserção dos objetos, inseri inicialmente as 'activities' e em seguida inseri os projetos com suas respectivas 'atividades', considerando que cada projeto terá 2 atividades [activities_insert.json](https://github.com/franklindias/be-mean-instagram-projects/blob/master/mongodb/data/activities_insert.json).


```js
mongoimport --db project --collection activities --file data/activities_insert.json 
connected to: 127.0.0.1
2015-12-25T21:25:26.528-0200 imported 10 objects
```

Em seguida, criei um arquivo json com todos os projetos, 'relacionando' seus respectivos usuários e atividades já cadastradas: [projects_insert.json] (https://github.com/franklindias/be-mean-instagram-projects/blob/master/mongodb/data/projects_insert.json).


```js
mongoimport --db project --collection projects --file data/projects_insert.json 
connected to: 127.0.0.1
2015-12-25T22:32:16.830-0200 imported 5 objects

```

## Retrieve - busca

> 1. Liste as informações dos membros de 1 projeto específico que deve ser buscado pelo seu nome de forma a não ligar para maiúsculas e minúsculas.

Criando o filtro para selecionar o projeto.
```js
localhost(mongod-2.6.11) project> var filter = {name: /projeto 3/i }
```

Instanciando array para utilização futura, caso contrário daria erro no momento de chamar a função 'push' na função a seguir.
```js
localhost(mongod-2.6.11) project> var users = [];
```

Varrendo o campo 'project_members' do objeto buscado, e em seguida varrendo o array resultante da consulta e inserindo os respectivos usuários no array users. 
```js
db.projects.findOne(filter, { "project_members.user":1, "_id":0}).project_members.forEach(function(member) {
    users.push(db.users.findOne({"_id":member.user}))
});
```

Listando os membros do 'Projeto 3'
```js
localhost(mongod-2.6.11) project> users
[
  {
    "_id": ObjectId("567dc0d33035895fd8c5c3ec"),
    "name": "José Costa",
    "bio": "bio de jose",
    "email": "jose@email.com",
    "date_register": ISODate("2015-12-25T21:16:44.716Z"),
    "avatar_path": "",
    "auth": {
      "username": "josecosta",
      "password": "123",
      "last_access": ISODate("2015-12-25T21:16:44.716Z"),
      "online": false,
      "disable": false,
      "hash_token": "202cb962ac523654964b07152d234b70"
    }
  },
  {
    "_id": ObjectId("567dc0d33035895fd8c5c3ed"),
    "name": "Maria Clara",
    "bio": "bio de maria",
    "email": "maria@email.com",
    "date_register": ISODate("2015-12-25T21:16:44.716Z"),
    "avatar_path": "",
    "auth": {
      "username": "mariaclara",
      "password": "123",
      "last_access": ISODate("2015-12-25T21:16:44.716Z"),
      "online": false,
      "disable": false,
      "hash_token": "202cb962ac59075b964b07152d234b70"
    }
  },
  {
    "_id": ObjectId("567dc0d33035895fd8c5c3ee"),
    "name": "Francisco Pereira",
    "bio": "bio de francisco",
    "email": "francisco@email.com",
    "date_register": ISODate("2015-12-25T21:16:44.716Z"),
    "avatar_path": "",
    "auth": {
      "username": "franciscopereira",
      "password": "123",
      "last_access": ISODate("2015-12-25T21:16:44.716Z"),
      "online": false,
      "disable": false,
      "hash_token": "202cb9612c1a075b964b07152d234b70"
    }
  },
  {
    "_id": ObjectId("567dc0d33035895fd8c5c3ef"),
    "name": "Gilberto Lima",
    "bio": "bio de gilberto",
    "email": "gilbertolima@email.com",
    "date_register": ISODate("2015-12-25T21:16:44.716Z"),
    "avatar_path": "",
    "auth": {
      "username": "gilmerto",
      "password": "123",
      "last_access": ISODate("2015-12-25T21:16:44.716Z"),
      "online": false,
      "disable": false,
      "hash_token": "202cb962ac5s1e75b964b07152d234b70"
    }
  },
  {
    "_id": ObjectId("567dc0d33035895fd8c5c3f0"),
    "name": "Luciana",
    "bio": "bio de luciana",
    "email": "luci@gmail.com",
    "date_register": ISODate("2015-12-25T21:16:44.716Z"),
    "avatar_path": "",
    "auth": {
      "username": "luci",
      "password": "123",
      "last_access": ISODate("2015-12-25T21:16:44.716Z"),
      "online": false,
      "disable": false,
      "hash_token": "202cb1f1ac59075b964b07152d234b70"
    }
  }
]

```


> 2. Liste todos os projetos com a tag que você escolheu para os 3 projetos em comum.

```js
localhost(mongod-2.6.11) project> db.projects.find({project_tags: {$in: [/node/i]}}, {name: 1})
{
  "_id": ObjectId("567de0103035895fd8c5c3ff"),
  "name": "Projeto 1"
}
{
  "_id": ObjectId("567de0103035895fd8c5c400"),
  "name": "Projeto 2"
}
{
  "_id": ObjectId("567de0103035895fd8c5c401"),
  "name": "Projeto 3"
}
Fetched 3 record(s) in 3ms

```

> 3. Liste apenas os nomes de todas as atividades para todos os projetos.

```js
localhost(mongod-2.6.11) project> db.activities.find({}, {name:1, _id:0})
{
  "name": "Activitie 1"
}
{
  "name": "Activitie 2"
}
{
  "name": "Activitie 3"
}
{
  "name": "Activitie 4"
}
{
  "name": "Activitie 5"
}
{
  "name": "Activitie 6"
}
{
  "name": "Activitie 7"
}
{
  "name": "Activitie 8"
}
{
  "name": "Activitie 9"
}
{
  "name": "Activitie 10"
}

```

> 4. Liste todos os projetos que não possuam uma tag.

```js
db.projects.find({project_tags: {$size: 0}}) 
Fetched 0 record(s) in 1ms
```

> 5. Liste todos os usuários que não fazem parte do primeiro projeto cadastrado.

```js
localhost(mongod-2.6.11) project> db.projects.find({}, {'name':1,'project_members.user': 1}).skip(1)
{
  "_id": ObjectId("567de0103035895fd8c5c400"),
  "name": "Projeto 2",
  "project_members": [
    {
      "user": ObjectId("567dbff3c2289ba833ee8741")
    },
    {
      "user": ObjectId("567dc0d33035895fd8c5c3ec")
    },
    {
      "user": ObjectId("567dc0d33035895fd8c5c3ed")
    },
    {
      "user": ObjectId("567dc0d33035895fd8c5c3ee")
    },
    {
      "user": ObjectId("567dc0d33035895fd8c5c3ef")
    }
  ]
}
{
  "_id": ObjectId("567de0103035895fd8c5c401"),
  "name": "Projeto 3",
  "project_members": [
    {
      "user": ObjectId("567dc0d33035895fd8c5c3ec")
    },
    {
      "user": ObjectId("567dc0d33035895fd8c5c3ed")
    },
    {
      "user": ObjectId("567dc0d33035895fd8c5c3ee")
    },
    {
      "user": ObjectId("567dc0d33035895fd8c5c3ef")
    },
    {
      "user": ObjectId("567dc0d33035895fd8c5c3f0")
    }
  ]
}
{
  "_id": ObjectId("567de0103035895fd8c5c402"),
  "name": "Projeto 4",
  "project_members": [
    {
      "user": ObjectId("567dc0d33035895fd8c5c3ed")
    },
    {
      "user": ObjectId("567dc0d33035895fd8c5c3ee")
    },
    {
      "user": ObjectId("567dc0d33035895fd8c5c3ef")
    },
    {
      "user": ObjectId("567dc0d33035895fd8c5c3f0")
    },
    {
      "user": ObjectId("567dc0d33035895fd8c5c3f1")
    }
  ]
}
{
  "_id": ObjectId("567deb9d3086e408cf4a2fe0"),
  "name": "Projeto 5",
  "project_members": [
    {
      "user": ObjectId("567dc0d33035895fd8c5c3ee")
    },
    {
      "user": ObjectId("567dc0d33035895fd8c5c3ef")
    },
    {
      "user": ObjectId("567dc0d33035895fd8c5c3f1")
    },
    {
      "user": ObjectId("567dc0d33035895fd8c5c3f3")
    },
    {
      "user": ObjectId("567dc0d33035895fd8c5c3f4")
    }
  ]
}
Fetched 4 record(s) in 2ms

```

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