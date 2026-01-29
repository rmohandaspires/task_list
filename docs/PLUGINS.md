# Plugins e Dependencias

Este projeto usa as dependencias abaixo (runtime e desenvolvimento). Cada item inclui descricao, exemplo no codigo e comando de instalacao com yarn.

Dependencias (runtime)

1) express
- Para que serve: framework web para criar API HTTP.
- Exemplo no codigo: src/app.js
  - cria servidor e registra rotas.
- Instalacao:
  yarn add express

2) sequelize
- Para que serve: ORM para PostgreSQL (modelos, consultas e migrations).
- Exemplo no codigo: src/database/index.js, src/app/models/User.js, src/app/models/Task.js
  - inicializa conexao e define models.
- Instalacao:
  yarn add sequelize

3) pg
- Para que serve: driver do PostgreSQL para Node.
- Exemplo no codigo: usado pelo Sequelize via src/config/database.js (dialect postgres).
- Instalacao:
  yarn add pg

4) pg-hstore
- Para que serve: suporte a campos do tipo hstore no PostgreSQL (dependencia comum do Sequelize + Postgres).
- Exemplo no codigo: indireto via Sequelize (nenhum uso direto em arquivo).
- Instalacao:
  yarn add pg-hstore

5) bcryptjs
- Para que serve: hash e verificacao de senha.
- Exemplo no codigo: src/app/models/User.js
  - hash no hook beforeSave e compare em checkPassword.
- Instalacao:
  yarn add bcryptjs

6) jsonwebtoken
- Para que serve: gerar e validar JWT de autenticacao.
- Exemplo no codigo: src/app/controllers/SessionController.js e src/app/middlewares/auth.js
  - gera token no login e valida nas rotas protegidas.
- Instalacao:
  yarn add jsonwebtoken

7) yup
- Para que serve: validacao de payloads.
- Exemplo no codigo: src/app/controllers/UserController.js e src/app/controllers/TaskController.js
  - valida campos de cadastro e update.
- Instalacao:
  yarn add yup

Dependencias (desenvolvimento)

1) sequelize-cli
- Para que serve: CLI para migrations e comandos do Sequelize.
- Exemplo no codigo: usa .sequelizerc e migrations em src/database/migrations.
- Exemplos de comandos:
  - Criar migration: yarn sequelize migration:create --name create-users
  - Rodar migrations: yarn sequelize db:migrate
  - Reverter ultima migration: yarn sequelize db:migrate:undo
- Instalacao:
  yarn add -D sequelize-cli

2) nodemon
- Para que serve: reinicia o servidor ao salvar arquivos.
- Exemplo no codigo: script "dev" em package.json e config em nodemon.json.
- Exemplos de comandos:
  - Iniciar em modo desenvolvimento: yarn dev
  - Rodar diretamente: npx nodemon src/server.js
- Instalacao:
  yarn add -D nodemon

3) sucrase
- Para que serve: transpilar import/export do Node em runtime (usado pelo nodemon em alguns setups).
- Exemplo no codigo: uso indireto pela configuracao do ambiente.
- Instalacao:
  yarn add -D sucrase

4) eslint
- Para que serve: lint de codigo JS.
- Exemplo no codigo: configuracao em .eslintrc.js.
- Instalacao:
  yarn add -D eslint

5) eslint-config-airbnb-base
- Para que serve: regras base do Airbnb para JS.
- Exemplo no codigo: configuracao em .eslintrc.js.
- Instalacao:
  yarn add -D eslint-config-airbnb-base

6) eslint-plugin-import
- Para que serve: regras do ESLint para validacao de imports.
- Exemplo no codigo: configuracao em .eslintrc.js.
- Instalacao:
  yarn add -D eslint-plugin-import

7) prettier
- Para que serve: formatador de codigo.
- Exemplo no codigo: configuracao em .prettierrc.
- Instalacao:
  yarn add -D prettier

8) eslint-config-prettier
- Para que serve: desliga regras do ESLint que conflitam com o Prettier.
- Exemplo no codigo: configuracao em .eslintrc.js.
- Instalacao:
  yarn add -D eslint-config-prettier

9) eslint-plugin-prettier
- Para que serve: integra Prettier ao ESLint.
- Exemplo no codigo: configuracao em .eslintrc.js.
- Instalacao:
  yarn add -D eslint-plugin-prettier
