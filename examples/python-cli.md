# Example Output: Python CLI Tool

This is what the skill's output looks like for a Python command-line application.

---

## Project Context: dataforge

**Stack**: Python 3.12 + Click + SQLite
**Architecture**: Flat monolith (CLI tool)
**Package Manager**: uv | **Build**: hatchling | **Deploy**: PyPI package

### Key Dependencies
- `click` — CLI framework (commands, options, arguments)
- `rich` — Terminal output formatting (tables, progress bars, panels)
- `sqlite-utils` — SQLite wrapper (no ORM, direct SQL + convenience methods)
- `httpx` — HTTP client for API calls
- `pydantic` — Data validation and serialization

### File Structure Pattern
- Single `src/dataforge/` package with flat module structure
- Entry: `src/dataforge/cli.py` (Click group) | Core: `src/dataforge/core.py`
- Commands as separate modules: `src/dataforge/commands/`

### Conventions
- Naming: files: snake_case, functions: snake_case, classes: PascalCase
- Imports: relative within package (`from .core import ...`), absolute for deps
- Exports: `__all__` in `__init__.py` for public API
- Formatting: Ruff (line-length 88, double quotes, trailing commas)

### Patterns In Use
- State: No persistent state — CLI is stateless per invocation
- Data fetching: `httpx` with retry logic in `src/dataforge/client.py`
- Styling: N/A (CLI)
- Testing: pytest with fixtures in `tests/conftest.py`, tmp_path for file tests
- Error handling: Custom `DataForgeError` base class, Click's `ClickException` for user-facing errors

### Important Context
- Entry point defined in `pyproject.toml` `[project.scripts]`: `dataforge = "dataforge.cli:main"`
- Database file created at `~/.dataforge/data.db` on first run
- `tests/` mirrors `src/dataforge/` structure — one test file per module
- CI runs `ruff check` + `ruff format --check` + `pytest` (see `.github/workflows/ci.yml`)
- Type-checked with `mypy` in strict mode — all functions need annotations
