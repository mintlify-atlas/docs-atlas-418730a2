---
title: /tdd Command
description: Enforce test-driven development workflow with 80%+ coverage requirement
---

# /tdd Command

This command invokes the **tdd-guide** agent to enforce test-driven development methodology.

## What This Command Does

1. **Scaffold Interfaces** - Define types/interfaces first
2. **Generate Tests First** - Write failing tests (RED)
3. **Implement Minimal Code** - Write just enough to pass (GREEN)
4. **Refactor** - Improve code while keeping tests green (REFACTOR)
5. **Verify Coverage** - Ensure 80%+ test coverage

## When to Use

Use `/tdd` when:
- Implementing new features
- Adding new functions/components
- Fixing bugs (write test that reproduces bug first)
- Refactoring existing code
- Building critical business logic

## TDD Cycle

```
RED → GREEN → REFACTOR → REPEAT

RED:      Write a failing test
GREEN:    Write minimal code to pass
REFACTOR: Improve code, keep tests passing
REPEAT:   Next feature/scenario
```

## Command Syntax

```bash
/tdd <feature description>
```

<ParamField path="feature description" type="string" required>
  Description of the functionality to implement with TDD
</ParamField>

## Examples

### Basic Usage

```bash
/tdd I need a function to calculate market liquidity score
```

### Example Session

See the full example in the [source documentation](/home/daytona/workspace/source/commands/tdd.md) showing:

1. **Step 1**: Define Interface (SCAFFOLD)
2. **Step 2**: Write Failing Test (RED)
3. **Step 3**: Run Tests - Verify FAIL
4. **Step 4**: Implement Minimal Code (GREEN)
5. **Step 5**: Run Tests - Verify PASS
6. **Step 6**: Refactor (IMPROVE)
7. **Step 7**: Verify Tests Still Pass
8. **Step 8**: Check Coverage (80%+ required)

## TDD Best Practices

**DO:**
- ✅ Write the test FIRST, before any implementation
- ✅ Run tests and verify they FAIL before implementing
- ✅ Write minimal code to make tests pass
- ✅ Refactor only after tests are green
- ✅ Add edge cases and error scenarios
- ✅ Aim for 80%+ coverage (100% for critical code)

**DON'T:**
- ❌ Write implementation before tests
- ❌ Skip running tests after each change
- ❌ Write too much code at once
- ❌ Ignore failing tests
- ❌ Test implementation details (test behavior)
- ❌ Mock everything (prefer integration tests)

## Test Types to Include

**Unit Tests** (Function-level):
- Happy path scenarios
- Edge cases (empty, null, max values)
- Error conditions
- Boundary values

**Integration Tests** (Component-level):
- API endpoints
- Database operations
- External service calls
- React components with hooks

**E2E Tests** (use `/e2e` command):
- Critical user flows
- Multi-step processes
- Full stack integration

## Coverage Requirements

| Code Type | Target Coverage |
|-----------|----------------|
| All code | 80% minimum |
| Financial calculations | 100% |
| Authentication logic | 100% |
| Security-critical code | 100% |
| Core business logic | 100% |

## Integration with Other Commands

- Use `/plan` first to understand what to build
- Use `/tdd` to implement with tests
- Use `/build-fix` if build errors occur
- Use `/code-review` to review implementation
- Use `/test-coverage` to verify coverage

## Related

- **Agent**: `~/.claude/agents/tdd-guide.md`
- **Skill**: `~/.claude/skills/tdd-workflow/`
- **Commands**: `/plan`, `/test-coverage`, `/verify`
