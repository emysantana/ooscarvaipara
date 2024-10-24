# ooscarvaipara
E o Oscar vai para...?

1- Quantas vezes Natalie Portman foi indicada ao Oscar?

R: Natalie Portman foi indicada 3 vezes.
```js
db["cerimônia do oscar"].countDocuments({nome_do_indicado: "Natalie Portman"})

```

2- Quantos Oscars Natalie Portman ganhou?

R: Natalie Portman ganhou 1 vez.
```js
db["cerimônia do oscar"].countDocuments({nome_do_indicado: "Natalie Portman", vencedor: "true"})

```

3- Amy Adams já ganhou algum Oscar?

R: Amy Adams nunca ganhou.
```js
db["cerimônia do oscar"].countDocuments({nome_do_indicado: "Amy Adams", vencedor: "true"})

```

4- 4- A série de filmes Toy Story ganhou um Oscar em quais anos?

R: Toy Story ganhou em 2011 e 2020.
```js
db["cerimônia do oscar"].find({nome_do_filme: {$in:
 ["Toy Story 1", "Toy Story 2", "Toy Story 3", "Toy Story 4"]} , vencedor: "true"})

```

5- A partir de que ano que a categoria "Actress" deixa de existir? 

R: 1976.
```js
db["cerimônia do oscar"].aggregate([{ $match: {categoria: "ACTRESS" } },{ $sort:
{ ano_cerimonia: -1 } },{ $project: { ano_cerimonia: 1 } }, {$limit: 1 } ])

```

6- O primeiro Oscar para melhor Atriz foi para quem? Em que ano?

R: Janet Gaynor.
```js
db["cerimônia do oscar"].find({
vencedor: "true", categoria: "ACTRESS"},
{nome_do_indicado: 1, _id: 0}).limit(1)

```

7- Na campo "Vencedor", altere todos os valores com "Sim" para 1 e todos os valores "Não" para 0.

```js
db["cerimônia do oscar"].updateMany( { "vencedor": "false"}, { $set: { "vencedor": 0 } } );
db["cerimônia do oscar"].updateMany( { "vencedor": "true" }, { $set: { "vencedor": 1 } } ),

```

8- Em qual edição do Oscar "Crash" concorreu ao Oscar?

R: No ano 2008, mais precisamente na 78º cerimônia do Oscar.

```js
db["cerimônia do oscar"].find({ "nome_do_filme": "Crash"},
{ "cerimonia": 1,
"ano_cerimonia": 1, "_id": 0 }).limit(1)

```

9- Bom... dê um Oscar para um filme que merece muito, mas não ganhou.

R: Toy Story 1.

```js
db["cerimônia do oscar"].updateOne({ "nome_do_filme":
"Toy Story 1" }, { $set: { "vencedor": "0" } } );

```

10- O filme Central do Brasil aparece no Oscar?

R: 2 vezes.

```js
db["cerimônia do oscar"].find({ nome_do_filme:
 "Central Statiom"})

```

11- Inclua no banco 3 filmes que nunca foram nem nomeados ao Oscar, mas que merecem ser. 

R: O Auto da Compadecida, Como Criar um Garoto Perfeito, Zapped.

```js
db["cerimônia do oscar"]. insertMany([
{"id_registro":7800, "ano_filmagem":"2000", "ano_cerimonia":"2001",
"cerimonia": "73",
"categoria": "Actor",
"nome_do_indicado": "Selton Mello",
"nome_do_filme": "O Auto da Compadecida", "vencedor: 1 "}}

db["cerimônia do oscar"]. insertMany([
{"id_registro":7800, "ano_filmagem":"2014", "ano_cerimonia":"2015",
"cerimonia": "87",
"categoria": "Actress",
"nome_do_indicado": "China Anne McClaim",
"nome_do_filme": "Como Criar um Garoto Perfeito", "vencedor: 1 "}}

db["cerimônia do oscar"]. insertMany([
{"id_registro":7800, "ano_filmagem":"2014", "ano_cerimonia":"2015",
"cerimonia": "87",
"categoria": "Best Original Screenplay",
"nome_do_indicado": "Zendaya",
"nome_do_filme": "Zapped", "vencedor: 1 "}}

```

12 - Pensando no ano em que você nasceu: Qual foi o Oscar de melhor filme, Melhor Atriz e Melhor Diretor?

R: Menina de Ouro, Melhor Filme é da Hilary Swank, Melhor Diretor Clint Eastwood
```js
db["cerimônia do oscar"].find({"categoria":
 {"$in": ["DIRECTING", "ACTRESS IN A LEADING ROLE",
"BEST PICTURE"]}, "ano_cerimonia":2005, "vencedor":1} )

```










