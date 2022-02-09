`\W` => nao palavras
`\w` => paralavras

`^(\d{3}).(\d{3}).(\d{3})-(\d{2})` -> pega os numeros (padrao mais iniciante)

123.123.123-14

321.321.321-32

200.300.500-19


procurar por: `[.-]`

replace por: vazio

---

Wendel, Erick

Gomes, Laila

Johnson, Jose


procurar por: `^(\w+),\s(\w+)`

replace por: `$2 $1`

resultado: Erick Wendel 


---

Wendel, Erick

Gomes, Laila

Johnson, Jose




procurar por: `^(\w+),\s(\w+)`

replace por: `{"firstName": "$2", "lastName": "$1"},`

resultado: 


{"firstName": "Erick", "lastName": "Wendel"},

{"firstName": "Laila", "lastName": "Gomes"},

{"firstName": "Jose", "lastName": "Johnson"},


---

SQL to MongoDB example

`SELECT id, nome, endereco FROM users WHERE id = 1`

`SELECT id, descricao, codigo FROM users WHERE descricao = 'SP'`


desejado: `db.users.find({id: 1 }).project({ id: true, nome: true, endereco: true })`


procurar por: `select\s(.*?)\sfrom\s(.*?)\swhere\s(.*?)\W{2}\s(.*)`

-> lembrar no regex101 -> `/gmi`


explicacao dos grupos:
1. projeção
2. db
3. where field
4. where value 

replace: `db.$2.find({ $3: $4 }).project({ $1 })`

só que, temos os `: true` para resolver


---

dado: `db.users.find({ id: 1 }).project({ id, nome, endereco })`

adicionar a virgula no `project`

dado: `db.users.find({ id: 1 }).project({ id, nome, endereco, })`


procurar por: `(\w+)(?=,)`

replace por: `$1: true`

resultado: `db.users.find({ id: 1 }).project({ id: true, nome: true, endereco: true, })`

