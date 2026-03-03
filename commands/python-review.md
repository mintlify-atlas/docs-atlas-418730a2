---
title: /python-review Command
description: Comprehensive Python code review for PEP 8, type hints, security, and Pythonic idioms
---

# /python-review Command

This command invokes the **python-reviewer** agent for comprehensive Python-specific code review.

## What This Command Does

1. **Identify Python Changes**: Find modified `.py` files via `git diff`
2. **Run Static Analysis**: Execute `ruff`, `mypy`, `pylint`, `black --check`
3. **Security Scan**: Check for SQL injection, unsafe deserialization
4. **Type Safety Review**: Analyze type hints and mypy errors
5. **Pythonic Code Check**: Verify PEP 8 and Python best practices
6. **Generate Report**: Categorize issues by severity

## Review Categories

### CRITICAL (Must Fix)
- SQL/Command injection vulnerabilities
- Unsafe eval/exec usage
- Pickle unsafe deserialization
- Hardcoded credentials
- YAML unsafe load
- Bare except clauses hiding errors

### HIGH (Should Fix)
- Missing type hints on public functions
- Mutable default arguments
- Swallowing exceptions silently
- Not using context managers for resources
- C-style looping instead of comprehensions
- Using type() instead of isinstance()

### MEDIUM (Consider)
- PEP 8 formatting violations
- Missing docstrings on public functions
- Print statements instead of logging
- Not using f-strings for formatting
- Magic numbers without named constants

## Automated Checks Run

```bash
# Type checking
mypy .

# Linting and formatting
ruff check .
black --check .
isort --check-only .

# Security scanning
bandit -r .

# Dependency audit
pip-audit
safety check

# Testing
pytest --cov=app --cov-report=term-missing
```

## Command Syntax

```bash
/python-review
```

No arguments required - automatically reviews all uncommitted Python changes.

## Common Fixes

### Fix Mutable Defaults

```python
# Before
def append(value, items=[]):
    items.append(value)
    return items

# After
def append(value, items=None):
    if items is None:
        items = []
    items.append(value)
    return items
```

### Use Context Managers

```python
# Before
f = open("file.txt")
data = f.read()
f.close()

# After
with open("file.txt") as f:
    data = f.read()
```

### Use f-strings

```python
# Before
greeting = "Hello, " + name + "!"

# After
greeting = f"Hello, {name}!"
```

## Framework-Specific Reviews

### Django Projects
- N+1 query issues (use `select_related`, `prefetch_related`)
- Missing migrations for model changes
- Missing `transaction.atomic()` for multi-step operations

### FastAPI Projects
- CORS misconfiguration
- Pydantic models for request validation
- Proper async/await usage

### Flask Projects
- Context management (app context, request context)
- Proper error handling
- Blueprint organization

## Related

- **Agent**: `agents/python-reviewer.md`
- **Skills**: `skills/python-patterns/`, `skills/python-testing/`
- **Commands**: `/tdd`, `/code-review`, `/verify`
