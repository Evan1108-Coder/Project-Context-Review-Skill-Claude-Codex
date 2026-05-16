# Convention Detection Rules

How to identify naming conventions, code style, and organizational patterns by sampling actual project files.

## Sampling Strategy

Don't scan every file. Sample strategically:

1. **3 source files** from different directories (not utility files — pick feature/domain files)
2. **1 test file** (to see test conventions)
3. **1 type/interface file** (if TypeScript/typed language)
4. **Config files** (formatter/linter for authoritative style rules)

## File Naming

| Pattern | Convention | Common In |
|---|---|---|
| `UserProfile.tsx` | PascalCase | React components |
| `user-profile.ts` | kebab-case | Angular, Remix routes, utilities |
| `userProfile.ts` | camelCase | Services, hooks, utilities |
| `user_profile.py` | snake_case | Python, Ruby, Go (sometimes) |
| `user_profile_test.go` | snake_case + _test suffix | Go |
| `UserProfile.test.tsx` | PascalCase + .test | React tests |
| `user-profile.spec.ts` | kebab-case + .spec | Angular tests |

**How to detect:** List 10+ source files, identify the dominant pattern. If mixed, note which pattern applies to which file type.

## Function/Method Naming

| Pattern | Convention | Common In |
|---|---|---|
| `getUserProfile()` | camelCase | JS/TS, Java, Kotlin |
| `get_user_profile()` | snake_case | Python, Ruby, Rust, Go (exported = PascalCase) |
| `GetUserProfile()` | PascalCase | Go (exported), C# |

**How to detect:** Read function declarations in 3 sample files.

## Variable Naming

| Pattern | Convention |
|---|---|
| `const userData = ...` | camelCase (JS/TS standard) |
| `user_data = ...` | snake_case (Python/Ruby/Rust) |
| `USER_DATA = ...` | SCREAMING_SNAKE (constants/env) |

## Component Patterns (Frontend)

| Pattern | Meaning |
|---|---|
| `export default function Component()` | Default export, function declaration |
| `export const Component = () => {}` | Named export, arrow function |
| `export function Component()` | Named export, function declaration |
| `const Component: React.FC<Props> = ...` | Typed FC pattern (older style) |

**Note the dominant pattern — new components should match.**

## Import Style

| Pattern | Convention |
|---|---|
| `import { x } from '@/lib/utils'` | Absolute with alias |
| `import { x } from '~/lib/utils'` | Absolute with tilde alias |
| `import { x } from '../../../lib/utils'` | Relative only |
| `import { x } from 'src/lib/utils'` | Absolute from src root |
| `import x from './utils'` | Relative with default imports |

**Check tsconfig.json `paths` or `baseUrl` for alias configuration.**

## Export Style

| Pattern | Meaning |
|---|---|
| `index.ts` re-exports everything | Barrel file pattern (module boundaries) |
| Each file exports directly | No barrels (simpler, faster builds) |
| Mix of both | Barrels at feature boundaries only |

## Formatting (Authoritative Sources)

Check these files for definitive formatting rules:

- `.prettierrc` / `.prettierrc.json` / `prettier.config.*` — semicolons, quotes, tab width, trailing commas
- `.editorconfig` — indent style, indent size, end of line
- `biome.json` — all-in-one formatter + linter config
- `.eslintrc*` — code quality rules (not just formatting)
- `deno.json` — Deno's built-in formatter settings
- `rustfmt.toml` — Rust formatting
- `.ruff.toml` / `ruff` section in `pyproject.toml` — Python formatting

**If no formatter config exists:** Sample 3 files and check:
- Tabs or spaces? How many?
- Semicolons or no semicolons?
- Single quotes or double quotes?
- Trailing commas?

## Error Handling Patterns

| Pattern | Style |
|---|---|
| `try { ... } catch (e) { ... }` | Try-catch (JS/TS/Java) |
| `if err != nil { return err }` | Error return (Go) |
| `Result<T, E>` / `.unwrap()` / `?` | Result type (Rust) |
| `raise` + `except` | Exception-based (Python) |
| Custom `AppError` class | Typed errors with codes |
| `{ success: bool, data?, error? }` | Result wrapper pattern |

## Type Patterns (TypeScript)

| Pattern | Style |
|---|---|
| `interface User { ... }` | Interface for object shapes |
| `type User = { ... }` | Type alias for object shapes |
| `type Props = { ... }` | Props as type (common in React) |
| `interface Props { ... }` | Props as interface |
| `z.object({ ... })` | Zod schema (runtime + type) |
| `export type { ... }` | Type-only exports |

**Note:** The choice between `interface` and `type` is often inconsistent. Report what the majority uses.
