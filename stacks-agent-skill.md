---
name: fullstack-stacks
description: Opinionated stack selector for Next.js, Astro, Node.js, Python, Go, and Rust projects. Recommends modern defaults for API, logging, validation, database, auth, env, testing, linting, and formatting.
---

# Fullstack Stacks Skill

## Purpose

Use this skill when creating or reviewing projects in any of these stacks:

- Next.js
- Astro
- Node.js
- Python
- Go
- Rust

The goal is to choose a **small, production-credible, low-friction stack** with good developer experience and predictable maintenance.

## Global rules

- Prefer **boring, well-supported defaults** over novelty.
- Prefer **one strong package per concern**.
- Keep the initial stack minimal. Add packages only when there is a clear use case.
- Choose **TypeScript** for Next.js, Astro, and most Node.js apps.
- For Python, prefer **FastAPI + Pydantic v2 + pytest + Ruff**.
- For Go, prefer the standard library first, then add small focused libraries.
- For Rust, prefer **axum + serde + tracing + sqlx** for APIs.
- For database-backed web apps, default to **PostgreSQL**.
- For validation, prefer **schema-first request validation**.
- For logging, prefer **structured logs** in JSON in production.
- For auth, use framework-native/session-friendly solutions for web apps and JWT/OAuth only when actually needed.
- Default to OpenAPI/Swagger support for API-first backends.

## Decision guide

### If the project is:
- **Interactive web app / SaaS / dashboard** → use **Next.js**
- **Content-heavy site / docs / marketing / hybrid static site** → use **Astro**
- **Backend API in TypeScript** → use **Node.js**
- **Backend API with fast iteration and strong typing** → use **Python**
- **High-throughput backend / simple deployable service** → use **Go**
- **High-performance backend with strong correctness guarantees** → use **Rust**

---

# 1) Next.js stack

## Use when
- Building a full web app with auth, dashboards, forms, and server rendering
- You want React + App Router + server actions/routes

## Base stack
- Language: **TypeScript**
- Package manager: **pnpm**
- Framework: **Next.js**
- Styling: **Tailwind CSS**
- Testing: **Vitest**, **Testing Library**, **Playwright**
- Linting: **ESLint**
- Formatting: **Prettier**

## Recommended packages

### API
- Built-in **Route Handlers**
- `zod`
- `@t3-oss/env-nextjs`

### Database
- **Prisma** for easiest team onboarding and strong DX
- **Drizzle** when you want more SQL control, lighter runtime, or edge-friendlier patterns

### Auth
- Start with **Next.js auth patterns**
- Use **Better Auth** for a modern auth library when app-level auth is needed

### Logging
- `pino`
- `pino-pretty` for local development

### Validation
- `zod`
- `react-hook-form`
- `@hookform/resolvers`

### Data fetching / caching
- Built-in server fetching first
- `@tanstack/react-query` for client-heavy apps

### Error monitoring / observability
- `@sentry/nextjs`

### Quality of life
- `tsx` for small scripts
- `lint-staged`
- `husky` or `lefthook`

## Default recommendation
- **Next.js + TypeScript + Zod + Prisma + Better Auth + Pino + Vitest + Playwright**

## Notes
- Prefer **server components** and server actions where they simplify the app.
- Do not add React Query unless there is real client-side state synchronization complexity.
- Prefer Prisma for general business apps; switch to Drizzle if SQL control or leaner runtime matters.

---

# 2) Astro stack

## Use when
- Building content sites, docs, blogs, landing pages, or mixed static/dynamic sites
- You want minimal client JavaScript by default

## Base stack
- Language: **TypeScript**
- Package manager: **pnpm**
- Framework: **Astro**
- Testing: **Vitest**, **Playwright**
- Linting: **Biome** or **ESLint**
- Formatting: **Biome** or **Prettier**

## Recommended packages

### API
- Astro endpoints / server actions where appropriate
- `zod`

### Database
- **Astro DB** for Astro-native/simple setups
- **Drizzle** for SQL-first external DB workflows
- **Prisma** only if the team already standardizes on it

### Auth
- Session/cookie-based auth with your adapter/runtime
- Add dedicated auth only when the site has real user accounts

### Logging
- `pino` for server-side logging

### Validation
- `zod`

### Content
- Astro content collections
- `@astrojs/sitemap`
- `@astrojs/mdx`

