# Let Me Ask - NLW 20

Este projeto foi desenvolvido durante a **NLW 20** da Rocketseat. Ele consiste em um agente (agent) que tem como principal objetivo responder dúvidas enviadas durante uma live stream, facilitando a interação entre audiência e apresentador.

## ✨ Descrição

O Let Me Ask é uma API backend que gerencia salas de perguntas, permitindo que usuários enviem dúvidas em tempo real para serem respondidas durante transmissões ao vivo. O foco está em fornecer uma experiência fluida para lives, centralizando e organizando as perguntas recebidas.

## 🚀 Tecnologias Utilizadas

- **Node.js** — Ambiente de execução JavaScript
- **TypeScript** — Tipagem estática para JavaScript
- **Fastify** — Framework web para Node.js, focado em performance
- **Zod** — Validação de esquemas e tipos
- **Drizzle ORM** — ORM para integração com banco de dados relacional
- **PostgreSQL** — Banco de dados relacional (com extensão [pgvector](https://github.com/pgvector/pgvector))
- **Docker** — Containerização do ambiente de banco de dados
- **Biome** — Linter e formatter para o código

## 📦 Estrutura do Projeto

- `src/server.ts` — Inicialização do servidor Fastify
- `src/http/routes/` — Rotas HTTP da API
- `src/db/` — Conexão, schema e seed do banco de dados
- `docker/` — Scripts de setup do banco
- `docker-compose.yml` — Orquestração do banco de dados

## 🛠️ Setup do Projeto

### Pré-requisitos

- Node.js (v18+)
- Docker e Docker Compose (para o banco de dados)
- pnpm, npm ou yarn

### Passos para rodar localmente

1. **Clone o repositório:**
   ```bash
   git clone https://github.com/seu-usuario/let-me-ask.git
   cd let-me-ask/server
   ```

2. **Instale as dependências:**
   ```bash
   npm install
   # ou
   yarn
   # ou
   pnpm install
   ```

3. **Suba o banco de dados com Docker:**
   ```bash
   docker-compose up -d
   ```
   O banco ficará disponível em `localhost:5433` com:
   - **Usuário:** docker
   - **Senha:** docker
   - **Database:** agents
   - **Extensão:** pgvector (instalada automaticamente)

4. **Configure as variáveis de ambiente:**
   - Crie um arquivo `.env` na raiz do projeto com o seguinte conteúdo:
     ```env
     DATABASE_URL=postgresql://docker:docker@localhost:5433/agents
     PORT=3333
     ```

5. **Rode as migrations e seeds:**
   ```bash
   npm run db:seed
   ```
   Isso irá criar as tabelas e popular a tabela `rooms` com dados fictícios.

6. **Inicie o servidor em modo desenvolvimento:**
   ```bash
   npm run dev
   ```

7. **Acesse a rota de health check:**
   - [http://localhost:3333/health](http://localhost:3333/health)

8. **Listar salas disponíveis:**
   - [http://localhost:3333/rooms](http://localhost:3333/rooms)

## 📚 Funcionalidades

- Cadastro e listagem de salas de perguntas
- Organização das perguntas por ordem de criação
- API pronta para integração com frontend de lives

## ⚙️ Variáveis de Ambiente

- `DATABASE_URL` — URL de conexão com o banco PostgreSQL (exemplo: `postgresql://docker:docker@localhost:5433/agents`)
- `PORT` — Porta onde o servidor irá rodar (padrão: 3333)

## 🗄️ Banco de Dados

- **Tabela principal:** `rooms`
  - `id` (UUID, PK)
  - `name` (texto, obrigatório)
  - `description` (texto, opcional)
  - `created_at` (timestamp, default: now)
- **Extensão:** [pgvector](https://github.com/pgvector/pgvector) já instalada via Docker

## 🧑‍💻 Dicas para Desenvolvimento

- Use o comando `npm run dev` para hot reload.
- Use o comando `npm run db:seed` para resetar e popular o banco com dados de teste.
- O projeto utiliza o [Biome](https://biomejs.dev/) para lint e format. Recomenda-se rodar `npx biome check .` antes de commitar.
- O TypeScript está configurado para modo estrito.
- O arquivo `.env` está no `.gitignore` e não deve ser versionado.

## 📝 Licença

Este projeto está sob a licença ISC.

---

Projeto desenvolvido na trilha Node.js da NLW 20 Rocketseat.