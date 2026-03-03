---
title: /test-coverage Command
description: Analyze test coverage, identify gaps, and generate missing tests to reach 80%+
---

# /test-coverage Command

Analyze test coverage, identify gaps, and generate missing tests to reach 80%+ coverage.

## Process

1. **Detect Test Framework** - Identify coverage tool
2. **Analyze Coverage Report** - List files below 80%
3. **Generate Missing Tests** - Prioritize happy path, errors, edge cases
4. **Verify** - Run tests and check coverage
5. **Report** - Show before/after comparison

## Supported Test Frameworks

| Indicator | Coverage Command |
|-----------|------------------|
| `jest.config.*` or `package.json` jest | `npx jest --coverage --coverageReporters=json-summary` |
| `vitest.config.*` | `npx vitest run --coverage` |
| `pytest.ini` / `pyproject.toml` pytest | `pytest --cov=src --cov-report=json` |
| `Cargo.toml` | `cargo llvm-cov --json` |
| `pom.xml` with JaCoCo | `mvn test jacoco:report` |
| `go.mod` | `go test -coverprofile=coverage.out ./...` |

## Test Generation Priority

1. **Happy path** - Core functionality with valid inputs
2. **Error handling** - Invalid inputs, missing data, network failures
3. **Edge cases** - Empty arrays, null/undefined, boundary values
4. **Branch coverage** - Each if/else, switch case, ternary

## Command Syntax

```bash
/test-coverage
```

No arguments required.

## Example Output

```
Coverage Report
──────────────────────────────
File                   Before  After
src/services/auth.ts   45%     88%
src/utils/validation.ts 32%    82%
──────────────────────────────
Overall:               67%     84%  ✅
```

## Coverage Targets

| Code Type | Target |
|-----------|--------|
| General code | 80%+ |
| Public APIs | 90%+ |
| Critical business logic | 100% |
| Generated code | Exclude |

## Test Generation Rules

- Place tests adjacent to source: `foo.ts` → `foo.test.ts`
- Use existing test patterns from the project
- Mock external dependencies (database, APIs, file system)
- Each test should be independent
- Name tests descriptively: `test_create_user_with_duplicate_email_returns_409`

## Related

- **Commands**: `/tdd`, `/verify`, `/e2e`
