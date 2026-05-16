# Docs Lens — Documentation & API Surface Analysis

Use this lens when writing documentation, understanding the project's public API, or contributing to an unfamiliar project with existing docs.

## What to Scan

### Documentation Structure

Check for documentation files and directories:
- `README.md` — Project overview, setup instructions, quick start
- `docs/` or `documentation/` — Structured docs site or markdown files
- `CONTRIBUTING.md` — How to contribute (critical for conventions)
- `CHANGELOG.md` or `HISTORY.md` — Release history and versioning approach
- `ADR/` or `decisions/` — Architecture Decision Records
- `API.md` or `api-docs/` — API documentation
- `.github/ISSUE_TEMPLATE/`, `.github/PULL_REQUEST_TEMPLATE.md` — Process templates

### API Documentation

Identify how the API is documented:
- **OpenAPI/Swagger**: `openapi.yaml`, `swagger.json`, or auto-generated from code
- **GraphQL Schema**: `.graphql` files, schema-first or code-first
- **TSDoc/JSDoc**: Inline documentation on exports
- **Separate docs**: Markdown files describing endpoints
- **Auto-generated**: Typedoc, Rustdoc, Godoc, Sphinx

### README Quality

Read the README and identify:
- Does it explain how to install and run the project?
- Does it explain the architecture or link to architecture docs?
- Does it list prerequisites?
- Is it up to date with the current code? (Check for references to files/commands that still exist)

### Internal Documentation

Look for documentation aimed at developers working IN the codebase:
- Code comments on complex logic (sample a few complex files)
- Type definitions that serve as documentation (well-named types with comments)
- Constants files with explanatory comments
- Config files with inline documentation

### Versioning & Releases

- Semantic versioning? (Check package version + CHANGELOG format)
- Release process: tags, GitHub releases, automated?
- Breaking change documentation approach

### Onboarding Gaps

Identify what's NOT documented but should be:
- Can you set up the project from README alone?
- Are environment variables documented? (`.env.example` vs just `.env` in gitignore)
- Are there undocumented prerequisites? (Check Dockerfile or CI for clues)
- Are there undocumented scripts in `package.json` or `Makefile`?

## Output Additions

```markdown
### Documentation Map
- README: [quality: good/outdated/minimal] | Setup instructions: [yes/no]
- Architecture docs: [path or "none"]
- API docs: [approach + path]
- Contributing guide: [yes/no] | ADRs: [yes/no]
- Changelog: [format + up-to-date?]

### Developer Onboarding
- Setup from README alone: [possible/missing steps]
- Env vars documented: [yes/no/partial]
- Key scripts: [list undocumented but important scripts]
- Prerequisites not in README: [list if found in CI/Docker]

### API Surface
- Public API: [REST/GraphQL/RPC] | Docs: [auto-generated/manual/none]
- Type exports: [well-typed / partial / untyped]
- Entry points for consumers: [main export paths]

### Documentation Gaps
- [specific things that should be documented but aren't]
```
