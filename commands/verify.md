---
title: /verify Command
description: Run comprehensive verification on current codebase state
---

# /verify Command

Run comprehensive verification on current codebase state - build, types, lint, tests, and more.

## Verification Steps

Executed in this exact order:

1. **Build Check** - Run the build command for this project
2. **Type Check** - Run TypeScript/type checker  
3. **Lint Check** - Run linter
4. **Test Suite** - Run all tests with coverage
5. **Console.log Audit** - Search for console.log in source files
6. **Git Status** - Show uncommitted changes

## Command Syntax

```bash
/verify [mode]
```

<ParamField path="mode" type="string" default="full">
  Verification mode:
  - `quick` - Only build + types
  - `full` - All checks (default)
  - `pre-commit` - Checks relevant for commits
  - `pre-pr` - Full checks plus security scan
</ParamField>

## Example Output

```
VERIFICATION: PASS

Build:    OK
Types:    OK
Lint:     OK
Tests:    45/45 passed, 87% coverage
Secrets:  OK
Logs:     2 console.logs found

Ready for PR: YES
```

## Examples

```bash
# Full verification
/verify

# Quick check (build + types only)
/verify quick

# Pre-commit checks
/verify pre-commit

# Full pre-PR verification
/verify pre-pr
```

## Related

- **Commands**: `/build-fix`, `/test-coverage`, `/code-review`
