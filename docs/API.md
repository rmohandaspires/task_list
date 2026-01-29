# Tasklist API

Resumo
- API REST em Node/Express para cadastro de usuarios, autenticacao via JWT e gerenciamento de tarefas.
- Banco: PostgreSQL via Sequelize.

Base URL
- http://localhost:3333

Autenticacao (fluxo)
1) Crie um usuario em POST /users.
2) Faça login em POST /sessions e receba o token JWT.
3) Envie o token nas rotas protegidas usando o header:
   - Authorization: Bearer <token>

Observacoes gerais
- Todas as rotas abaixo do middleware de autenticacao exigem token valido.
- Respostas de erro seguem o formato: { "error": "mensagem" }
- Campos com datas usam timestamps do Sequelize: created_at e updated_at.

Endpoints

1) POST /users
- Descricao: cria um novo usuario.
- Protegido: nao
- Payload (JSON):
  {
    "name": "Joao",
    "email": "joao@email.com",
    "password": "123456"
  }
- Response 200:
  {
    "id": 1,
    "name": "Joao",
    "email": "joao@email.com"
  }
- Erros comuns:
  - 400 { "error": "Falha na validacao." }
  - 400 { "error": "Usuario ja existe." }

2) POST /sessions
- Descricao: autentica usuario e retorna token JWT.
- Protegido: nao
- Payload (JSON):
  {
    "email": "joao@email.com",
    "password": "123456"
  }
- Response 200:
  {
    "user": {
      "id": 1,
      "name": "Joao",
      "email": "joao@email.com"
    },
    "token": "<jwt>"
  }
- Erros comuns:
  - 401 { "error": "Usuario nao existe." }
  - 401 { "error": "Senha incorreta." }

3) PUT /users
- Descricao: atualiza dados do usuario autenticado.
- Protegido: sim
- Header:
  Authorization: Bearer <token>
- Payload (JSON) (todos opcionais, mas com regras):
  {
    "name": "Novo Nome",
    "email": "novo@email.com",
    "oldPassword": "123456",
    "password": "654321",
    "confirmPassword": "654321"
  }
- Regras:
  - Para trocar senha, enviar oldPassword e password.
  - confirmPassword deve ser igual a password.
- Response 200:
  {
    "id": 1,
    "name": "Novo Nome",
    "email": "novo@email.com"
  }
- Erros comuns:
  - 400 { "error": "Falha na validacao." }
  - 400 { "error": "Usuario ja existe." }
  - 401 { "error": "Senha incorreta." }

4) POST /tasks
- Descricao: cria uma tarefa para o usuario autenticado.
- Protegido: sim
- Header:
  Authorization: Bearer <token>
- Payload (JSON):
  {
    "task": "Comprar leite"
  }
- Response 200 (exemplo):
  {
    "id": 1,
    "task": "Comprar leite",
    "check": false,
    "user_id": 1,
    "created_at": "2019-11-15T02:00:00.000Z",
    "updated_at": "2019-11-15T02:00:00.000Z"
  }
- Erros comuns:
  - 400 { "error": "Falha ao cadastrar. " }

5) GET /tasks
- Descricao: lista tarefas do usuario autenticado que ainda nao foram concluídas.
- Protegido: sim
- Header:
  Authorization: Bearer <token>
- Response 200 (exemplo):
  [
    {
      "id": 1,
      "task": "Comprar leite",
      "check": false,
      "user_id": 1,
      "created_at": "2019-11-15T02:00:00.000Z",
      "updated_at": "2019-11-15T02:00:00.000Z"
    }
  ]

6) PUT /tasks/:task_id
- Descricao: atualiza uma tarefa por id.
- Protegido: sim
- Header:
  Authorization: Bearer <token>
- Params:
  - task_id (numero)
- Payload (JSON) (exemplos):
  {
    "task": "Comprar leite e pao",
    "check": true
  }
- Response 200: retorna a tarefa atualizada.
- Erros comuns:
  - 400 { "error": "Tarefa nao existe." }

7) DELETE /tasks/:task_id
- Descricao: remove uma tarefa por id.
- Protegido: sim
- Header:
  Authorization: Bearer <token>
- Params:
  - task_id (numero)
- Response 200: sem corpo.
- Erros comuns:
  - 400 { "error": "Tarefa nao existe." }
  - 401 { "error": "Requisicao nao autorizada." }

Configuracao
- Banco de dados em src/config/database.js
- Chave JWT em src/config/auth.js

Execucao
- Iniciar servidor: yarn dev
