---
title: /promote Command
description: Promote project-scoped instincts to global scope
---

# /promote Command

Promote instincts from project scope to global scope when they're valuable across multiple projects.

## Command Syntax

```bash
/promote [instinct-id] [options]
```

<ParamField path="instinct-id" type="string">
  Specific instinct ID to promote (optional)
</ParamField>

<ParamField path="--dry-run" type="boolean">
  Preview promotion candidates without promoting
</ParamField>

<ParamField path="--force" type="boolean">
  Promote all qualified candidates without prompt
</ParamField>

## Examples

```bash
# Auto-detect promotion candidates
/promote

# Preview candidates
/promote --dry-run

# Force promote all qualified
/promote --force

# Promote specific instinct
/promote grep-before-edit
```

## Promotion Logic

1. Detects current project
2. If `instinct-id` provided, promotes only that instinct
3. Otherwise, finds cross-project candidates that:
   - Appear in at least 2 projects
   - Meet confidence threshold (typically 0.7+)
4. Writes promoted instincts to `~/.claude/homunculus/instincts/personal/` with `scope: global`

## Example Output

```
🔼 Promotion Candidates
========================

Found 3 instincts that appear in multiple projects:

1. grep-before-edit
   - Projects: 3
   - Avg confidence: 0.82
   - Action: Search codebase before editing
   → Promote to global? YES

2. test-first
   - Projects: 2
   - Avg confidence: 0.75
   - Action: Write tests before implementation
   → Promote to global? YES

Promote 2 instincts to global scope? (yes/no)
```

## Related

- **Commands**: `/instinct-status`, `/evolve`, `/projects`
