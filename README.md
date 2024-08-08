# Tutoriais  

## Turma 01
- Alan 
  - https://github.com/0Rocha/2024-IA22-2TRI
- Antony 
  - https://github.com/GabrielSilva47/2024-IA22-2TRI.git
- Arthur 
  - https://github.com/arpbr/2024-IA22-2TRI
- Carolina 
  - https://github.com/Carolina-Da-Silva/2024-IA22-2TRI
- Carolina Crestani 
  - https://github.com/Kriegs1889/2024-IA22-2TRI
- Carolina da Silva
  - https://github.com/Carolina-Da-Silva/2024-IA22-2TRI.git
- Cristian 
  - https://github.com/CrishBic/2024-IA22-2TRI-Cristian
- Edson 
  - github.com/Edson-Edu
- Eduardo Minosso 
  - https://github.com/Eduard0liveira/2024-IA22-2TRI
- Eduardo proença 
  - https://github.com/EduardoCruz78/AtividadeProg2
- Emanuella 
  - https://github.com/EmanuellaPereira01/Atv2TrimestreManu.git
- Érick 
  - https://github.com/Erickkullmann/2024-IA22-2TRI
- Gabriel 
  - https://github.com/GabrielRicardo1
- Hiago de Araújo Pereira
  - https://github.com/caomuna/2024-IA22-2TRI
- hugo 
  - https://github.com/Hou-woo/2024-IA22-2TRI
- iuri 
  - https://github.com/iuri2007/2024-IA22-2TRI
- joão pelegrin 
  - https://github.com/Joaovitordepelegrin/2024-IA22-2TRi

## Turma 02
- João gomes 
  - https://github.com/Gomes047/2024-IA22-2TRI
- Josué 
  - https://github.com/Sholipatv
- Kallebi 
  - https://github.com/kallebi10 
- Leticia 
  - github.com/leh-lima
- Lucas 
  - https://github.com/lucasmirandak/2024-IA22-2TRI
- Marcos Domainski 
  - https://github.com/domainski2/IAMarcos2024-IA22-2TRI
- Marcus 
  - https://github.com/fentanylity/2024-2TRI-IA22
- Nícolas Ferreira dos Santos
  - https://github.com/nicolicof/2024-IA22-2TRI
- Raquel 
  - https://github.com/raquelgw/2024-IA22-2TRI
- Rhai 
  - https://github.com/Rhaiiiii/projeto-IA22.git
- Roger Alan 
  - https://github.com/helo-wordd/2024-IA22-2TRI
- Roger Eduardo 
  - https://github.com/reczin
- Ronald 
  - https://github.com/IARonald/2024-IA22-2TRI
- Yan 
  - https://github.com/YanWeberFrancelino/2024-IA22-2TRI
- Yasmim Rassoul Rebello
  - https://github.com/YBroflovski/2024-IA22-2TRI-Yasmim
- Yasmin andrade 
  - https://github.com/yasandradeRJ/2024-IA22

# Iniciando um projeto Node.js com TypeScript

Crie um diretório para o projeto e acesse-o pelo vscode, abra o terminal e siga os passos abaixo.

```bash
npm init -y
npm install express cors sqlite3 sqlite
npm install --save-dev typescript nodemon ts-node @types/express @types/cors
npx tsc --init
mkdir src
touch src/app.ts
```

## Configuranado o `tsconfig.json`

<<<<<<< HEAD
Mude a linha ```"outDir": "./",``` para ```"outDir": "./dist",``` e adicione a linha ```"rootDir": "./src",```, seu arquivo de configuração do compilador do TypeScript ficará mais ou menos assim.
=======
Mude a linha utilizando a barra de pesquisa localizada no centro superior da tela ` "outDir": "./" ` , para 
` "outDir": "./dist" ` e adicione embaixo na linha ` "rootDir": "./"` e coloque ` "rootDir": "./src"`, seu arquivo de configuração do compilador do TypeScript ficará mais ou menos assim.
>>>>>>> dcdbc44 (...)

```json
{
  "compilerOptions": {
    "target": "ES2017",
    "module": "commonjs",
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true
  }
}
<<<<<<< HEAD
```
=======
```` 
# Configurando o `package.json`
>>>>>>> dcdbc44 (...)

## Configurando o `package.json`

Adicione o seguinte script ao seu `package.json`

