# Tech Challenge Fase 2 - FIAP

## 👥 Integrantes

* Bruno
* Diogo
* Lucas
* Victor


---

# 📑 Sumário

* [Introdução](#introdução)
* [Pré-requisitos](#pré-requisitos)
* [Execução da Aplicação](#execução-da-aplicação)
* [Uso Básico](#uso-básico)
* [Arquitetura do Sistema](#arquitetura-do-sistema)
* [API REST](#api-rest)
* [Modelo de Dados](#modelo-de-dados)
* [Docker e Deploy](#docker-e-deploy)
* [CI/CD](#cicd)
* [Testes](#testes)
* [Swagger](#swagger)

---

# 📌 Introdução

Este projeto consiste no desenvolvimento de uma API REST para gerenciamento de postagens (blog), permitindo operações completas de CRUD (Create, Read, Update, Delete), além de busca por palavras-chave.

A aplicação foi construída utilizando Node.js com TypeScript, integrada ao MongoDB e conteinerizada com Docker, garantindo portabilidade e escalabilidade.

---

# ⚙️ Pré-requisitos

* Node.js 18+
* Docker + Docker Compose
* Git
* Conta no Docker Hub (opcional)

---

# 🚀 Execução da Aplicação

## 🔹 Usando Docker (RECOMENDADO)

```bash
docker compose up --build
```

Acesse:

```
http://localhost:3000/posts
```

Swagger:

```
http://localhost:3000/api-docs
```

---

## 🔹 Usando imagem do Docker Hub

```bash
docker pull SEU_USUARIO/tech-challenge-2-fiap
```

```bash
docker run -d -p 27017:27017 --name mongodb mongo:7
```

```bash
docker run -d \
-p 3000:3000 \
--link mongodb \
-e MONGO_URI=mongodb://mongodb:27017/blog \
SEU_USUARIO/tech-challenge-2-fiap
```

---

## 🔹 Rodando local (sem Docker)

```bash
npm install
npm run dev
```

---

# 📡 Uso Básico

## Criar Post

```bash
POST /posts
```

```json
{
  "title": "Meu Post",
  "content": "Conteúdo",
  "author": "Aluno"
}
```

---

## Listar Posts

```bash
GET /posts
```

---

# 🧠 Arquitetura do Sistema

## Estrutura de Pastas

tech-challenge-2-fiap/
├── .github/
│   └── workflows/
│       └── ci.yml                # Pipeline de CI/CD (GitHub Actions)
│
├── src/                          # Código-fonte da aplicação
│   ├── config/
│   │   ├── database.ts           # Conexão com MongoDB
│   │   └── swagger.ts            # Configuração do Swagger
│   │
│   ├── modules/
│   │   └── post/
│   │       ├── post.controller.ts # Regras de negócio (CRUD)
│   │       ├── post.model.ts      # Schema do MongoDB (Mongoose)
│   │       └── post.routes.ts     # Definição das rotas da API
│   │
│   ├── routes/
│   │   └── index.ts              # Agrupador de rotas
│   │
│   ├── app.ts                    # Configuração do Express
│   └── server.ts                 # Inicialização do servidor
│
├── tests/
│   └── post.test.ts              # Testes unitários com Jest e Supertest
│
├── .dockerignore                 # Arquivos ignorados no build Docker
├── .env                          # Variáveis de ambiente
├── .env.example                  # Exemplo de variáveis de ambiente
├── .gitignore                    # Arquivos ignorados pelo Git
├── docker-compose.yml            # Orquestração dos containers (API + MongoDB)
├── Dockerfile                    # Definição da imagem Docker
├── jest.config.js                # Configuração dos testes
├── package.json                  # Dependências e scripts
├── package-lock.json             # Lock de dependências
├── tsconfig.json                 # Configuração do TypeScript
└── README.md                     # Documentação do projeto

---

## 🧠 Padrão Utilizado

A arquitetura do projeto segue o princípio de **separação de responsabilidades**, organizada de forma modular para garantir escalabilidade, manutenção e clareza no código.

A estrutura é baseada em camadas bem definidas:

- **Model (post.model.ts)**  
  Responsável pela definição do schema e interação com o banco de dados MongoDB, utilizando Mongoose para modelagem dos dados.

- **Controller (post.controller.ts)**  
  Contém a lógica de negócio da aplicação, realizando o processamento das requisições, validações, regras e integração com o Model.

- **Routes (post.routes.ts e routes/index.ts)**  
  Define os endpoints da API e faz o roteamento das requisições HTTP para os respectivos controllers.

- **Config (src/config)**  
  Centraliza configurações da aplicação, como conexão com o banco de dados (`database.ts`) e documentação Swagger (`swagger.ts`).

- **App (app.ts)**  
  Configura os middlewares globais (como JSON e CORS) e registra as rotas da aplicação.

- **Server (server.ts)**  
  Responsável por inicializar o servidor e estabelecer a conexão com o banco de dados.

Essa abordagem modular permite que cada responsabilidade seja isolada, facilitando testes, manutenção e evolução do sistema.

---

# 🔗 API REST

## Endpoints

### GET /posts

Lista todos os posts

### GET /posts/:id

Busca post por ID

### POST /posts

Cria novo post

### PUT /posts/:id

Atualiza post

### DELETE /posts/:id

Remove post

### GET /posts/search?q=termo

Busca por palavra-chave

---

# 🗄️ Modelo de Dados

```json
{
  "_id": "ObjectId",
  "title": "string",
  "content": "string",
  "author": "string",
  "createdAt": "Date",
  "updatedAt": "Date"
}
```

---

# 🐳 Docker e Deploy

## Build manual

```bash
docker build -t SEU_USUARIO/tech-challenge-2-fiap .
```

## Push para Docker Hub

```bash
docker push SEU_USUARIO/tech-challenge-2-fiap
```

---

# ⚙️ CI/CD

Pipeline com GitHub Actions:

* Instala dependências
* Executa testes
* Build da aplicação
* Build da imagem Docker
* Push para Docker Hub

---

# 🧪 Testes

Executar:

```bash
npm test
```

Cobertura:

```bash
npm test -- --coverage
```

## Tipos de testes

* CRUD completo
* Validação de dados
* Tratamento de erros
* Busca

---

# 📘 Swagger

Documentação disponível em:

```
http://localhost:3000/api-docs
```

Permite:

* Visualizar endpoints
* Testar API
* Ver contratos de requisição/resposta

---

# 🏆 Considerações Finais

O projeto demonstra:

* Arquitetura organizada
* Uso de boas práticas
* Containerização com Docker
* Automação com CI/CD
* Testes automatizados
* Documentação com Swagger


