# Documentacao do Projeto Tasklist

Resumo
Este projeto e uma API REST em Node.js/Express para cadastro de usuarios, autenticacao via JWT e gerenciamento de tarefas (tasks). Usa PostgreSQL via Sequelize.

Arquitetura e Estrutura
- src/server.js: inicia o servidor e escuta na porta 3333.
- src/app.js: configura middlewares e rotas.
- src/routes.js: define as rotas publicas e protegidas.
- src/app/controllers: logica de negocio para usuarios, sessao e tarefas.
- src/app/models: modelos Sequelize (User, Task).
- src/app/middlewares/auth.js: middleware de autenticacao JWT.
- src/database/index.js: inicializa Sequelize e associa modelos.
- src/database/migrations: migrations para criar tabelas users e tasks.
- src/config/database.js: configuracao do banco.
- src/config/auth.js: segredo e expiracao do JWT.

Fluxo de Autenticacao
1) POST /users cria usuario.
2) POST /sessions autentica e retorna token.
3) Rotas protegidas exigem header Authorization: Bearer <token>.

Diagrama simples (ASCII)

Cadastro e Login
   [Cliente] ---> POST /users -----------------> [API] ---> [DB]
       |                                         |
       +---> POST /sessions -------------------->+--> valida senha -> token JWT

Acesso a Rotas Protegidas
   [Cliente] -- Authorization: Bearer <token> --> [auth middleware]
                                       |            |
                                       +-- valido -->[Controller]-->[DB]
                                       +-- invalido->[401]

Rotas e Endpoints (resumo)
- POST /users: cadastra usuario.
- POST /sessions: login e token.
- PUT /users: atualiza usuario logado.
- POST /tasks: cria tarefa.
- GET /tasks: lista tarefas nao concluídas do usuario.
- PUT /tasks/:task_id: atualiza tarefa.
- DELETE /tasks/:task_id: remove tarefa.

Regras de Negocio Principais
- Email de usuario e unico.
- Senhas sao armazenadas como hash (bcryptjs).
- Atualizacao de senha exige oldPassword e confirmPassword.
- Tarefas pertencem a um usuario e nao podem ser apagadas por outro.

Dependencias
- Runtime: express, sequelize, pg, pg-hstore, bcryptjs, jsonwebtoken, yup.
- Dev: sequelize-cli, nodemon, sucrase, eslint, prettier e plugins.

Execucao
- Iniciar API: yarn dev
- Rodar migrations: yarn sequelize db:migrate

Arquivos de Documentacao
- docs/API.md: endpoints detalhados, payloads e responses.
- docs/PLUGINS.md: dependencias com descricao e exemplos.
