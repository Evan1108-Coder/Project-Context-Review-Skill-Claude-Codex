# Project Context Review Skill

A Claude/Codex skill that auto-scans a project codebase and generates structured context — tech stack, patterns, conventions, architecture — so the AI understands the project before writing code.

## What It Does

Instead of hand-writing CLAUDE.md files, this skill tells the AI HOW to scan your project and extract the facts it needs. When triggered, it:

1. **Scans** key project files (package manifests, configs, entry points, directory tree)
2. **Detects** tech stack, architecture patterns, naming conventions, and tooling
3. **Outputs** a structured context block that can be referenced while coding

The skill injects **knowledge** (what exists in this codebase), not **judgment** (how things should look). This distinction matters — [A/B testing showed](https://github.com/Evan1108-Coder/Frontend-Web-UI-Craft-Skill) that skills constraining creative judgment hurt AI performance, while skills injecting factual context help.

## Structure

```text
.
├── SKILL.md                    # Core skill — scan process + output format
├── lenses/
│   ├── code.md                 # Deep architecture & pattern analysis
│   ├── design.md               # UI/styling/component library analysis
│   ├── testing.md              # Test infrastructure & pattern analysis
│   └── docs.md                 # Documentation structure & API surface
├── detection/
│   ├── tech-stack.md           # File patterns → technology identification
│   ├── conventions.md          # How to identify naming/style conventions
│   └── architecture.md         # Directory patterns → architecture classification
├── examples/
│   ├── nextjs-saas.md          # Example output for a Next.js SaaS app
│   └── python-cli.md           # Example output for a Python CLI tool
├── scripts/
│   └── validate-skill.mjs      # Validation script
├── LICENSE
└── README.md
```

## Lenses

The skill supports focused scans via lenses:

| Lens | Use When |
|---|---|
| **Code** | Starting a new feature, understanding architecture, finding where to add code |
| **Design** | Working on UI, adding components, matching the existing styling approach |
| **Testing** | Writing tests, fixing test failures, setting up test infrastructure |
| **Docs** | Writing documentation, understanding the API surface, onboarding |

Use "full scan" (all lenses) when onboarding to a completely new project.

## Installation

### Claude Code (Project-Level)

```bash
mkdir -p .claude/skills
git clone -b master-skill https://github.com/Evan1108-Coder/Project-Context-Review-Skill-Claude-Codex.git .claude/skills/project-context-review
```

### Claude Code (User-Level)

```bash
mkdir -p ~/.claude/skills
git clone -b master-skill https://github.com/Evan1108-Coder/Project-Context-Review-Skill-Claude-Codex.git ~/.claude/skills/project-context-review
```

### Codex

Place the skill folder in your Codex skills directory per the Codex skill documentation.

### Claude.ai

```bash
git clone -b master-skill https://github.com/Evan1108-Coder/Project-Context-Review-Skill-Claude-Codex.git project-context-review
zip -r project-context-review.zip project-context-review -x "project-context-review/.git/*"
```

Upload `project-context-review.zip` in the Claude skills/projects interface.

## Usage

The skill triggers automatically when you:
- Start working on an unfamiliar codebase
- Ask the AI to "review the project context" or "scan this project"
- Need context before a major implementation task

You can also invoke explicitly:

```text
Use project-context-review to scan this codebase before I start implementing.
```

With a specific lens:

```text
Use project-context-review with the testing lens — I need to write tests for this project.
```

## Design Philosophy

This skill succeeds because it focuses on **factual context injection**:

- **DOES**: Detect what exists, identify patterns, report conventions, map architecture
- **DOES NOT**: Judge code quality, suggest improvements, prescribe patterns, constrain creativity

The AI writes better code when it knows the conventions. It writes worse code when it's trying to satisfy a checklist of aesthetic criteria.

## Validation

```bash
node scripts/validate-skill.mjs
```

## License

MIT. See [LICENSE](LICENSE).
