# Code Lens — Deep Architecture & Pattern Analysis

Use this lens when the goal is understanding how to write code that fits the project. Goes deeper than the base scan into architecture decisions, module boundaries, and implementation patterns.

## What to Scan

### Module Boundaries

Read the top-level `src/` (or equivalent) directory structure. For each major directory:
- What is its responsibility? (Look at file names and exports)
- Does it import from other top-level directories? (Map dependencies)
- Does it have its own barrel file / index? (Module boundary signal)

Map the dependency direction: which modules depend on which? Flag circular dependencies.

### Entry Points & Boot Sequence

Find the main entry (`index.ts`, `main.py`, `cmd/main.go`, etc.) and trace:
1. What gets initialized first? (DB connections, config, DI container)
2. What middleware/plugins are registered?
3. What order do things boot in?

This tells you where to add new initializations.

### API Surface

For backend projects, find the route/handler registration:
- Where are routes defined? (Single file, distributed, auto-generated)
- What's the handler signature? (req/res, context-based, typed params)
- What middleware is applied per-route vs globally?
- How are request/response types defined?

For frontend projects, find the page/route structure:
- File-based routing (Next.js, Remix, SvelteKit) or config-based?
- Where do layouts live?
- How is data loaded per route?

### Data Layer

Find the database/data access pattern:
- Where are models/schemas defined?
- Is there a repository pattern, service layer, or direct ORM calls?
- How are migrations handled?
- Where are queries built?

### Error Handling Strategy

Sample 3+ files that handle errors. Identify:
- Custom error classes or error codes?
- Centralized error handler or per-route?
- How are errors surfaced to the user?
- Logging: structured (JSON) or unstructured? What library?

### Shared Utilities

Check for `utils/`, `lib/`, `shared/`, `common/`, `helpers/` directories:
- What patterns are centralized? (validation, formatting, auth checks)
- Are there project-specific abstractions you should reuse?
- Any wrappers around external libraries?

## Output Additions

Add these sections to the base context output:

```markdown
### Architecture Details
- Module dependency graph: [A → B → C, D → B]
- Entry point: [path] → boots [what] in [what order]
- API pattern: [route registration style + handler signature]

### Data Layer
- Models: [path] | ORM: [name] | Migrations: [path/tool]
- Query pattern: [repository/service/direct]

### Extension Points
- To add a new API route: [where + pattern to follow]
- To add a new feature module: [where + what to export]
- To add a new data model: [where + migration step]
```
