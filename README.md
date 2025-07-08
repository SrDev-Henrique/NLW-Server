# NLW Agents

Projeto desenvolvido durante o evento **NLW (Next Level Week)** da RocketSeat, focado em criar uma API para gerenciamento de agentes/rooms.

## 🚀 Tecnologias

- **Node.js** - Runtime JavaScript
- **TypeScript** - Linguagem de programação
- **Fastify** - Framework web para Node.js
- **Drizzle ORM** - ORM TypeScript-first para banco de dados
- **PostgreSQL** - Banco de dados relacional
- **Zod** - Validação de schemas
- **Docker** - Containerização do banco de dados

## 📋 Pré-requisitos

- Node.js 18+
- Docker e Docker Compose
- npm ou yarn

## ⚙️ Configuração

1. **Clone o repositório**

```bash
git clone <url-do-repositorio>
cd server
```

2. **Instale as dependências**

```bash
npm install
```

3. **Configure as variáveis de ambiente**
   Crie um arquivo `.env` na raiz do projeto:

```env
PORT=3333
DATABASE_URL=postgresql://docker:docker@localhost:5432/agents
```

4. **Inicie o banco de dados**

```bash
docker-compose up -d
```

5. **Execute as migrações**

```bash
npx drizzle-kit migrate
```

6. **Popule o banco com dados iniciais (opcional)**

```bash
npm run db:seed
```

## 🏃‍♂️ Executando o projeto

**Desenvolvimento:**

```bash
npm run dev
```

**Produção:**

```bash
npm start
```

O servidor estará disponível em `http://localhost:3333`

## 📁 Estrutura do Projeto

```
src/
├── db/
│   ├── connection.ts      # Conexão com banco
│   ├── migrations/        # Migrações do Drizzle
│   ├── schema/           # Schemas das tabelas
│   └── seed.ts           # Dados iniciais
├── http/
│   └── routes/           # Rotas da API
├── env.ts               # Configuração de variáveis
└── server.ts            # Servidor Fastify
```

## 🔧 Scripts Disponíveis

- `npm run dev` - Executa em modo desenvolvimento com hot reload
- `npm start` - Executa em modo produção
- `npm run db:seed` - Popula o banco com dados iniciais

## 📝 Endpoints

- `GET /health` - Health check da API
- `GET /rooms` - Lista todas as rooms/agentes

## 🛠️ Padrões Utilizados

- **TypeScript-first** - Desenvolvimento com tipagem forte
- **Schema validation** - Validação de dados com Zod
- **ORM moderno** - Drizzle ORM para operações de banco
- **Containerização** - Docker para ambiente de desenvolvimento
- **Modularização** - Estrutura organizada por responsabilidades
