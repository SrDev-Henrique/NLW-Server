# NLW Agents - Sistema de IA com Transcrição e Q&A

Projeto desenvolvido durante o evento **NLW (Next Level Week)** da RocketSeat, focado em criar uma API inteligente para gerenciamento de salas virtuais com capacidades de IA, transcrição de áudio e sistema de perguntas e respostas baseado em contexto.

## 🚀 Tecnologias

- **Node.js** - Runtime JavaScript
- **TypeScript** - Linguagem de programação
- **Fastify** - Framework web para Node.js
- **Drizzle ORM** - ORM TypeScript-first para banco de dados
- **PostgreSQL** - Banco de dados relacional
- **pgvector** - Extensão PostgreSQL para vetores/embeddings
- **Google Gemini AI** - API de IA para transcrição e geração de respostas
- **Zod** - Validação de schemas
- **Docker** - Containerização do banco de dados
- **Biome** - Linter e formatter

## 🎯 Funcionalidades

### ✨ Principais Recursos

- **Criação de Salas Virtuais** - Organize conteúdo em salas temáticas
- **Upload e Transcrição de Áudio** - Converta áudio em texto usando IA
- **Sistema de Embeddings** - Armazene representações vetoriais do conteúdo
- **Perguntas e Respostas Inteligentes** - Faça perguntas e receba respostas baseadas no contexto
- **Busca Semântica** - Encontre conteúdo relevante usando similaridade de vetores
- **API RESTful** - Endpoints bem estruturados com validação

### 🧠 Capacidades de IA

- **Transcrição Automática** - Converte áudio para texto em português
- **Geração de Embeddings** - Cria representações vetoriais para busca semântica
- **Respostas Contextuais** - Gera respostas baseadas no conteúdo das salas
- **Busca Inteligente** - Encontra trechos relevantes usando similaridade de vetores

## 📋 Pré-requisitos

