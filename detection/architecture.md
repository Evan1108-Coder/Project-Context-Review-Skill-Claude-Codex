# Architecture Detection Rules

How to identify the project's architectural pattern from its directory structure and file organization.

## Architecture Classification

### Step 1: Check Project Scale

| Signal | Classification |
|---|---|
| `packages/` or `apps/` at root with multiple package.json | Monorepo |
| Single `src/` with one entry point | Monolith |
| Multiple independent service directories | Multi-service |
| `serverless.yml` with functions | Serverless/FaaS |
| Single file or very few files | Script/utility |

### Step 2: Identify Organization Pattern

**Feature-based (most modern projects):**
```
src/
  features/
    auth/
      components/
      hooks/
      api.ts
      types.ts
    dashboard/
      ...
```
Signal: Top-level directories named after business concepts.

**Layer-based (traditional MVC):**
```
src/
  controllers/
  models/
  views/
  services/
  middleware/
```
Signal: Top-level directories named after technical layers.

**Domain-driven:**
```
src/
  domain/
    user/
      entity.ts
      repository.ts
      service.ts
    order/
      ...
  infrastructure/
  application/
```
Signal: `domain/`, `infrastructure/`, `application/` directories; repository pattern.

**Flat (small projects):**
```
src/
  App.tsx
  Header.tsx
  api.ts
  utils.ts
  types.ts
```
Signal: All files in one directory, no subdirectories.

**Route-based (file-system routing):**
```
app/
  page.tsx
  layout.tsx
  dashboard/
    page.tsx
  api/
    users/
      route.ts
```
Signal: Next.js App Router, Remix, SvelteKit file conventions.

### Step 3: Identify Boundaries

For each major directory, determine if it's a **hard boundary** or **soft boundary**:

**Hard boundary signals:**
- Has its own `package.json` (workspace package)
- Has a barrel file (`index.ts`) that controls exports
- Never imported by siblings (only by parent/shared)
- Has its own types that aren't shared

**Soft boundary signals:**
- No barrel file — files imported directly
- Cross-references between sibling directories
- Shared types across directories

## Monorepo Detection

| Signal | Monorepo Tool |
|---|---|
| `pnpm-workspace.yaml` | pnpm workspaces |
| `workspaces` in package.json | npm/yarn workspaces |
| `turbo.json` | Turborepo |
| `nx.json` | Nx |
| `lerna.json` | Lerna |
| `rush.json` | Rush |
| Multiple `go.mod` files | Go multi-module |
| `Cargo.toml` with `[workspace]` | Cargo workspace |

For monorepos, identify:
- Which packages are apps vs libraries
- Shared packages (often `packages/shared`, `packages/ui`, `packages/config`)
- Internal dependency graph (read workspace package.json files)

## Full-Stack Detection

| Pattern | Architecture |
|---|---|
| `client/` + `server/` | Split full-stack |
| `frontend/` + `backend/` | Split full-stack |
| `app/` + `api/` in Next.js/Remix | Unified full-stack |
| Separate repos for FE/BE | Distributed (note this in context) |
| `src/` with both React + Express | Monolith full-stack |

## State Management Detection (Frontend)

| Signal | Approach |
|---|---|
| `store/` or `stores/` directory | Centralized state |
| `zustand` in deps | Zustand stores |
| `@reduxjs/toolkit` in deps | Redux Toolkit |
| `pinia` in deps | Pinia (Vue) |
| `jotai` or `recoil` in deps | Atomic state |
| `@tanstack/react-query` in deps | Server state (cache-first) |
| Only React Context usage | Context-based (check for providers) |
| `signals` in deps | Signal-based reactivity |

## API Architecture Detection

| Signal | Pattern |
|---|---|
| `routes/` with HTTP method handlers | REST API |
| `.graphql` files or `typeDefs` | GraphQL |
| `trpc` in deps or `router.ts` with procedures | tRPC |
| `grpc` or `.proto` files | gRPC |
| WebSocket setup (`ws`, `socket.io`) | Real-time/WebSocket |
| `app/api/` in Next.js | API routes (serverless-style) |
| OpenAPI spec file | Contract-first REST |

## Output

After detection, summarize as:

```markdown
### Architecture
- Pattern: [feature-based / layer-based / domain-driven / flat / route-based]
- Scale: [monolith / monorepo / multi-service / serverless]
- Boundaries: [hard (barrel files) / soft (direct imports) / mixed]
- Full-stack: [unified / split / frontend-only / backend-only]
- State: [approach if frontend]
- API: [REST / GraphQL / tRPC / mixed]
```
