---
title: /multi-execute Command
description: Multi-model collaborative execution - Get prototype → Refactor → Multi-model audit
---

# /multi-execute Command

Multi-model collaborative execution - Get prototype from plan → Claude refactors and implements → Multi-model audit and delivery.

## Core Protocols

- **Language Protocol**: Use English when interacting with tools/models
- **Code Sovereignty**: External models have **zero filesystem write access**, all modifications by Claude
- **Dirty Prototype Refactoring**: Treat Codex/Gemini Unified Diff as "dirty prototype", must refactor to production-grade
- **Prerequisite**: Only execute after user explicitly confirms plan

## Command Syntax

```bash
/multi-execute <plan-file|task-description>
```

<ParamField path="plan-file|task-description" type="string" required>
  Path to plan file (`.claude/plan/feature.md`) or direct task description
</ParamField>

## Execution Workflow

### Phase 0: Read Plan

1. **Identify Input Type** - Plan file path or direct task
2. **Read Plan Content** - Extract task type, steps, key files, SESSION_ID
3. **Pre-Execution Confirmation** - Confirm user approval
4. **Task Type Routing**:
   - **Frontend** → Gemini
   - **Backend** → Codex
   - **Fullstack** → Codex ∥ Gemini parallel

### Phase 1: Quick Context Retrieval

Call `mcp__ace-tool__search_context` based on "Key Files" list in plan.

### Phase 3: Prototype Acquisition

**Route Based on Task Type:**

- **Frontend/UI** → Gemini (frontend design authority)
- **Backend/Logic** → Codex (backend logic authority)
- **Fullstack** → Parallel calls to both

Each model returns **Unified Diff Patch ONLY** (no file modifications).

### Phase 4: Code Implementation

Claude as Code Sovereign:

1. **Read Diff** - Parse Unified Diff Patch from Codex/Gemini
2. **Mental Sandbox** - Simulate applying Diff
3. **Refactor and Clean** - Convert "dirty prototype" to production-grade code
4. **Minimal Scope** - Changes limited to requirement scope only
5. **Apply Changes** - Use Edit/Write tools
6. **Self-Verification** - Run lint/typecheck/tests

### Phase 5: Audit and Delivery

**Automatic Audit** - Parallel call Codex and Gemini for Code Review:

- **Codex Review**: Security, performance, error handling, logic
- **Gemini Review**: Accessibility, design consistency, UX

**Integrate and Fix** - Synthesize feedback, execute fixes

**Delivery Confirmation**:

```markdown
## Execution Complete

### Change Summary
| File | Operation | Description |
|------|-----------|-------------|
| path/to/file.ts | Modified | Description |

### Audit Results
- Codex: Passed
- Gemini: Passed

### Recommendations
1. [ ] Test the changes
2. [ ] Verify in browser
```

## Examples

```bash
# Execute plan file
/multi-execute .claude/plan/feature-name.md

# Execute task directly
/multi-execute implement user authentication based on previous plan
```

## Key Rules

1. **Code Sovereignty** - All file modifications by Claude
2. **Dirty Prototype Refactoring** - Codex/Gemini output treated as draft
3. **Trust Rules** - Backend follows Codex, Frontend follows Gemini
4. **Minimal Changes** - Only modify necessary code
5. **Mandatory Audit** - Must perform multi-model Code Review after changes

## Related

- **Commands**: `/multi-plan`, `/multi-workflow`
