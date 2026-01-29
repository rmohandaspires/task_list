# Documentacao Tecnica - Tasklist API

## 1) Stack e Versoes
- Node.js (runtime)
- Express 4
- Sequelize 6
- PostgreSQL
- JWT para autenticacao
- Yup para validacao

## 2) Topologia da Aplicacao
- Processo unico Node
- HTTP server na porta 3333
- Banco externo Postgres

## 3) Configuracoes
- Banco: src/config/database.js
  - dialect: postgres
  - host, username, password, database
  - define: timestamps e underscored
- Auth: src/config/auth.js
  - secret: string fixa
  - expiresIn: 7d

## 4) Modelagem de Dados

Tabela users
- id (PK, integer, auto increment)
- name (string)
- email (string, unique)
- password_hash (string)
- created_at, updated_at (date)

Tabela tasks
- id (PK)
- task (string)
- check (boolean, default false)
- user_id (FK -> users.id)
- created_at, updated_at

Associacoes
- Task pertence a User (belongsTo)

## 5) Autenticacao
- Login em /sessions retorna JWT.
- Middleware auth.js valida token e injeta req.userId.
- Rotas protegidas ficam abaixo do middleware em routes.js.

## 6) Validacao de Entrada
- Yup valida payload de usuarios e tarefas.
- Erros de validacao retornam 400 com { "error": "Falha na validacao." }.

## 7) Fluxos principais

Cadastro
- POST /users -> UserController.store
- Verifica email unico e cria usuario.

Login
- POST /sessions -> SessionController.store
- Verifica usuario e senha, retorna token.

Atualizacao de usuario
- PUT /users -> UserController.update
- Exige token
- Para troca de senha: oldPassword + password + confirmPassword.
- Valida email unico.

Tarefas
- POST /tasks cria tarefa com user_id do token.
- GET /tasks lista tarefas do usuario onde check = false.
- PUT /tasks/:task_id atualiza tarefa.
- DELETE /tasks/:task_id remove tarefa (apenas do proprio usuario).

## 8) Erros comuns
- 401 Token nao existe / Token invalido
- 401 Usuario nao existe / Senha incorreta
- 400 Falha na validacao
- 400 Usuario ja existe / Tarefa nao existe

## 9) Scripts e CLI
- Iniciar: yarn dev
- Migrations: yarn sequelize db:migrate

## 10) Pontos de Atencao
- Segredo JWT hardcoded (ideal usar env).
- Sem rate limit e sem CORS configurado.
- Nao ha refresh token.
