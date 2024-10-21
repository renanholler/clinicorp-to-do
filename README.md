# Task Management App

Esta aplicação é um sistema simples de gerenciamento de tarefas, onde é possível cadastrar e listar tarefas. A aplicação é composta por um frontend em **React** (utilizando **Vite** e **React Hooks**) e um backend em **Node.js** com **Express**, salvando os dados no **Firestore**. Além disso, foram utilizados **Tailwind CSS** e **Shadcn** para o design dos componentes.

## Funcionalidades

- **Cadastrar tarefas**: Permite adicionar novas tarefas ao sistema.
- **Listar tarefas**: Exibe todas as tarefas cadastradas.
- **Salvamento no Firestore**: O nome do servidor que realizou o cadastro é automaticamente salvo junto com a tarefa.

> **Observação**: Inicialmente, o objetivo era salvar o nome do computador do cliente que fez a requisição. No entanto, por questões de segurança e confiabilidade, optou-se por salvar o nome do servidor que processou o pedido, já que é impraticável e inseguro acessar diretamente o nome da máquina cliente via navegador. O nome do servidor é obtido diretamente, garantindo que o dado seja coletado corretamente em todas as requisições.

## Requisitos

### Requisitos Funcionais

1. O sistema deve permitir cadastrar tarefas.
2. O sistema deve exibir todas as tarefas cadastradas.

### Requisitos Não Funcionais

1. O frontend deve ser desenvolvido com React Hooks e Vite.
2. O backend deve ser em Node.js 20 com Express.
3. O servidor deve conter dois endpoints:
   - **POST** `/insert-tasks`: Insere novas tarefas.
   - **GET** `/get-tasks`: Retorna todas as tarefas em formato JSON.
4. As tarefas são salvas no Firestore e incluem o nome do servidor que processou a inserção.
5. O projeto deve conter testes unitários utilizando Jest.

## Tecnologias Utilizadas

- **Frontend**:
  - React com Hooks
  - Vite
  - Tailwind CSS
  - Shadcn (componentes de UI)

- **Backend**:
  - Node.js 20
  - Express
  - Firestore
  - Jest (para testes unitários)

## Configurações Necessárias

### Firestore

Para que o projeto funcione corretamente, é necessário configurar o Firestore. O backend espera que um arquivo de credenciais do Firestore seja fornecido. Siga os passos abaixo para configurar:

1. No diretório `api`, crie um arquivo `.env` com as seguintes variáveis:
```bash
  FIREBASE_CREDENTIALS_PATH=./src/config/firebaseKey.json
  PORT=3000
```
2. O arquivo de credenciais JSON do Firestore deve estar localizado no caminho especificado em `FIREBASE_CREDENTIALS_PATH` (no exemplo acima, em `./src/config/firebaseKey.json`).
3. O backend utiliza o seguinte código para inicializar a conexão com o Firestore:

```javascript
const admin = require('firebase-admin');
require('dotenv').config();

const { FIREBASE_CREDENTIALS_PATH } = process.env;

admin.initializeApp({
  credential: admin.credential.cert(FIREBASE_CREDENTIALS_PATH),
});

const db = admin.firestore();

module.exports = db;
```

### Frontend

Não são necessárias configurações adicionais para o frontend além das dependências padrão, que podem ser instaladas conforme descrito a seguir.

## Como Executar o Projeto

### Backend (`api`)

1. Instale as dependências:
  ```bash
    npm install
  ```

2. Configure o Firestore conforme mencionado acima.

3. Inicie o servidor:

   ```bash
    npm start
   ```

   O servidor estará rodando em `http://localhost:3000`.

4. Testar endpoints:

   - Para inserir tarefas, use o seguinte comando curl:

     ```bash
     curl -X POST -H "Content-Type: application/json" \
     -d '[{"description":"Criar Login", "responsable":"bruno", "status":"done"}]' \
     http://localhost:3000/insert-tasks
     ```

   - Para listar as tarefas, use:

     ```bash
     curl http://localhost:3000/get-tasks
     ```

### Frontend (`front`)

1. Instale as dependências:

  ```bash
    npm install
  ```

2. Inicie o frontend:

  ```bash
    npm run dev
  ```

   A aplicação estará rodando em `http://localhost:5173`.

### Rodando os Testes

Para executar os testes unitários:
  ```bash
    npm test
  ```
