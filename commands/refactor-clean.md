---
title: /refactor-clean Command
description: Safely identify and remove dead code with test verification at every step
---

# /refactor-clean Command

Safely identify and remove dead code with test verification at every step.

## Process

1. **Detect Dead Code** - Run analysis tools
2. **Categorize Findings** - Sort into safety tiers
3. **Safe Deletion Loop** - Delete one item at a time, verify tests
4. **Handle Caution Items** - Check for dynamic imports and string references
5. **Consolidate Duplicates** - Merge near-duplicate functions
6. **Summary** - Report results

## Dead Code Detection Tools

| Tool | What It Finds | Command |
|------|--------------|---------|  
| knip | Unused exports, files, dependencies | `npx knip` |
| depcheck | Unused npm dependencies | `npx depcheck` |
| ts-prune | Unused TypeScript exports | `npx ts-prune` |
| vulture | Unused Python code | `vulture src/` |
| deadcode | Unused Go code | `deadcode ./...` |
| cargo-udeps | Unused Rust dependencies | `cargo +nightly udeps` |

## Safety Tiers

| Tier | Examples | Action |
|------|----------|--------|
| **SAFE** | Unused utilities, test helpers, internal functions | Delete with confidence |
| **CAUTION** | Components, API routes, middleware | Verify no dynamic imports |
| **DANGER** | Config files, entry points, type definitions | Investigate before touching |

## Safe Deletion Loop

For each SAFE item:

1. **Run full test suite** - Establish baseline (all green)
2. **Delete the dead code** - Surgical removal
3. **Re-run test suite** - Verify nothing broke
4. **If tests fail** - Immediately revert and skip
5. **If tests pass** - Move to next item

## Command Syntax

```bash
/refactor-clean
```

No arguments required.

## Example Output

```
Dead Code Cleanup
──────────────────────────────
Deleted:   12 unused functions
           3 unused files
           5 unused dependencies
Skipped:   2 items (tests failed)
Saved:     ~450 lines removed
──────────────────────────────
All tests passing ✅
```

## Rules

- **Never delete without running tests first**
- **One deletion at a time** - Atomic changes make rollback easy
- **Skip if uncertain** - Better to keep dead code than break production
- **Don't refactor while cleaning** - Separate concerns

## Related

- **Commands**: `/verify`, `/test-coverage`