- Node.js 18+
- Docker e Docker Compose
- npm ou yarn
- Chave de API do Google Gemini

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
GEMINI_API_KEY=sua_chave_api_gemini_aqui
```

4. **Inicie o banco de dados**

```bash
docker-compose up -d
```

5. **Execute as migrações**

```bash
npm run db:migrate
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
│   ├── connection.ts      # Conexão com banco PostgreSQL
│   ├── migrations/        # Migrações do Drizzle
│   ├── schema/           # Schemas das tabelas
│   │   ├── rooms.ts      # Tabela de salas
│   │   ├── audio-chunks.ts # Tabela de chunks de áudio
│   │   ├── questions.ts  # Tabela de perguntas
│   │   └── index.ts      # Exportação dos schemas
│   └── seed.ts           # Dados iniciais
├── http/
│   └── routes/           # Rotas da API
│       ├── create-room.ts # Criação de salas
│       ├── get-rooms.ts  # Listagem de salas
│       ├── upload-audio.ts # Upload e transcrição
│       ├── create-questions.ts # Sistema de Q&A
│       └── get-questions.ts # Listagem de perguntas
├── services/
│   └── gemini.ts         # Integração com Google Gemini AI
├── env.ts               # Configuração de variáveis
└── server.ts            # Servidor Fastify
```

## 🔧 Scripts Disponíveis

- `npm run dev` - Executa em modo desenvolvimento com hot reload
- `npm start` - Executa em modo produção
- `npm run db:generate` - Gera novas migrações
- `npm run db:migrate` - Executa migrações do banco
- `npm run db:seed` - Popula o banco com dados iniciais

## 📝 Endpoints da API

### 🏠 Gerenciamento de Salas

- `GET /rooms` - Lista todas as salas/agentes
- `POST /rooms` - Cria uma nova sala

### 🎵 Upload e Transcrição de Áudio

- `POST /rooms/:roomId/audio` - Faz upload de áudio e transcreve automaticamente

### ❓ Sistema de Perguntas e Respostas

- `POST /rooms/:roomId/questions` - Cria uma pergunta e gera resposta baseada no contexto
- `GET /rooms/:roomId/questions` - Lista todas as perguntas de uma sala

### 🔍 Health Check

- `GET /health` - Verifica o status da API

## 🗄️ Modelo de Dados

### Rooms (Salas)

- `id` - UUID único
- `name` - Nome da sala
- `description` - Descrição da sala
- `createdAt` - Data de criação

### AudioChunks (Chunks de Áudio)

- `id` - UUID único
- `roomId` - Referência à sala
- `transcription` - Texto transcrito do áudio
- `embeddings` - Vetor de 768 dimensões para busca semântica
- `createdAt` - Data de criação

### Questions (Perguntas)

- `id` - UUID único
- `roomId` - Referência à sala
- `question` - Pergunta do usuário
- `answer` - Resposta gerada pela IA (pode ser null)
- `createdAt` - Data de criação

## 🧠 Como Funciona a IA

### 1. Transcrição de Áudio

- Upload de arquivo de áudio
- Conversão para base64
- Envio para Google Gemini AI
- Transcrição para português brasileiro
- Armazenamento no banco

### 2. Geração de Embeddings

- Texto transcrito é convertido em vetor de 768 dimensões
- Armazenado usando extensão pgvector do PostgreSQL
- Permite busca por similaridade semântica

### 3. Sistema de Q&A

- Pergunta é convertida em embeddings
- Busca por chunks similares (similaridade > 0.7)
- Seleção dos 3 chunks mais relevantes
- Geração de resposta baseada no contexto
- Armazenamento da pergunta e resposta

## 🛠️ Padrões Utilizados

- **TypeScript-first** - Desenvolvimento com tipagem forte
- **Schema validation** - Validação de dados com Zod
- **ORM moderno** - Drizzle ORM para operações de banco
- **Containerização** - Docker para ambiente de desenvolvimento
- **Modularização** - Estrutura organizada por responsabilidades
- **AI Integration** - Integração com APIs de IA para funcionalidades avançadas
- **Vector Search** - Busca semântica usando embeddings

## 🔒 Variáveis de Ambiente

| Variável         | Descrição                  | Obrigatória        |
| ---------------- | -------------------------- | ------------------ |
| `PORT`           | Porta do servidor          | Não (padrão: 3333) |
| `DATABASE_URL`   | URL de conexão PostgreSQL  | Sim                |
| `GEMINI_API_KEY` | Chave da API Google Gemini | Sim                |

## 🐳 Docker

O projeto utiliza Docker para o banco de dados PostgreSQL com extensão pgvector:

```yaml
services:
  nlw-agents-pg:
    image: pgvector/pgvector:pg17
    environment:
      POSTGRES_USER: docker
      POSTGRES_PASSWORD: docker
      POSTGRES_DB: agents
    ports:
      - "5432:5432"
```

## 📚 Dependências Principais

### Runtime

- `fastify` - Framework web
- `@fastify/cors` - CORS para Fastify
- `@fastify/multipart` - Upload de arquivos
- `drizzle-orm` - ORM TypeScript
- `postgres` - Driver PostgreSQL
- `@google/genai` - SDK Google Gemini AI
- `zod` - Validação de schemas

### Desenvolvimento

- `typescript` - Compilador TypeScript
- `@biomejs/biome` - Linter e formatter
- `drizzle-kit` - CLI do Drizzle ORM

## 🚀 Próximos Passos

- [ ] Implementar autenticação de usuários
- [ ] Adicionar cache para melhorar performance
- [ ] Implementar rate limiting
- [ ] Adicionar logs estruturados
- [ ] Implementar testes automatizados
- [ ] Adicionar documentação da API (Swagger/OpenAPI)
- [ ] Implementar streaming de respostas
- [ ] Adicionar suporte a múltiplos idiomas

## 📄 Licença

Este projeto foi desenvolvido durante o NLW da RocketSeat. Sinta-se livre para usar e modificar conforme necessário.