### Quality of life
- `biome` if you want one tool for lint + format
- `eslint` + `prettier` if your team already standardizes on that combo

## Default recommendation
- **Astro + TypeScript + Zod + Astro DB or Drizzle + Pino + Vitest + Playwright + Biome**

## Notes
- Prefer Astro when content is primary and interactivity is secondary.
- Only hydrate islands that truly need client JavaScript.

---

# 3) Node.js stack

## Use when
- Building REST APIs, internal services, workers, or TypeScript backends
- You do not need a frontend framework in the same app

## Base stack
- Language: **TypeScript**
- Runtime: **Node.js**
- Package manager: **pnpm**
- Testing: **Node test runner** or **Vitest**
- Linting: **ESLint**
- Formatting: **Prettier**

## Recommended packages

### API
- **Fastify** as the default API framework
- `@fastify/sensible`
- `@fastify/cors`
- `@fastify/helmet`
- `@fastify/rate-limit`
- `@fastify/swagger`
- `@fastify/swagger-ui`

### Logging
- `pino`

### Validation
- `zod`
- `fastify-type-provider-zod` if using Zod-driven Fastify typing

### Database
- **Prisma** for easiest team onboarding
- **Drizzle** for more SQL-centric control
- `pg` for PostgreSQL driver

### Auth
- `jose` for JWT/OAuth token work
- `bcrypt` or `argon2` for passwords
- Prefer session/cookie auth unless pure API token auth is required

### Config
- `envalid` or `zod`-based env parsing
- `dotenv` only if needed outside framework support

### Background jobs / queues
- `bullmq` with Redis

### HTTP client
- Native `fetch`
- `undici` when lower-level control is needed

### Quality of life
- `tsx`
- `lint-staged`
- `husky` or `lefthook`

## Default recommendation
- **Node.js + TypeScript + Fastify + Zod + Pino + Prisma + Vitest**

## Notes
- Prefer Fastify over Express for new projects unless ecosystem constraints require Express.
- Use the built-in Node test runner for very small services; use Vitest for richer DX.

---

# 4) Python stack

## Use when
- Building APIs quickly with strong validation and fast iteration
- You want high productivity and clean typing

## Base stack
- Language: **Python 3.12+**
- Project manager: **uv**
- Framework: **FastAPI**
- Testing: **pytest**
- Linting: **Ruff**
- Formatting: **Ruff format**

## Recommended packages

### API
- `fastapi`
- `uvicorn`
- `pydantic`
- `pydantic-settings`

### Logging
- `structlog` or standard `logging`
- Prefer JSON structured logs in production

### Validation
- **Pydantic v2** for request/response/domain validation

### Database
- `sqlmodel` for FastAPI-friendly apps
- `sqlalchemy` when you need fuller ORM control
- `alembic` for migrations
- `psycopg` for PostgreSQL

### Auth
- `pyjwt` or `python-jose` for JWT use cases
- `passlib` or `pwdlib` for password hashing
- OAuth helpers only when required

### HTTP client
- `httpx`

### Background jobs
- `celery` for mature distributed jobs
- `arq` for smaller Redis-backed async jobs

### Quality of life
- `pytest-asyncio`
- `coverage`
- `pre-commit`

## Default recommendation
- **Python + uv + FastAPI + Pydantic Settings + SQLModel + Alembic + structlog + pytest + Ruff**

## Notes
- Prefer Pydantic v2-first libraries.
- Keep app settings typed and centralized.
- Use SQLModel for typical CRUD-heavy business APIs; use raw SQLAlchemy for more advanced patterns.

---

# 5) Go stack

## Use when
- Building reliable APIs and services with minimal dependencies
- You want easy deployment, speed, and strong concurrency support

## Base stack
- Language: **Go**
- Testing: **go test**
- Linting: **golangci-lint**
- Formatting: **gofmt**

## Recommended packages

### API
- Standard `net/http` first
- `chi` as the default router if you want a lightweight router
- `oapi-codegen` if working from an OpenAPI-first workflow

### Logging
- Standard library **`log/slog`** by default
- `zap` when ultra-high throughput structured logging is needed

### Validation
- `go-playground/validator/v10`

### Database
- `pgx` for PostgreSQL driver
- `sqlc` for typed SQL queries
- `gorm` only when a full ORM is explicitly wanted

