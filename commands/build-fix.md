---
title: /build-fix Command
description: Incrementally fix build and type errors with minimal, safe changes
---

# /build-fix Command

Incrementally fix build and type errors with minimal, safe changes.

## What This Command Does

1. **Detect Build System** - Identify project type and build command
2. **Parse and Group Errors** - Group by file, sort by dependency order
3. **Fix Loop** - Fix one error at a time, verify after each
4. **Summary** - Report errors fixed, remaining, and new errors

## Supported Build Systems

| Indicator | Build Command |
|-----------|---------------|
| `package.json` with `build` script | `npm run build` or `pnpm build` |
| `tsconfig.json` (TypeScript only) | `npx tsc --noEmit` |
| `Cargo.toml` | `cargo build 2>&1` |
| `pom.xml` | `mvn compile` |
| `build.gradle` | `./gradlew compileJava` |
| `go.mod` | `go build ./...` |
| `pyproject.toml` | `python -m py_compile` or `mypy .` |

## Fix Strategy

1. **Build errors first** - Code must compile
2. **Vet warnings second** - Fix suspicious constructs
3. **Lint warnings third** - Style and best practices
4. **One fix at a time** - Verify each change
5. **Minimal changes** - Don't refactor, just fix

## Fix Loop Process

For each error:

1. **Read the file** - See error context (10 lines around error)
2. **Diagnose** - Identify root cause
3. **Fix minimally** - Smallest change that resolves error
4. **Re-run build** - Verify error is gone
5. **Move to next** - Continue with remaining errors

## Command Syntax

```bash
/build-fix
```

No arguments required - automatically detects build system and fixes errors.

## Example Session

```
# Initial Build
$ npm run build

Error: Type 'string' is not assignable to type 'number'
  src/utils/calc.ts:25:15

Error: Cannot find name 'User'
  src/api/users.ts:42:9

Total: 2 errors

# Fix 1: Type Mismatch
File: src/utils/calc.ts:25
Changing: count = params.get("count")
To: count = Number(params.get("count"))

$ npm run build
Remaining: 1 error

# Fix 2: Missing Import
File: src/api/users.ts:42
Adding: import { User } from "./types"

$ npm run build
Build successful! ✅

# Summary
- Errors fixed: 2
- Files modified: 2
- Remaining issues: 0
```

## Common Errors Fixed

| Error | Typical Fix |
|-------|-------------|
| `undefined: X` | Add import or fix typo |
| `cannot use X as Y` | Type conversion or fix assignment |
| `missing return` | Add return statement |
| `X does not implement Y` | Add missing method |
| `import cycle` | Restructure packages |
| `declared but not used` | Remove or use variable |
| `cannot find package` | `go get` or `go mod tidy` |

## Stop Conditions

The command stops and asks for help if:
- Same error persists after 3 attempts
- Fix introduces more errors than it resolves
- Requires architectural changes (not just a build fix)
- Missing external dependencies need installation

## Integration with Other Commands

- Use after making code changes
- Use before running tests with `/verify`
- Language-specific: `/go-build` for Go projects

## Related

- **Agent**: `agents/build-error-resolver.md`
- **Commands**: `/go-build`, `/verify`, `/tdd`
