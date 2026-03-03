---
title: /evolve Command
description: Analyze instincts and suggest or generate evolved structures
---

# /evolve Command

Analyzes instincts and clusters related ones into higher-level structures:
- **Commands**: When instincts describe user-invoked actions
- **Skills**: When instincts describe auto-triggered behaviors
- **Agents**: When instincts describe complex, multi-step processes

## Command Syntax

```bash
/evolve [--generate]
```

<ParamField path="--generate" type="boolean">
  Also generate files under `evolved/{skills,commands,agents}`
</ParamField>

## Evolution Rules

### → Command (User-Invoked)

When instincts describe actions a user would explicitly request:
- Multiple instincts about "when user asks to..."
- Instincts with triggers like "when creating a new X"
- Instincts that follow a repeatable sequence

**Example:**
- `new-table-step1`: "when adding a database table, create migration"
- `new-table-step2`: "when adding a database table, update schema"
- `new-table-step3`: "when adding a database table, regenerate types"

→ Creates: **new-table** command

### → Skill (Auto-Triggered)

When instincts describe behaviors that should happen automatically:
- Pattern-matching triggers
- Error handling responses
- Code style enforcement

**Example:**
- `prefer-functional`: "when writing functions, prefer functional style"
- `use-immutable`: "when modifying state, use immutable patterns"
- `avoid-classes`: "when designing modules, avoid class-based design"

→ Creates: `functional-patterns` skill

### → Agent (Needs Depth/Isolation)

When instincts describe complex, multi-step processes:
- Debugging workflows
- Refactoring sequences
- Research tasks

**Example:**
- `debug-step1`: "when debugging, first check logs"
- `debug-step2`: "when debugging, isolate the failing component"
- `debug-step3`: "when debugging, create minimal reproduction"
- `debug-step4`: "when debugging, verify fix with test"

→ Creates: **debugger** agent

## Example Output

```
============================================================
  EVOLVE ANALYSIS - 12 instincts
  Project: my-app (a1b2c3d4e5f6)
  Project-scoped: 8 | Global: 4
============================================================

High confidence instincts (>=80%): 5

## SKILL CANDIDATES
1. Cluster: "adding tests"
   Instincts: 3
   Avg confidence: 82%
   Domains: testing
   Scopes: project

## COMMAND CANDIDATES (2)
  /adding-tests
    From: test-first-workflow [project]
    Confidence: 84%

## AGENT CANDIDATES (1)
  adding-tests-agent
    Covers 3 instincts
    Avg confidence: 82%
```

## Generated File Locations

- **Project scope**: `~/.claude/homunculus/projects/<project-id>/evolved/`
- **Global fallback**: `~/.claude/homunculus/evolved/`

## Related

- **Commands**: `/instinct-status`, `/promote`, `/learn-eval`
- **Skill**: `skills/continuous-learning-v2/`
