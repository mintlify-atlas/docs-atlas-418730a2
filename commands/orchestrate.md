---
title: /orchestrate Command
description: Sequential agent workflow for complex tasks
---

# /orchestrate Command

Sequential agent workflow for complex tasks - chains specialized agents together.

## Workflow Types

### feature
Full feature implementation workflow:
```
planner → tdd-guide → code-reviewer → security-reviewer
```

### bugfix
Bug investigation and fix workflow:
```
planner → tdd-guide → code-reviewer
```

### refactor
Safe refactoring workflow:
```
architect → code-reviewer → tdd-guide
```

### security
Security-focused review:
```
security-reviewer → code-reviewer → architect
```

## Command Syntax

```bash
/orchestrate <workflow-type> <task-description>
```

<ParamField path="workflow-type" type="string" required>
  Type of workflow: `feature`, `bugfix`, `refactor`, `security`, or `custom`
</ParamField>

<ParamField path="task-description" type="string" required>
  Description of the task to orchestrate
</ParamField>

## Examples

### Feature Workflow

```bash
/orchestrate feature "Add user authentication"
```

Executes:
1. **Planner Agent** - Analyzes requirements, creates implementation plan
2. **TDD Guide Agent** - Writes tests first, implements to pass tests
3. **Code Reviewer Agent** - Reviews implementation, suggests improvements
4. **Security Reviewer Agent** - Security audit, vulnerability check

### Custom Workflow

```bash
/orchestrate custom "architect,tdd-guide,code-reviewer" "Redesign caching layer"
```

## Handoff Document Format

Between agents, a handoff document is created:

```markdown
## HANDOFF: planner → tdd-guide

### Context
User authentication system implementation

### Findings
- Use JWT tokens for session management
- Store refresh tokens in secure HTTP-only cookies
- Implement password hashing with bcrypt

### Files Modified
- None yet (planning phase)

### Open Questions
- Should we support OAuth providers?
- Password reset flow via email or SMS?

### Recommendations
- Start with email/password auth
- Add social OAuth in Phase 2
- Implement rate limiting on login endpoint
```

## Final Report Format

```markdown
ORCHESTRATION REPORT
====================
Workflow: feature
Task: Add user authentication
Agents: planner → tdd-guide → code-reviewer → security-reviewer

SUMMARY
Implemented JWT-based authentication with password hashing,
rate limiting, and comprehensive test coverage.

AGENT OUTPUTS
-------------
Planner: Created 4-phase implementation plan
TDD Guide: Implemented with 95% test coverage
Code Reviewer: Found 2 MEDIUM issues, all resolved
Security Reviewer: No vulnerabilities found

FILES CHANGED
-------------
- src/auth/login.ts (new)
- src/auth/tokens.ts (new)
- src/middleware/auth.ts (new)
- tests/auth/login.test.ts (new)

TEST RESULTS
------------
42/42 tests passed
95% coverage

SECURITY STATUS
---------------
No vulnerabilities found
Rate limiting implemented
Passwords hashed with bcrypt (cost 10)

RECOMMENDATION
--------------
SHIP - Ready for production
```

## Related

- **Agents**: All 13 specialized agents
- **Commands**: `/plan`, `/tdd`, `/code-review`