### Auth
- `golang-jwt/jwt`
- `oauth2` packages as needed

### Config
- `caarlos0/env` or `envconfig`

### Docs
- `swaggo/swag` or OpenAPI-first tooling

### Background jobs
- Keep simple jobs in-process first
- Add Redis/queue tooling only if operationally necessary

## Default recommendation
- **Go + chi + slog + validator + pgx + sqlc + go test + golangci-lint**

## Notes
- Prefer stdlib plus a few sharp libraries.
- Prefer `sqlc` over heavy ORM usage for long-lived Go backends.
- Treat `gofmt` as non-optional.

---

# 6) Rust stack

## Use when
- Building APIs or services where correctness, performance, and explicitness matter
- You are comfortable with a steeper learning curve

## Base stack
- Language: **Rust**
- Async runtime: **tokio**
- Framework: **axum**
- Testing: **cargo test**
- Linting: **clippy**
- Formatting: **rustfmt**

## Recommended packages

### API
- `axum`
- `tower-http`

### Logging / tracing
- `tracing`
- `tracing-subscriber`

### Validation / serialization
- `serde`
- `serde_json`
- `validator` if field validation is needed

### Database
- `sqlx` as the default database toolkit
- `sea-orm` only if a full ORM is preferred

### Auth
- `jsonwebtoken`
- `argon2`

### Config
- `config` or `figment`
- `dotenvy` for local env loading

### Docs
- `utoipa`

### Error handling
- `thiserror`
- `anyhow` for app/service-level error ergonomics

## Default recommendation
- **Rust + axum + tokio + tracing + serde + sqlx + utoipa + cargo test + clippy + rustfmt**

## Notes
- Prefer `sqlx` for explicit, production-friendly database access.
- Use `thiserror` for typed domain errors and `anyhow` sparingly at app boundaries.

---

# Package selection rules by concern

## API framework
- Next.js: built-in route handlers
- Astro: built-in endpoints
- Node.js: Fastify
- Python: FastAPI
- Go: net/http or chi
- Rust: axum

## Logger
- TS/Node/web server: Pino
- Python: structlog
- Go: slog
- Rust: tracing

## Validation
- TS: Zod
- Python: Pydantic
- Go: validator
- Rust: validator + serde

## Database
- TS apps: Prisma by default, Drizzle when SQL control/runtime size matters
- Python: SQLModel or SQLAlchemy
- Go: pgx + sqlc
- Rust: sqlx

## Auth
- Web apps: session/cookie-first
- APIs: JWT only if clients truly need token auth
- Passwords: use strong password hashing libraries, never plain hashes

## Env/config
- Always parse and validate env vars at startup
- Never read raw env vars all over the codebase

---

# Minimal starter presets

## Next.js preset
- next
- react
- typescript
- zod
- prisma
- better-auth
- pino
- vitest
- @testing-library/react
- playwright
- eslint
- prettier

## Astro preset
- astro
- typescript
- zod
- astro-db or drizzle-orm
- pino
- vitest
- playwright
- biome

## Node.js preset
- typescript
- fastify
- zod
- pino
- prisma
- vitest
- eslint
- prettier

## Python preset
- fastapi
- uvicorn
- pydantic
- pydantic-settings
- sqlmodel
- alembic
- structlog
- pytest
- ruff

## Go preset
- chi
- slog
- validator
- pgx
- sqlc
- golangci-lint

## Rust preset
- axum
- tokio
- tracing
- tracing-subscriber
- serde
- sqlx
- utoipa
- thiserror
- anyhow

---

# What to avoid

- Do not add both Prisma and Drizzle unless there is a migration or mixed strategy reason.
- Do not add Redux, React Query, and Zustand by default to every frontend app.
- Do not use JWT auth for a normal server-rendered web app unless there is a real multi-client/API need.
- Do not add a heavy ORM in Go unless the team explicitly wants it.
- Do not over-engineer background jobs on day one.
- Do not use untyped env access.
- Do not introduce multiple logging systems.

---

# Output style when using this skill

When recommending a stack:
1. State the chosen stack.
2. List the core packages by concern:
   - api
   - logger
   - validation
   - database
   - auth
   - config/env
   - testing
   - linting
   - formatting
3. Add 1 short sentence explaining why each package was chosen.
4. Keep the initial recommendation lean.
5. Mention alternatives only when they are genuinely relevant.
