
# Node.js Backend Base - Clean Architecture

Este repositório fornece uma base de backend em Node.js com TypeScript, estruturado com arquitetura em camadas e seguindo as boas práticas da equipe da Alliance.

## Estrutura de Pastas

- `src/controllers` — Entrada da API
- `src/services` — Regras de negócio
- `src/repositories` — Acesso a dados
- `src/models` — Entidades e tipos

## Padrões Utilizados

- Framework: `Express.js`
- Linguagem: `TypeScript` com `strict`
- Validação: `Zod` ou `Joi`
- Testes: `Jest`, com mocks

## Requisitos

- Node.js >= 18
- Yarn ou npm
- Docker (opcional)

## Como iniciar

```bash
npm install
npm run dev
```

## Convenções

- Arquivos em `snake_case`
- Uso de `async/await`
- Variáveis e funções com nomes descritivos


## Docker

```Dockerfile
# Dockerfile para Node.js com TypeScript
FROM node:18

WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .

RUN npm run build
CMD ["npm", "start"]
```

## GitHub Actions - CI

```yaml
# .github/workflows/node-ci.yml
name: Node.js CI

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        node-version: [18.x]

    steps:
    - uses: actions/checkout@v3
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v3
      with:
        node-version: ${{ matrix.node-version }}
    - run: npm ci
    - run: npm run build --if-present
    - run: npm test
```