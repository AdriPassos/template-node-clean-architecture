
# Node.js Backend Base - Clean Architecture

Este repositório fornece uma base sólida para desenvolvimento backend em Node.js com TypeScript, seguindo os princípios de Clean Architecture e boas práticas de engenharia e arquitetura em camadas e seguindo as boas práticas de mercado.

## Principais Características

- Estrutura em camadas desacopladas (Controller, Service, Repository, Model)

- TypeScript com strict mode habilitado

- Validação robusta com Zod (ou Joi como alternativa)

- Testes com Jest e uso extensivo de mocks

- Pronto para uso com Docker

- Integração contínua com GitHub Actions

## Estrutura de Pastas

src/
├── controllers/    # Entrada da API - Express Handlers
├── services/       # Regras de negócio - Aplicação
├── repositories/   # Acesso a dados - Interface com banco ou APIs
├── models/         # Entidades, DTOs e tipagens (Domain Models)
└── utils/          # Funções auxiliares e helpers

## Padrões Utilizados

- Componente	Tecnologia

-- Framework	Express.js
-- Linguagem	TypeScript (modo strict)
-- Validação	Zod (padrão) ou Joi
-- Testes	Jest com mocks (jest.mock)
-- CI/CD	GitHub Actions
-- Containerização	Docker com Node.js 18

## Pré Requisitos

- Node.js >= 18
- Yarn >= 1.22 ou npm >= 8
- Docker >= 20.x (opcional, para ambiente containerizado)

## Como iniciar

Como Iniciar o Projeto

# Instale as dependências
npm install

# Inicie em modo desenvolvimento
npm run dev

> OBS: O servidor estará disponível em http://localhost:3000 por padrão.

## Scripts Disponíveis

- npm run dev       # Inicia com nodemon
- npm run build     # Compila o projeto para produção (dist/)
- npm run start     # Executa a versão compilada
- npm run test      # Executa os testes unitários com Jest


## Docker

Dockerfile (produção)

FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

RUN npm run build

CMD ["npm", "start"]

## Build e execução com Docker

docker build -t node-backend-clean .
docker run -p 3000:3000 node-backend-clean

## CI com GitHub Actions

.github/workflows/node-ci.yml

name: Node.js CI

on:
  [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [18.x]

    steps:
      - uses: actions/checkout@v3
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: ${{ matrix.node-version }}
      - run: npm ci
      - run: npm run build --if-present
      - run: npm test


## Boas Práticas e Convenções
- Arquivos em snake_case

- Funções e variáveis com nomes descritivos e semânticos

- Uso obrigatório de async/await para operações assíncronas

- Tratamento de erros centralizado (middleware)

- Código limpo, modular e testável

- Separação entre lógica de negócio e transporte (HTTP)

## Melhorias Futuras (To-do)

- Adição de Swagger/OpenAPI para documentação de endpoints

- Configuração de ESLint + Prettier

- Suporte a banco de dados PostgreSQL com ORM (Prisma/TypeORM)

- Autenticação com JWT

- Versionamento de API
