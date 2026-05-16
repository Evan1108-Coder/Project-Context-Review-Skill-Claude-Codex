# Testing Lens — Test Infrastructure & Pattern Analysis

Use this lens when writing tests, debugging test failures, or setting up test infrastructure. Detects exactly how this project tests so new tests match existing patterns.

## What to Scan

### Test Framework

Identify from config and lock files:
- **JavaScript/TypeScript**: Jest, Vitest, Mocha, Playwright, Cypress, Testing Library
- **Python**: pytest, unittest, hypothesis
- **Go**: built-in `testing`, testify, gomock
- **Rust**: built-in `#[test]`, proptest, mockall
- **Java/Kotlin**: JUnit, Mockito, TestContainers

Check the test config file for custom settings:
- `jest.config.*` / `vitest.config.*` / `playwright.config.*` / `pytest.ini` / `conftest.py`
- Transform settings, module aliases, setup files, global mocks

### Test Location Pattern

Where do tests live?
- **Co-located**: `Component.test.tsx` next to `Component.tsx`
- **Mirror tree**: `tests/` mirrors `src/` structure
- **Feature-grouped**: Tests inside feature folders
- **Flat**: All tests in one `__tests__/` or `tests/` directory

Check the pattern by running: find test files, compare paths to source files.

### Test Patterns

Sample 3-5 test files and identify:
- **Describe/it structure** or flat test functions?
- **Arrange-Act-Assert** or inline assertions?
- **Factory functions** for test data or inline objects?
- **beforeEach/afterEach** patterns or fresh setup per test?
- **Snapshot testing** used? Where?

### Mocking Approach

How does this project handle dependencies in tests?
- **Mock framework**: jest.mock, vi.mock, unittest.mock, testify/mock
- **DI-based**: Inject test implementations (no mocking library)
- **Test doubles directory**: Check for `__mocks__/`, `testutils/`, `fixtures/`
- **HTTP mocking**: MSW, nock, httptest, VCR

### Test Data

How is test data managed?
- **Fixtures**: JSON/YAML files in `fixtures/` or `__fixtures__/`
- **Factories**: Builder pattern or factory functions (check for `factory`, `create`, `build` in test utils)
- **Seeds**: Database seeds for integration tests
- **Inline**: Data defined directly in each test

### E2E / Integration Tests

If present, identify:
- What tool? (Playwright, Cypress, Selenium, supertest)
- What do they test? (Critical paths, smoke tests, full flows)
- How to run them? (Separate command, needs running server, Docker)
- Where do they live? (Separate directory, separate package)

### Coverage & CI

- Coverage tool configured? (c8, istanbul, coverage.py, go tool cover)
- Coverage thresholds set? (Check config for `coverageThreshold` or equivalent)
- Which tests run in CI? (Check `.github/workflows/` or CI config)
- Separate test commands? (`test:unit`, `test:e2e`, `test:integration`)

## Output Additions

```markdown
### Test Infrastructure
- Framework: [name] | Config: [path]
- Location: [co-located / mirror tree / etc]
- Run command: [npm test / pytest / go test ./...]
- Coverage: [tool] | Threshold: [if set]

### Test Patterns
- Structure: [describe/it or flat]
- Data: [factories / fixtures / inline]
- Mocking: [approach + library]
- Setup: [beforeEach pattern or per-test]

### E2E Tests
- Tool: [name] | Location: [path]
- Run: [command] | Requires: [server, DB, Docker?]

### To Write a New Test
- Create file: [where + naming pattern]
- Import from: [test utilities path]
- Mock pattern: [how to mock dependencies]
- Run: [command to run single test file]
```
