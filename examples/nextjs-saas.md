# Example Output: Next.js SaaS App

This is what the skill's output looks like for a typical Next.js full-stack SaaS application.

---

## Project Context: acme-dashboard

**Stack**: TypeScript + Next.js 14 (App Router) + Node.js
**Architecture**: Feature-based monolith (full-stack unified)
**Package Manager**: pnpm | **Build**: Next.js (Turbopack dev) | **Deploy**: Vercel

### Key Dependencies
- `next` 14.2 — Framework (App Router with server components)
- `@tanstack/react-query` — Client-side data fetching and caching
- `prisma` — ORM (PostgreSQL via Neon)
- `next-auth` — Authentication (GitHub + Google OAuth)
- `tailwindcss` — Styling
- `zod` — Schema validation (shared between client/server)
- `resend` — Transactional email

### File Structure Pattern
- Route-based organization via `app/` directory (Next.js App Router conventions)
- Shared features in `src/features/` with co-located components, hooks, and server actions
- Entry: `app/layout.tsx` | Routes: `app/(dashboard)/`, `app/(auth)/` | Components: `src/components/`

### Conventions
- Naming: files: kebab-case, functions: camelCase, components: PascalCase, types: PascalCase
- Imports: absolute with `@/` alias (maps to `src/`)
- Exports: named exports (no default except page/layout components)
- Formatting: Prettier (single quotes, no semicolons, 2-space indent, trailing commas)

### Patterns In Use
- State: React Query for server state, React Context for UI state (theme, sidebar)
- Data fetching: Server Components for initial load, React Query for client mutations
- Styling: Tailwind CSS + `cn()` utility (clsx + tailwind-merge)
- Testing: Vitest + Testing Library (co-located `*.test.tsx` files)
- Error handling: Zod validation at API boundaries, `notFound()` / `redirect()` in server components

### Important Context
- Route groups `(dashboard)` and `(auth)` share different layouts
- All server actions in `src/features/*/actions.ts` — validated with Zod schemas
- Database migrations via `prisma migrate` — schema at `prisma/schema.prisma`
- Environment: `.env.local` for dev (see `.env.example` for required vars)
- No `src/app/api/` routes — uses server actions instead of API routes
