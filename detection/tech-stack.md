# Tech Stack Detection Rules

Concrete file patterns that identify the project's technology stack. Check these in order — first match wins for each category.

## Language

| Signal File | Language |
|---|---|
| `tsconfig.json` or `*.ts` in src | TypeScript |
| `package.json` (no tsconfig) | JavaScript |
| `go.mod` | Go |
| `Cargo.toml` | Rust |
| `pyproject.toml` / `setup.py` / `requirements.txt` | Python |
| `Gemfile` | Ruby |
| `pom.xml` / `build.gradle` | Java/Kotlin |
| `*.swift` / `Package.swift` | Swift |
| `mix.exs` | Elixir |
| `composer.json` | PHP |

## Framework

| Signal | Framework |
|---|---|
| `next.config.*` | Next.js |
| `nuxt.config.*` | Nuxt |
| `svelte.config.*` | SvelteKit |
| `remix.config.*` or `app/root.tsx` with `@remix-run` | Remix |
| `astro.config.*` | Astro |
| `angular.json` | Angular |
| `vite.config.*` + `src/App.vue` | Vue (Vite) |
| `vite.config.*` + `src/App.tsx` | React (Vite) |
| `create-react-app` in package.json scripts | Create React App |
| `nest-cli.json` or `@nestjs/core` in deps | NestJS |
| `express` in deps + no framework config | Express |
| `fastify` in deps | Fastify |
| `hono` in deps | Hono |
| `django` in requirements/pyproject | Django |
| `flask` in requirements/pyproject | Flask |
| `fastapi` in requirements/pyproject | FastAPI |
| `gin-gonic/gin` in go.mod | Gin (Go) |
| `fiber` in go.mod | Fiber (Go) |
| `actix-web` in Cargo.toml | Actix (Rust) |
| `axum` in Cargo.toml | Axum (Rust) |
| `rails` in Gemfile | Ruby on Rails |
| `laravel` in composer.json | Laravel |

## Runtime

| Signal | Runtime |
|---|---|
| `bun.lockb` or `bunfig.toml` | Bun |
| `deno.json` or `deno.lock` | Deno |
| `package.json` (default) | Node.js |
| `.python-version` / `pyproject.toml` | CPython |
| `go.mod` | Go runtime |
| `Cargo.toml` | Rust/cargo |

## Package Manager

| Signal File | Manager |
|---|---|
| `pnpm-lock.yaml` | pnpm |
| `yarn.lock` | Yarn |
| `bun.lockb` | Bun |
| `package-lock.json` | npm |
| `poetry.lock` | Poetry |
| `uv.lock` | uv |
| `Pipfile.lock` | Pipenv |
| `go.sum` | Go modules |
| `Cargo.lock` | Cargo |
| `Gemfile.lock` | Bundler |

## Build Tool

| Signal | Tool |
|---|---|
| `vite.config.*` | Vite |
| `webpack.config.*` | Webpack |
| `turbo.json` | Turborepo |
| `nx.json` | Nx |
| `esbuild` in scripts or deps | esbuild |
| `tsup.config.*` | tsup |
| `rollup.config.*` | Rollup |
| `Makefile` (non-JS) | Make |
| `justfile` | Just |
| `Taskfile.yml` | Task |

## Database

| Signal | Database |
|---|---|
| `prisma/schema.prisma` | Prisma (+ check datasource for DB type) |
| `drizzle.config.*` | Drizzle ORM |
| `src/db/schema.*` with drizzle imports | Drizzle ORM |
| `typeorm` in deps | TypeORM |
| `sequelize` in deps | Sequelize |
| `knex` in deps | Knex.js |
| `sqlalchemy` in requirements | SQLAlchemy |
| `django.db` imports | Django ORM |
| `gorm.io/gorm` in go.mod | GORM |
| `diesel` in Cargo.toml | Diesel |
| `alembic/` or `alembic.ini` | Alembic migrations |
| `migrations/` with numbered SQL files | Raw SQL migrations |
| `supabase/` directory | Supabase |
| `firebase` in deps | Firebase |
| `mongodb` or `mongoose` in deps | MongoDB |
| `redis` or `ioredis` in deps | Redis |

## Deployment Target

| Signal | Target |
|---|---|
| `vercel.json` or `.vercel/` | Vercel |
| `netlify.toml` | Netlify |
| `fly.toml` | Fly.io |
| `railway.json` or `railway.toml` | Railway |
| `render.yaml` | Render |
| `Dockerfile` | Container-based |
| `serverless.yml` | Serverless Framework |
| `sam-template.yaml` or `template.yaml` (AWS) | AWS SAM |
| `cdk.json` | AWS CDK |
| `terraform/` or `*.tf` | Terraform |
| `pulumi.*` | Pulumi |
| `wrangler.toml` | Cloudflare Workers |
