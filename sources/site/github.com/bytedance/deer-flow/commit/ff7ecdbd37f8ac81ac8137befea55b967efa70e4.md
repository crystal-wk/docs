# Source: https://github.com/bytedance/deer-flow/commit/ff7ecdbd37f8ac81ac8137befea55b967efa70e4

### Uh oh!

There was an error while loading. [Please reload this page]().

[bytedance](https://github.com/bytedance) / **[deer-flow](https://github.com/bytedance/deer-flow)** Public

- [Notifications](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow) You must be signed in to change notification settings
- [Fork 10.9k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)
- [Star 79.8k](https://github.com/login?return_to=%2Fbytedance%2Fdeer-flow)

 ## File tree

Expand file treeCollapse file tree

TopOpen diff view settings

Filter options

- [AGENTS.md](https://github.com/bytedance/deer-flow/commit/ff7ecdbd37f8ac81ac8137befea55b967efa70e4#diff-a54ff182c7e8acf56acfd6e4b9c3ff41e2c41a31c9b211b2deb9df75d9a478f9)

- [CLAUDE.md](https://github.com/bytedance/deer-flow/commit/ff7ecdbd37f8ac81ac8137befea55b967efa70e4#diff-6ebdb617a8104a7756d0cf36578ab01103dc9f07e4dc6feb751296b9c402faf7)

- backend

 - [AGENTS.md](https://github.com/bytedance/deer-flow/commit/ff7ecdbd37f8ac81ac8137befea55b967efa70e4#diff-2c0330701aa3b374d2869cd99dc511b7220af9fb606a7981982d8ce5bc247554)

 - [CLAUDE.md](https://github.com/bytedance/deer-flow/commit/ff7ecdbd37f8ac81ac8137befea55b967efa70e4#diff-11cca2fba0e3c1246420be768e2e9018de14582c57124f428ab050106de9118e)

- frontend

 - [AGENTS.md](https://github.com/bytedance/deer-flow/commit/ff7ecdbd37f8ac81ac8137befea55b967efa70e4#diff-bd492002340e08c1a80064210146f37abfd91630027add166548233cc645f6a8)

 - [CLAUDE.md](https://github.com/bytedance/deer-flow/commit/ff7ecdbd37f8ac81ac8137befea55b967efa70e4#diff-e15e11ddea7a1bee8e30c75ad5e191005f7c811fccfc7fe5201f90bdb7b3aa12)

Expand file treeCollapse file tree

Top

Open diff view settings

Collapse file

### [`‎AGENTS.md‎`](https://github.com/bytedance/deer-flow/commit/ff7ecdbd37f8ac81ac8137befea55b967efa70e4#diff-a54ff182c7e8acf56acfd6e4b9c3ff41e2c41a31c9b211b2deb9df75d9a478f9)

Copy file name to clipboard

+123Lines changed: 123 additions & 0 deletions

- Display the source diff
- Display the rich diff

| Original file line number | Diff line number | Diff line change |
| --- | --- | --- |
| 
`   @@ -0,0 +1,123 @@   `

 |
| | `1` | `+  # AGENTS.md  ` |
| | `2` | `+  ` |
| | `3` | ``+  This file provides guidance to AI coding agents (Claude Code, Codex, and others) when working with code in this repository. It is the source of truth; the sibling `CLAUDE.md` imports it via `@AGENTS.md`.  `` |
| | `4` | `+  ` |
| | `5` | `+  It is the **monorepo orientation layer**: it maps the whole repo and points to the  ` |
| | `6` | `+  module guides that own the depth. For anything inside a module, read that module's  ` |
| | `7` | `+  guide rather than expecting full detail here:  ` |
| | `8` | `+  ` |
| | `9` | `+  - **[backend/AGENTS.md](backend/AGENTS.md)** — backend depth: harness/app split, agent &  ` |
| | `10` | `+  middleware chain, sandbox, MCP, skills, memory, IM channels, persistence/migrations,  ` |
| | `11` | `+  config system, test layout.  ` |
| | `12` | `+  - **[frontend/AGENTS.md](frontend/AGENTS.md)** — frontend depth: Next.js App Router layout,  ` |
| | `13` | `+  thread/streaming data flow, code style, commands.  ` |
| | `14` | `+  ` |
| | `15` | `+  ## What is DeerFlow  ` |
| | `16` | `+  ` |
| | `17` | `+  DeerFlow is a LangGraph-based AI super-agent system with a full-stack architecture. The  ` |
| | `18` | `+  backend runs a "super agent" with sandboxed execution, persistent memory, subagent  ` |
| | `19` | `+  delegation, and extensible tools (built-in, MCP, community), all per-thread isolated. The  ` |
| | `20` | `+  frontend is a Next.js chat UI. External IM platforms (Feishu, Slack, Telegram, Discord,  ` |
| | `21` | `+  DingTalk) bridge into the same agent through the Gateway.  ` |
| | `22` | `+  ` |
| | `23` | `+  ## Service Topology  ` |
| | `24` | `+  ` |
| | `25` | ``+  A single `make dev` / Docker stack runs four cooperating services:  `` |
| | `26` | `+  ` |
| | `27` | `+  | Service | Port | Role |  ` |
| | `28` | `+  | --------------- | ------ | ------------------------------------------------------------------- |  ` |
| | `29` | ``+  | **Nginx** | `2026` | Unified reverse-proxy entry point — open this in the browser |  `` |
| | `30` | ``+  | **Gateway API** | `8001` | FastAPI REST API + embedded LangGraph-compatible agent runtime |  `` |
| | `31` | ``+  | **Frontend** | `3000` | Next.js web interface |  `` |
| | `32` | ``+  | **Provisioner** | `8002` | Optional — only when sandbox is configured for provisioner/K8s mode |  `` |
| | `33` | `+  ` |
| | `34` | ``+  Nginx is the single public entry: it serves the frontend and proxies `/api/langgraph/*`  `` |
| | `35` | ``+  to the Gateway's LangGraph runtime, rewriting it to Gateway's native `/api/*` routes; all  `` |
| | `36` | ``+  other `/api/*` go straight to the Gateway REST routers. See  `` |
| | `37` | `+  [backend/AGENTS.md](backend/AGENTS.md) for the runtime and router detail.  ` |
| | `38` | `+  ` |
| | `39` | `+  ## Repository Map  ` |
| | `40` | `+  ` |
| | `41` | `+  ```  ` |
| | `42` | `+  deer-flow/  ` |
| | `43` | `+  ├── Makefile # Root orchestration: drives the full stack (dev/start/stop, docker, setup)  ` |
| | `44` | `+  ├── config.example.yaml # Template → copy to config.yaml (gitignored) at repo root  ` |
| | `45` | `+  ├── extensions_config.example.json # Template → copy to extensions_config.json (gitignored): MCP servers + skills  ` |
| | `46` | `+  ├── backend/ # Python backend — see backend/AGENTS.md  ` |
| | `47` | `+  │ ├── Makefile # Per-module backend commands (dev, gateway, test, lint, migrate-rev)  ` |
| | `48` | `+  │ ├── packages/harness/ # deerflow-harness package (import: deerflow.*) — agent framework  ` |
| | `49` | `+  │ └── app/ # FastAPI Gateway + IM channels (import: app.*)  ` |
| | `50` | `+  ├── frontend/ # Next.js frontend (pnpm) — see frontend/AGENTS.md  ` |
| | `51` | `+  ├── docker/ # docker-compose files, nginx config, provisioner  ` |
| | `52` | `+  ├── skills/ # Agent skills: public/ (committed), custom/ (gitignored)  ` |
| | `53` | `+  ├── contracts/ # Cross-component JSON contracts (e.g. subagent status)  ` |
| | `54` | `+  ├── scripts/ # Root orchestration scripts invoked by the Makefile (check, configure, doctor, serve, docker, deploy, setup_wizard)  ` |
| | `55` | `+  ├── tests/ # Root-level tests (currently tests/skills/ — public skill tests)  ` |
| | `56` | `+  └── docs/ # Cross-cutting docs, plans, and design notes  ` |
| | `57` | `+  ```  ` |
| | `58` | `+  ` |
| | `59` | ``+  Runtime config lives at the **repo root**: copy `config.example.yaml` → `config.yaml`  `` |
| | `60` | ``+  (main app config) and `extensions_config.example.json` → `extensions_config.json` (MCP  `` |
| | `61` | `+  servers + skills). Both real files are gitignored and may be edited at runtime via the  ` |
| | `62` | `+  Gateway API. Config schema and resolution order are documented in  ` |
| | `63` | `+  [backend/AGENTS.md](backend/AGENTS.md).  ` |
| | `64` | `+  ` |
| | `65` | `+  ## Commands: Root vs. Module  ` |
| | `66` | `+  ` |
| | `67` | ``+  **Root `make` targets drive the whole stack** (run from the repo root):  `` |
| | `68` | `+  ` |
| | `69` | `+  ```bash  ` |
| | `70` | `+  make setup # Interactive setup wizard (recommended for new users)  ` |
| | `71` | `+  make doctor # Check configuration and system requirements  ` |
| | `72` | `+  make config # Generate local config files from the examples  ` |
| | `73` | `+  make check # Check that required tools are installed  ` |
| | `74` | `+  make install # Install all dependencies (frontend + backend + pre-commit hooks)  ` |
| | `75` | `+  make dev # Start all services with hot-reload (Gateway + Frontend + Nginx)  ` |
| | `76` | `+  make start # Start all services in production mode (local, optimized)  ` |
| | `77` | `+  make stop # Stop all running services  ` |
| | `78` | `+  make up / down # Build/stop the production Docker stack (browser at localhost:2026)  ` |
| | `79` | `+  make docker-start / docker-stop / docker-logs # Docker development environment  ` |
| | `80` | `+  ```  ` |
| | `81` | `+  ` |
| | `82` | ``+  Run `make help` for the full list.  `` |
| | `83` | `+  ` |
| | `84` | `+  **Per-module commands drive a single module** (run inside that module):  ` |
| | `85` | `+  ` |
| | `86` | `+  ```bash  ` |
| | `87` | `+  # Backend (see backend/AGENTS.md for the full set)  ` |
| | `88` | `+  cd backend && make dev # Gateway API with reload (port 8001)  ` |
| | `89` | `+  cd backend && make test # Backend test suite  ` |
| | `90` | `+  cd backend && make lint # ruff check  ` |
| | `91` | `+  cd backend && make format # ruff format  ` |
| | `92` | `+  ` |
| | `93` | `+  # Frontend (see frontend/AGENTS.md for the full set)  ` |
| | `94` | `+  cd frontend && pnpm dev # Dev server with Turbopack (port 3000)  ` |
| | `95` | `+  cd frontend && pnpm check # Lint + type check (run before committing)  ` |
| | `96` | `+  cd frontend && pnpm test # Unit tests  ` |
| | `97` | `+  ```  ` |
| | `98` | `+  ` |
| | `99` | ``+  Rule of thumb: **root `make` = the full application**; **`backend/Makefile` and `frontend/`  `` |
| | `100` | ``+  (`pnpm`) = per-module work.**  `` |
| | `101` | `+  ` |
| | `102` | `+  ## Where to Go Next  ` |
| | `103` | `+  ` |
| | `104` | `+  - Backend work → **[backend/AGENTS.md](backend/AGENTS.md)**  ` |
| | `105` | `+  - Frontend work → **[frontend/AGENTS.md](frontend/AGENTS.md)**  ` |
| | `106` | `+  - Setup & install → **[Install.md](Install.md)**, **[CONTRIBUTING.md](CONTRIBUTING.md)**  ` |
| | `107` | ``+  - Project overview & usage → **[README.md](README.md)** (translations: `README_zh.md`,  `` |
| | `108` | ``+  `README_ja.md`, `README_fr.md`, `README_ru.md`)  `` |
| | `109` | `+  - Security policy → **[SECURITY.md](SECURITY.md)**  ` |
| | `110` | `+  - Changes → **[CHANGELOG.md](CHANGELOG.md)**  ` |
| | `111` | `+  ` |
| | `112` | `+  ## Cross-Cutting Conventions  ` |
| | `113` | `+  ` |
| | `114` | `+  These apply repo-wide; module guides own the module-specific detail.  ` |
| | `115` | `+  ` |
| | `116` | ``+  - **Documentation update policy** — keep docs in sync with code: update `README.md` for  `` |
| | `117` | ``+  user-facing changes and the relevant `AGENTS.md` for development/architecture changes in  `` |
| | `118` | `+  the same change set.  ` |
| | `119` | `+  - **Test-driven development** — features and bug fixes ship with tests. Backend tests live  ` |
| | `120` | ``+  in `backend/tests/` (TDD is mandatory there; see [backend/AGENTS.md](backend/AGENTS.md));  `` |
| | `121` | ``+  frontend tests live in `frontend/tests/`.  `` |
| | `122` | ``+  - **Format before pushing** — run `make format` (backend) / `pnpm check` (frontend). Backend  `` |
| | `123` | ``+  CI enforces `ruff format --check`, so formatting must be clean before a push.  `` |

Collapse file

### [`‎CLAUDE.md‎`](https://github.com/bytedance/deer-flow/commit/ff7ecdbd37f8ac81ac8137befea55b967efa70e4#diff-6ebdb617a8104a7756d0cf36578ab01103dc9f07e4dc6feb751296b9c402faf7)

Copy file name to clipboard

+5Lines changed: 5 additions & 0 deletions

- Display the source diff
- Display the rich diff

| Original file line number | Diff line number | Diff line change |
| --- | --- | --- |
| 
`   @@ -0,0 +1,5 @@   `

 |
| | `1` | `+  # CLAUDE.md  ` |
| | `2` | `+  ` |
| | `3` | `+  The repo's agent guidance lives in [AGENTS.md](AGENTS.md) so it is shared across coding agents (Claude Code, Codex, and others). Claude Code imports it below.  ` |
| | `4` | `+  ` |
| | `5` | `+  @AGENTS.md  ` |

Collapse file

### [`‎backend/AGENTS.md‎`](https://github.com/bytedance/deer-flow/commit/ff7ecdbd37f8ac81ac8137befea55b967efa70e4#diff-2c0330701aa3b374d2869cd99dc511b7220af9fb606a7981982d8ce5bc247554)

Copy file name to clipboardExpand all lines: backend/AGENTS.md

+737\-2Lines changed: 737 additions & 2 deletions

- Display the source diff
- Display the rich diff

Load diffLarge diffs are not rendered by default.

Collapse file

### [`‎backend/CLAUDE.md‎`](https://github.com/bytedance/deer-flow/commit/ff7ecdbd37f8ac81ac8137befea55b967efa70e4#diff-11cca2fba0e3c1246420be768e2e9018de14582c57124f428ab050106de9118e)

Copy file name to clipboardExpand all lines: backend/CLAUDE.md

+2\-719Lines changed: 2 additions & 719 deletions

- Display the source diff
- Display the rich diff

Load diffLarge diffs are not rendered by default.

Collapse file

### [`‎frontend/AGENTS.md‎`](https://github.com/bytedance/deer-flow/commit/ff7ecdbd37f8ac81ac8137befea55b967efa70e4#diff-bd492002340e08c1a80064210146f37abfd91630027add166548233cc645f6a8)

Copy file name to clipboard

+90\-82Lines changed: 90 additions & 82 deletions

- Display the source diff
- Display the rich diff

| Original file line number | Diff line number | Diff line change |
| --- | --- | --- |
| 
`   @@ -1,90 +1,103 @@   `

 |
| `1` | | `-  # Agents Architecture  ` |
| | `1` | `+  # AGENTS.md  ` |
| `2` | `2` | `       ` |
| `3` | | `-  ## Overview  ` |
| | `3` | ``+  This file provides guidance to AI coding agents (Claude Code, Codex, and others) when working with the DeerFlow frontend. It is the source of truth; the sibling `CLAUDE.md` imports it via `@AGENTS.md`.  `` |
| `4` | `4` | `       ` |
| `5` | | `-  DeerFlow is built on a sophisticated agent-based architecture using the [LangGraph SDK](https://github.com/langchain-ai/langgraph) to enable intelligent, stateful AI interactions. This document outlines the agent system architecture, patterns, and best practices for working with agents in the frontend application.  ` |
| | `5` | `+  ## Project Overview  ` |
| `6` | `6` | `       ` |
| `7` | | `-  ## Architecture Overview  ` |
| | `7` | `+  DeerFlow Frontend is a Next.js 16 web interface for an AI agent system. It communicates with a LangGraph-based backend to provide thread-based AI conversations with streaming responses, artifacts, and a skills/tools system.  ` |
| `8` | `8` | `       ` |
| `9` | | `-  ### Core Components  ` |
| | `9` | `+  **Stack**: Next.js 16, React 19, TypeScript 5.8, Tailwind CSS 4, pnpm 10.26.2. Requires Node.js 22+ and pnpm 10.26.2+.  ` |
| `10` | `10` | `       ` |
| `11` | | `-  ```  ` |
| `12` | | `-  ┌────────────────────────────────────────────────────────┐  ` |
| `13` | | `-  │ Frontend (Next.js) │  ` |
| `14` | | `-  ├────────────────────────────────────────────────────────┤  ` |
| `15` | | `-  │ ┌──────────────┐ ┌──────────────┐ ┌──────────┐ │  ` |
| `16` | | `-  │ │ UI Components│───▶│ Thread Hooks │───▶│ LangGraph│ │  ` |
| `17` | | `-  │ │ │ │ │ │ SDK │ │  ` |
| `18` | | `-  │ └──────────────┘ └──────────────┘ └──────────┘ │  ` |
| `19` | | `-  │ │ │ │ │  ` |
| `20` | | `-  │ │ ▼ │ │  ` |
| `21` | | `-  │ │ ┌──────────────┐ │ │  ` |
| `22` | | `-  │ └───────────▶│ Thread State │◀──────────┘ │  ` |
| `23` | | `-  │ │ Management │ │  ` |
| `24` | | `-  │ └──────────────┘ │  ` |
| `25` | | `-  └────────────────────────────────────────────────────────┘  ` |
| `26` | | `-  │  ` |
| `27` | | `-  ▼  ` |
| `28` | | `-  ┌────────────────────────────────────────────────────────┐  ` |
| `29` | | `-  │ LangGraph Backend (lead_agent) │  ` |
| `30` | | `-  │ ┌────────────┐ ┌──────────┐ ┌───────────────────┐ │  ` |
| `31` | | `-  │ │Main Agent │─▶│Sub-Agents│─▶│ Tools & Skills │ │  ` |
| `32` | | `-  │ └────────────┘ └──────────┘ └───────────────────┘ │  ` |
| `33` | | `-  └────────────────────────────────────────────────────────┘  ` |
| `34` | | `-  ```  ` |
| | `11` | `+  ### Core dependencies  ` |
| | `12` | `+  ` |
| | `13` | ``+  - **LangGraph SDK** (`@langchain/langgraph-sdk` ^1.5.3) — Agent orchestration and streaming  `` |
| | `14` | ``+  - **LangChain Core** (`@langchain/core` ^1.1.15) — Fundamental AI building blocks  `` |
| | `15` | ``+  - **TanStack Query** (`@tanstack/react-query` ^5.90.17) — Server state management  `` |
| | `16` | `+  - **UI**: Shadcn UI, MagicUI, React Bits, and Vercel AI SDK elements (generated from registries — see Code Style)  ` |
| | `17` | `+  ` |
| | `18` | `+  ## Commands  ` |
| | `19` | `+  ` |
| | `20` | `+  | Command | Purpose |  ` |
| | `21` | `+  | ---------------- | ------------------------------------------------- |  ` |
| | `22` | ``+  | `pnpm dev` | Dev server with Turbopack (http://localhost:3000) |  `` |
| | `23` | ``+  | `pnpm build` | Production build |  `` |
| | `24` | ``+  | `pnpm check` | Lint + type check (run before committing) |  `` |
| | `25` | ``+  | `pnpm lint` | ESLint only |  `` |
| | `26` | ``+  | `pnpm lint:fix` | ESLint with auto-fix |  `` |
| | `27` | ``+  | `pnpm format` | Prettier check (`pnpm format:write` to apply) |  `` |
| | `28` | ``+  | `pnpm test` | Run unit tests with Rstest |  `` |
| | `29` | ``+  | `pnpm test:e2e` | Run E2E tests with Playwright (Chromium) |  `` |
| | `30` | ``+  | `pnpm typecheck` | TypeScript type check (`tsc --noEmit`) |  `` |
| | `31` | ``+  | `pnpm start` | Start production server |  `` |
| | `32` | `+  ` |
| | `33` | ``+  Unit tests live under `tests/unit/` and mirror the `src/` layout (e.g., `tests/unit/core/api/stream-mode.test.ts` tests `src/core/api/stream-mode.ts`). Powered by Rstest; import source modules via the `@/` path alias.  `` |
| `35` | `34` | `       ` |
| `36` | | `-  ## Project Structure  ` |
| | `35` | ``+  E2E tests live under `tests/e2e/` and use Playwright with Chromium. They mock all backend APIs via `page.route()` network interception and test real page interactions (navigation, chat input, streaming responses). Config: `playwright.config.ts`.  `` |
| | `36` | `+  ` |
| | `37` | `+  ## Architecture  ` |
| `37` | `38` | `       ` |
| `38` | `39` | `   ```   ` |
| `39` | | `-  tests/  ` |
| `40` | | `-  ├── e2e/ # E2E tests (Playwright, Chromium, mocked backend)  ` |
| `41` | | `-  └── unit/ # Unit tests (mirrors src/ layout, powered by Rstest)  ` |
| `42` | | `-  src/  ` |
| `43` | | `-  ├── app/ # Next.js App Router pages  ` |
| `44` | | `-  │ ├── api/ # API routes  ` |
| `45` | | `-  │ ├── workspace/ # Main workspace pages  ` |
| `46` | | `-  │ └── mock/ # Mock/demo pages  ` |
| `47` | | `-  ├── components/ # React components  ` |
| `48` | | `-  │ ├── ui/ # Reusable UI components  ` |
| `49` | | `-  │ ├── workspace/ # Workspace-specific components  ` |
| `50` | | `-  │ ├── landing/ # Landing page components  ` |
| `51` | | `-  │ └── ai-elements/ # AI-related UI elements  ` |
| `52` | | `-  ├── core/ # Core business logic  ` |
| `53` | | `-  │ ├── api/ # API client & data fetching  ` |
| `54` | | `-  │ ├── artifacts/ # Artifact management  ` |
| `55` | | `-  │ ├── channels/ # IM channel connections (providers, connect flow)  ` |
| `56` | | `-  │ ├── config/ # App configuration  ` |
| `57` | | `-  │ ├── i18n/ # Internationalization  ` |
| `58` | | `-  │ ├── mcp/ # MCP integration  ` |
| `59` | | `-  │ ├── messages/ # Message handling  ` |
| `60` | | `-  │ ├── models/ # Data models & types  ` |
| `61` | | `-  │ ├── settings/ # User settings  ` |
| `62` | | `-  │ ├── skills/ # Skills system  ` |
| `63` | | `-  │ ├── threads/ # Thread management  ` |
| `64` | | `-  │ ├── todos/ # Todo system  ` |
| `65` | | `-  │ └── utils/ # Utility functions  ` |
| `66` | | `-  ├── hooks/ # Custom React hooks  ` |
| `67` | | `-  ├── lib/ # Shared libraries & utilities  ` |
| `68` | | `-  ├── server/ # Server-side code (Not available yet)  ` |
| `69` | | `-  │ └── better-auth/ # Authentication setup (Not available yet)  ` |
| `70` | | `-  └── styles/ # Global styles  ` |
| | `40` | `+  Frontend (Next.js) ──▶ LangGraph SDK ──▶ LangGraph Backend (lead_agent)  ` |
| | `41` | `+  ├── Sub-Agents  ` |
| | `42` | `+  └── Tools & Skills  ` |
| `71` | `43` | `   ```   ` |
| `72` | `44` | `       ` |
| `73` | | `-  ### Technology Stack  ` |
| | `45` | `+  The frontend is a stateful chat application. Users create **threads** (conversations), send messages, and receive streamed AI responses. The backend orchestrates agents that can produce **artifacts** (files/code) and **todos**.  ` |
| | `46` | `+  ` |
| | `47` | ``+  ### Source Layout (`src/`)  `` |
| | `48` | `+  ` |
| | `49` | ``+  - **`app/`** — Next.js App Router. Routes include `/` (landing), `/workspace/chats/[thread_id]` (chat), `/workspace/agents/[agent_name]` and `/workspace/agents/new` (custom agents), `/blog/…`, the `(auth)/{login,setup,auth/callback}` flow, `/[lang]/docs/…`, and `/api/…` route handlers (e.g. `/api/memory`).  `` |
| | `50` | ``+  - **`components/`** — React components:  `` |
| | `51` | ``+  - `ui/` — Shadcn UI primitives (auto-generated, ESLint-ignored)  `` |
| | `52` | ``+  - `ai-elements/` — Vercel AI SDK elements (auto-generated, ESLint-ignored)  `` |
| | `53` | ``+  - `workspace/` — Chat page components (messages, artifacts, settings)  `` |
| | `54` | ``+  - `landing/` — Landing page sections  `` |
| | `55` | ``+  - `docs/` — Docs / MDX rendering components  `` |
| | `56` | ``+  - **`core/`** — Business logic, the heart of the app. Domains include `threads/` (creation, streaming, state), `api/` (LangGraph client singleton), `agents/` (custom agents), `auth/` (authentication), `artifacts/`, `channels/` (IM connections), `i18n/` (en-US, zh-CN), `settings/`, `memory/`, `skills/`, `messages/`, `mcp/`, `models/`, `suggestions/`, `tasks/`, `todos/`, `tools/`, `config/`, `notification/`, `blog/`, plus rendering helpers (`rehype/`, `streamdown/`) and `utils/`.  `` |
| | `57` | ``+  - **`hooks/`** — Shared React hooks  `` |
| | `58` | ``+  - **`lib/`** — Utilities (`cn()` from clsx + tailwind-merge)  `` |
| | `59` | ``+  - **`content/`** — MDX content (blog posts, docs) rendered by the app  `` |
| | `60` | ``+  - **`styles/`** — Global CSS with Tailwind v4 `@import` syntax and CSS variables for theming  `` |
| | `61` | ``+  - **`typings/`** — Ambient TypeScript declarations  `` |
| | `62` | ``+  - Root files: `env.js` (env validation), `mdx-components.ts` (MDX component map)  `` |
| | `63` | `+  ` |
| | `64` | `+  ### Data Flow  ` |
| | `65` | `+  ` |
| | `66` | ``+  1. User input → thread hooks (`core/threads/hooks.ts`) → LangGraph SDK streaming  `` |
| | `67` | `+  2. Stream events update thread state (messages, artifacts, todos)  ` |
| | `68` | `+  3. TanStack Query manages server state; localStorage stores user settings  ` |
| | `69` | `+  4. Components subscribe to thread state and render updates  ` |
| `74` | `70` | `       ` |
| `75` | | ``-  - **LangGraph SDK** (`@langchain/langgraph-sdk@1.5.3`) - Agent orchestration and streaming  `` |
| `76` | | ``-  - **LangChain Core** (`@langchain/core@1.1.15`) - Fundamental AI building blocks  `` |
| `77` | | ``-  - **TanStack Query** (`@tanstack/react-query@5.90.17`) - Server state management  `` |
| `78` | | `-  - **React Hooks** - Thread lifecycle and state management  ` |
| `79` | | `-  - **Shadcn UI** - UI components  ` |
| `80` | | `-  - **MagicUI** - Magic UI components  ` |
| `81` | | `-  - **React Bits** - React bits components  ` |
| | `71` | `+  ### Key Patterns  ` |
| | `72` | `+  ` |
| | `73` | ``+  - **Server Components by default**, `"use client"` only for interactive components  `` |
| | `74` | ``+  - **Thread hooks** (`useThreadStream`, `useSubmitThread`, `useThreads`) are the primary API interface  `` |
| | `75` | ``+  - **LangGraph client** is a singleton obtained via `getAPIClient()` in `core/api/`  `` |
| | `76` | ``+  - **Environment validation** uses `@t3-oss/env-nextjs` with Zod schemas (`src/env.js`). Skip with `SKIP_ENV_VALIDATION=1`  `` |
| `82` | `77` | `       ` |
| `83` | `78` | `   ### Interaction Ownership   ` |
| `84` | `79` | `       ` |
| `85` | `80` | ``   - `src/app/workspace/chats/[thread_id]/page.tsx` owns composer busy-state wiring.   `` |
| `86` | `81` | ``   - `src/core/threads/hooks.ts` owns pre-submit upload state and thread submission.   `` |
| `87` | | ``-  - `src/hooks/usePoseStream.ts` is a passive store selector; global WebSocket lifecycle stays in `App.tsx`.  `` |
| | `82` | `+  ` |
| | `83` | `+  ## Code Style  ` |
| | `84` | `+  ` |
| | `85` | ``+  - **Imports**: Enforced ordering (builtin → external → internal → parent → sibling), alphabetized, newlines between groups. Use inline type imports: `import { type Foo }`.  `` |
| | `86` | ``+  - **Unused variables**: Prefix with `_`.  `` |
| | `87` | ``+  - **Class names**: Use `cn()` from `@/lib/utils` for conditional Tailwind classes.  `` |
| | `88` | ``+  - **Path alias**: `@/*` maps to `src/*`.  `` |
| | `89` | ``+  - **Components**: `ui/` and `ai-elements/` are generated from registries (Shadcn, MagicUI, React Bits, Vercel AI SDK) — don't manually edit these.  `` |
| | `90` | `+  ` |
| | `91` | `+  ## Environment  ` |
| | `92` | `+  ` |
| | `93` | `+  Backend API URLs are optional; an nginx proxy is used by default:  ` |
| | `94` | `+  ` |
| | `95` | `+  ```  ` |
| | `96` | `+  NEXT_PUBLIC_BACKEND_BASE_URL=http://localhost:8001  ` |
| | `97` | `+  NEXT_PUBLIC_LANGGRAPH_BASE_URL=http://localhost:8001/api  ` |
| | `98` | `+  ```  ` |
| | `99` | `+  ` |
| | `100` | ``+  Leave these unset for the standard `make dev` / Docker flow, where nginx serves the public `/api/langgraph/*` prefix and rewrites it to Gateway's native `/api/*` routes.  `` |
| `88` | `101` | `       ` |
| `89` | `102` | `   ## Resources   ` |
| `90` | `103` | `       ` |
| 

`   @@ -95,15 +108,10 @@ src/   `

 |
| `95` | `108` | `       ` |
| `96` | `109` | `   ## Contributing   ` |
| `97` | `110` | `       ` |
| `98` | | `-  When adding new agent features:  ` |
| `99` | | `-  ` |
| `100` | | `-  1. Follow the established project structure  ` |
| `101` | | `-  2. Add comprehensive TypeScript types  ` |
| `102` | | `-  3. Implement proper error handling  ` |
| `103` | | ``-  4. Write unit tests under `tests/unit/` (run with `pnpm test`) and E2E tests under `tests/e2e/` (run with `pnpm test:e2e`)  `` |
| `104` | | `-  5. Update this documentation  ` |
| `105` | | `-  6. Follow the code style guide (ESLint + Prettier)  ` |
| `106` | | `-  ` |
| `107` | | `-  ## License  ` |
| | `111` | `+  When adding features:  ` |
| `108` | `112` | `       ` |
| `109` | | `-  This agent architecture is part of the DeerFlow project.  ` |
| | `113` | ``+  1. Follow the established `src/` structure  `` |
| | `114` | `+  2. Add TypeScript types and proper error handling  ` |
| | `115` | ``+  3. Write unit tests under `tests/unit/` (`pnpm test`) and E2E tests under `tests/e2e/` (`pnpm test:e2e`)  `` |
| | `116` | ``+  4. Run `pnpm check` before committing  `` |
| | `117` | ``+  5. Update this `AGENTS.md` when architecture, commands, or conventions change  `` |

Collapse file

### [`‎frontend/CLAUDE.md‎`](https://github.com/bytedance/deer-flow/commit/ff7ecdbd37f8ac81ac8137befea55b967efa70e4#diff-e15e11ddea7a1bee8e30c75ad5e191005f7c811fccfc7fe5201f90bdb7b3aa12)

Copy file name to clipboard

+2\-96Lines changed: 2 additions & 96 deletions

- Display the source diff
- Display the rich diff

| Original file line number | Diff line number | Diff line change |
| --- | --- | --- |
| 
`   @@ -1,99 +1,5 @@   `

 |
| `1` | `1` | `   # CLAUDE.md   ` |
| `2` | `2` | `       ` |
| `3` | | `-  This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.  ` |
| | `3` | `+  The frontend agent guidance lives in [AGENTS.md](AGENTS.md) so it is shared across coding agents (Claude Code, Codex, and others). Claude Code imports it below.  ` |
| `4` | `4` | `       ` |
| `5` | | `-  ## Project Overview  ` |
| `6` | | `-  ` |
| `7` | | `-  DeerFlow Frontend is a Next.js 16 web interface for an AI agent system. It communicates with a LangGraph-based backend to provide thread-based AI conversations with streaming responses, artifacts, and a skills/tools system.  ` |
| `8` | | `-  ` |
| `9` | | `-  **Stack**: Next.js 16, React 19, TypeScript 5.8, Tailwind CSS 4, pnpm 10.26.2  ` |
| `10` | | `-  ` |
| `11` | | `-  ## Commands  ` |
| `12` | | `-  ` |
| `13` | | `-  | Command | Purpose |  ` |
| `14` | | `-  | ---------------- | ------------------------------------------------- |  ` |
| `15` | | ``-  | `pnpm dev` | Dev server with Turbopack (http://localhost:3000) |  `` |
| `16` | | ``-  | `pnpm build` | Production build |  `` |
| `17` | | ``-  | `pnpm check` | Lint + type check (run before committing) |  `` |
| `18` | | ``-  | `pnpm lint` | ESLint only |  `` |
| `19` | | ``-  | `pnpm lint:fix` | ESLint with auto-fix |  `` |
| `20` | | ``-  | `pnpm test` | Run unit tests with Rstest |  `` |
| `21` | | ``-  | `pnpm test:e2e` | Run E2E tests with Playwright (Chromium) |  `` |
| `22` | | ``-  | `pnpm typecheck` | TypeScript type check (`tsc --noEmit`) |  `` |
| `23` | | ``-  | `pnpm start` | Start production server |  `` |
| `24` | | `-  ` |
| `25` | | ``-  Unit tests live under `tests/unit/` and mirror the `src/` layout (e.g., `tests/unit/core/api/stream-mode.test.ts` tests `src/core/api/stream-mode.ts`). Powered by Rstest; import source modules via the `@/` path alias.  `` |
| `26` | | `-  ` |
| `27` | | ``-  E2E tests live under `tests/e2e/` and use Playwright with Chromium. They mock all backend APIs via `page.route()` network interception and test real page interactions (navigation, chat input, streaming responses). Config: `playwright.config.ts`.  `` |
| `28` | | `-  ` |
| `29` | | `-  ## Architecture  ` |
| `30` | | `-  ` |
| `31` | | `-  ```  ` |
| `32` | | `-  Frontend (Next.js) ──▶ LangGraph SDK ──▶ LangGraph Backend (lead_agent)  ` |
| `33` | | `-  ├── Sub-Agents  ` |
| `34` | | `-  └── Tools & Skills  ` |
| `35` | | `-  ```  ` |
| `36` | | `-  ` |
| `37` | | `-  The frontend is a stateful chat application. Users create **threads** (conversations), send messages, and receive streamed AI responses. The backend orchestrates agents that can produce **artifacts** (files/code) and **todos**.  ` |
| `38` | | `-  ` |
| `39` | | ``-  ### Source Layout (`src/`)  `` |
| `40` | | `-  ` |
| `41` | | ``-  - **`app/`** — Next.js App Router. Routes: `/` (landing), `/workspace/chats/[thread_id]` (chat).  `` |
| `42` | | ``-  - **`components/`** — React components split into:  `` |
| `43` | | ``-  - `ui/` — Shadcn UI primitives (auto-generated, ESLint-ignored)  `` |
| `44` | | ``-  - `ai-elements/` — Vercel AI SDK elements (auto-generated, ESLint-ignored)  `` |
| `45` | | ``-  - `workspace/` — Chat page components (messages, artifacts, settings)  `` |
| `46` | | ``-  - `landing/` — Landing page sections  `` |
| `47` | | ``-  - **`core/`** — Business logic, the heart of the app:  `` |
| `48` | | ``-  - `threads/` — Thread creation, streaming, state management (hooks + types)  `` |
| `49` | | ``-  - `api/` — LangGraph client singleton  `` |
| `50` | | ``-  - `artifacts/` — Artifact loading and caching  `` |
| `51` | | ``-  - `channels/` — IM channel connections (provider catalog, connect/runtime-config API + hooks)  `` |
| `52` | | ``-  - `i18n/` — Internationalization (en-US, zh-CN)  `` |
| `53` | | ``-  - `settings/` — User preferences in localStorage  `` |
| `54` | | ``-  - `memory/` — Persistent user memory system  `` |
| `55` | | ``-  - `skills/` — Skills installation and management  `` |
| `56` | | ``-  - `messages/` — Message processing and transformation  `` |
| `57` | | ``-  - `mcp/` — Model Context Protocol integration  `` |
| `58` | | ``-  - `models/` — TypeScript types and data models  `` |
| `59` | | ``-  - **`hooks/`** — Shared React hooks  `` |
| `60` | | ``-  - **`lib/`** — Utilities (`cn()` from clsx + tailwind-merge)  `` |
| `61` | | ``-  - **`server/`** — Server-side code (better-auth, not yet active)  `` |
| `62` | | ``-  - **`styles/`** — Global CSS with Tailwind v4 `@import` syntax and CSS variables for theming  `` |
| `63` | | `-  ` |
| `64` | | `-  ### Data Flow  ` |
| `65` | | `-  ` |
| `66` | | ``-  1. User input → thread hooks (`core/threads/hooks.ts`) → LangGraph SDK streaming  `` |
| `67` | | `-  2. Stream events update thread state (messages, artifacts, todos)  ` |
| `68` | | `-  3. TanStack Query manages server state; localStorage stores user settings  ` |
| `69` | | `-  4. Components subscribe to thread state and render updates  ` |
| `70` | | `-  ` |
| `71` | | `-  ### Key Patterns  ` |
| `72` | | `-  ` |
| `73` | | ``-  - **Server Components by default**, `"use client"` only for interactive components  `` |
| `74` | | ``-  - **Thread hooks** (`useThreadStream`, `useSubmitThread`, `useThreads`) are the primary API interface  `` |
| `75` | | ``-  - **LangGraph client** is a singleton obtained via `getAPIClient()` in `core/api/`  `` |
| `76` | | ``-  - **Environment validation** uses `@t3-oss/env-nextjs` with Zod schemas (`src/env.js`). Skip with `SKIP_ENV_VALIDATION=1`  `` |
| `77` | | `-  ` |
| `78` | | `-  ## Code Style  ` |
| `79` | | `-  ` |
| `80` | | ``-  - **Imports**: Enforced ordering (builtin → external → internal → parent → sibling), alphabetized, newlines between groups. Use inline type imports: `import { type Foo }`.  `` |
| `81` | | ``-  - **Unused variables**: Prefix with `_`.  `` |
| `82` | | ``-  - **Class names**: Use `cn()` from `@/lib/utils` for conditional Tailwind classes.  `` |
| `83` | | ``-  - **Path alias**: `@/*` maps to `src/*`.  `` |
| `84` | | ``-  - **Components**: `ui/` and `ai-elements/` are generated from registries (Shadcn, MagicUI, React Bits, Vercel AI SDK) — don't manually edit these.  `` |
| `85` | | `-  ` |
| `86` | | `-  ## Environment  ` |
| `87` | | `-  ` |
| `88` | | `-  Backend API URLs are optional; an nginx proxy is used by default:  ` |
| `89` | | `-  ` |
| `90` | | `-  ```  ` |
| `91` | | `-  NEXT_PUBLIC_BACKEND_BASE_URL=http://localhost:8001  ` |
| `92` | | `-  NEXT_PUBLIC_LANGGRAPH_BASE_URL=http://localhost:8001/api  ` |
| `93` | | `-  ```  ` |
| `94` | | `-  ` |
| `95` | | ``-  Leave these unset for the standard `make dev` / Docker flow, where nginx serves  `` |
| `96` | | ``-  the public `/api/langgraph/*` prefix and rewrites it to Gateway's native `/api/*`  `` |
| `97` | | `-  routes.  ` |
| `98` | | `-  ` |
| `99` | | `-  Requires Node.js 22+ and pnpm 10.26.2+.  ` |
| | `5` | `+  @AGENTS.md  ` |

## 0 commit comments

Comments

0 (0)

Please [sign in](https://github.com/login?return_to=https://github.com/bytedance/deer-flow/commit/ff7ecdbd37f8ac81ac8137befea55b967efa70e4) to comment.