<<<<<<< HEAD
```json
"scripts": {
  "dev": "nodemon src/app.ts"
}
```
=======
Na linha seguinte estará escrito o seguinte:
```javascript
 "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
````
Não esqueça a vírgula ao lado do `"test": "echo \"Error: no test specified\" && exit 1"`

Adicione o seguinte na linha abaixo do `"test": [...]`:
>>>>>>> dcdbc44 (...)

## Criando arquivo inicial do servidor

```typescript
import express from 'express';
import cors from 'cors';

const port = 3333;
const app = express();

app.use(cors());
app.use(express.json());

app.get('/', (req, res) => {
  res.send('Hello World');
});

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

## Inicializando o servidor

```bash
npm run dev
```

Se tudo ocorrer bem, você verá a mensagem `Server running on port 3333` no terminal.

## Testando o servidor

Abra o navegador e acesse `http://localhost:3333`, você verá a mensagem `Hello World`.

## Configurando o banco de dados

Crie um arquivo `database.ts` dentro da pasta `src` e adicione o seguinte código.

```typescript
import { open, Database } from 'sqlite';
import sqlite3 from 'sqlite3';

let instance: Database | null = null;

export async function connect() {
  if (instance) return instance;

  const db = await open({
     filename: './src/database.sqlite',
     driver: sqlite3.Database
   });
  
  await db.exec(`
    CREATE TABLE IF NOT EXISTS users (
      id INTEGER PRIMARY KEY AUTOINCREMENT,
      name TEXT,
      email TEXT
    )
  `);

  instance = db;
  return db;
}
```

## Adicionando o banco de dados ao servidor

```typescript
import express from 'express';
import cors from 'cors';
import { connect } from './database';

const port = 3333;
const app = express();

app.use(cors());
app.use(express.json());

app.get('/', (req, res) => {
  res.send('Hello World');
});

app.post('/users', async (req, res) => {
  const db = await connect();
  const { name, email } = req.body;

  const result = await db.run('INSERT INTO users (name, email) VALUES (?, ?)', [name, email]);
  const user = await db.get('SELECT * FROM users WHERE id = ?', [result.lastID]);

  res.json(user);
});

app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

## Testando a inserção de dados

Abra o Postman e faça uma requisição POST para `http://localhost:3333/users` com o seguinte corpo.

```json
{
  "name": "John Doe",
  "email": "johndoe@mail.com"
}
```

Se tudo ocorrer bem, você verá a resposta com o usuário inserido.

```json
{
  "id": 1,
  "name": "John Doe",
  "email": "johndoe@mail.com"
}
```

## Listando os usuários

<<<<<<< HEAD
Adicione a rota `/users` ao servidor.
=======
# Atualize ``teste.http``
Ele ficará assim

```javascript
POST https://localhost:3333/users HTTP/1.1
Content-Type: application/json
Authorization: token xxx

{
  "name": "John Doe",
  "email": "john@example.com"
}
####

PUT https://localhost:3333/users/1 HTTP/1.1
Content-Type: application/json

{
  "name": "John Doe update",
  "email": "john@example.com"
}

####

DELETE https://localhost:3333/users/1 HTTP/1.1

```` 
Tambem alteraremos ``app.ts``
```javascript
import express from 'express';
import cors from 'cors';
import { connect } from './database';

const port = 3333;
const app = express();

app.use(cors());
app.use(express.json());

app.get('/', (req, res) => {
  res.send('Hello World');
});

app.post('/users', async (req, res) => {
  const db = await connect();
  const { name, email } = req.body;

  const result = await db.run('INSERT INTO users (name, email) VALUES (?, ?)', [name, email]);
  const user = await db.get('SELECT * FROM users WHERE id = ?', [result.lastID]);

  res.json(user);
});
>>>>>>> dcdbc44 (...)

```typescript
app.get('/users', async (req, res) => {
  const db = await connect();
  const users = await db.all('SELECT * FROM users');

  res.json(users);
});
```

## Editando um usuário

Adicione a rota `/users/:id` ao servidor.

```typescript
app.put('/users/:id', async (req, res) => {
  const db = await connect();
  const { name, email } = req.body;
  const { id } = req.params;

  await db.run('UPDATE users SET name = ?, email = ? WHERE id = ?', [name, email, id]);
  const user = await db.get('SELECT * FROM users WHERE id = ?', [id]);

  res.json(user);
});
```

## Deletando um usuário

Adicione a rota `/users/:id` ao servidor.

```typescript
app.delete('/users/:id', async (req, res) => {
  const db = await connect();
  const { id } = req.params;

  await db.run('DELETE FROM users WHERE id = ?', [id]);

  res.json({ message: 'User deleted' });
});
```
