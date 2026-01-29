# Tasklist API

API REST em Node.js/Express para cadastro de usuarios, autenticacao via JWT e gerenciamento de tarefas. Projeto simples, objetivo e pronto para estudo, demonstracao e extensoes.

## Funcionalidades
- Cadastro e login de usuarios
- Autenticacao via JWT
- CRUD de tarefas por usuario
- Validacao de payloads com Yup
- ORM Sequelize com PostgreSQL

## Stack
- Node.js + Express
- PostgreSQL + Sequelize
- JWT + bcryptjs
- Yup

## Endpoints principais
- POST /users
- POST /sessions
- PUT /users
- POST /tasks
- GET /tasks
- PUT /tasks/:task_id
- DELETE /tasks/:task_id

## Fluxo de autenticacao
1) Crie usuario em /users
2) Faça login em /sessions e receba o token JWT
3) Use Authorization: Bearer <token> nas rotas protegidas

## Como rodar localmente

### 1) Instalar dependencias
```
yarn
```

### 2) Configurar banco
Edite `src/config/database.js` com as credenciais do seu PostgreSQL.

### 3) Rodar migrations
```
yarn sequelize db:migrate
```

### 4) Iniciar servidor
```
yarn dev
```

A API vai subir em `http://localhost:3333`.

## Exemplos de uso (curl)

### Criar usuario
```
curl -X POST http://localhost:3333/users \
  -H "Content-Type: application/json" \
  -d '{"name":"Joao","email":"joao@email.com","password":"123456"}'
```

### Login
```
curl -X POST http://localhost:3333/sessions \
  -H "Content-Type: application/json" \
  -d '{"email":"joao@email.com","password":"123456"}'
```

### Criar tarefa (com token)
```
curl -X POST http://localhost:3333/tasks \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <token>" \
  -d '{"task":"Comprar leite"}'
```

## Documentacao
- `docs/API.md`: endpoints com payloads e responses
- `docs/PLUGINS.md`: dependencias com descricao e exemplos
- `docs/OVERVIEW.md`: visao geral e fluxo
- `docs/TECHNICAL.md`: documentacao tecnica

## Melhorias futuras (ideias)
- Refresh token
- Paginação e filtros de tarefas
- Rate limiting e CORS
- Variaveis de ambiente com dotenv

---

Feito para estudo e pratica com Node.js, Sequelize e APIs REST.
