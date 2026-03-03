---
title: /eval Command
description: Manage eval-driven development workflow
---

# /eval Command

Manage eval-driven development workflow.

## Command Syntax

```bash
/eval <action> [feature-name]
```

<ParamField path="action" type="string" required>
  Action: `define`, `check`, `report`, `list`, or `clean`
</ParamField>

<ParamField path="feature-name" type="string">
  Feature name (required for define, check, report)
</ParamField>

## Actions

### Define Evals

```bash
/eval define user-authentication
```

Creates eval definition at `.claude/evals/user-authentication.md`:

```markdown
## EVAL: user-authentication
Created: 2026-03-03

### Capability Evals
- [ ] User can sign up with email/password
- [ ] User can log in with valid credentials
- [ ] Invalid credentials return 401
- [ ] JWT token is returned on successful login

### Regression Evals
- [ ] Existing public endpoints still work without auth
- [ ] Database migrations apply cleanly

### Success Criteria
- pass@3 > 90% for capability evals
- pass^3 = 100% for regression evals
```

### Check Evals

```bash
/eval check user-authentication
```

Runs evals and reports:

```
EVAL CHECK: user-authentication
========================
Capability: 4/4 passing
Regression: 2/2 passing
Status: READY
```

### Report Evals

```bash
/eval report user-authentication
```

Generate comprehensive report:

```markdown
EVAL REPORT: user-authentication
=========================
Generated: 2026-03-03

CAPABILITY EVALS
----------------
[eval-1]: PASS (pass@1)
[eval-2]: PASS (pass@2) - required retry
[eval-3]: PASS (pass@1)
[eval-4]: PASS (pass@1)

REGRESSION EVALS
----------------
[test-1]: PASS
[test-2]: PASS

METRICS
-------
Capability pass@1: 75%
Capability pass@3: 100%
Regression pass^3: 100%

RECOMMENDATION
--------------
SHIP
```

### List Evals

```bash
/eval list
```

Shows all eval definitions:

```
EVAL DEFINITIONS
================
feature-auth      [3/5 passing] IN PROGRESS
feature-search    [5/5 passing] READY
feature-export    [0/4 passing] NOT STARTED
```

## Related

- **Commands**: `/checkpoint`, `/verify`, `/tdd`
