---
title: /checkpoint Command
description: Create or verify checkpoints in your development workflow
---

# /checkpoint Command

Create or verify checkpoints in your development workflow.

## Command Syntax

```bash
/checkpoint <action> [name]
```

<ParamField path="action" type="string" required>
  Action to perform: `create`, `verify`, `list`, or `clear`
</ParamField>

<ParamField path="name" type="string">
  Checkpoint name (required for create and verify)
</ParamField>

## Actions

### Create Checkpoint

```bash
/checkpoint create "feature-start"
```

When creating a checkpoint:
1. Run `/verify quick` to ensure current state is clean
2. Create a git stash or commit with checkpoint name
3. Log checkpoint to `.claude/checkpoints.log`
4. Report checkpoint created

### Verify Checkpoint

```bash
/checkpoint verify "feature-start"
```

Compares current state to checkpoint:
- Files added since checkpoint
- Files modified since checkpoint
- Test pass rate now vs then
- Coverage now vs then

### List Checkpoints

```bash
/checkpoint list
```

Shows all checkpoints with:
- Name
- Timestamp
- Git SHA
- Status (current, behind, ahead)

### Clear Old Checkpoints

```bash
/checkpoint clear
```

Remove old checkpoints (keeps last 5)

## Typical Workflow

```bash
# Start feature
/checkpoint create "feature-start"

# Implement core
/checkpoint create "core-done"

# Verify progress
/checkpoint verify "core-done"

# After refactoring
/checkpoint create "refactor-done"

# Before PR
/checkpoint verify "feature-start"
```

## Example Output

```
CHECKPOINT COMPARISON: feature-start
============================
Files changed: 12
Tests: +5 passed / -0 failed
Coverage: +8% (79% → 87%)
Build: PASS

Summary:
- Added 8 new files
- Modified 4 existing files
- All tests passing
- Coverage improved
```

## Related

- **Commands**: `/verify`, `/eval`
