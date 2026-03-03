---
title: /multi-plan Command
description: Multi-model collaborative planning with Context retrieval + Dual-model analysis
---

# /multi-plan Command

Multi-model collaborative planning - Context retrieval + Dual-model analysis (Codex + Gemini) → Generate step-by-step implementation plan.

## Core Protocols

- **Language Protocol**: Use English when interacting with tools/models
- **Mandatory Parallel**: Codex/Gemini calls MUST use `run_in_background: true`
- **Code Sovereignty**: External models have **zero filesystem write access**
- **Planning Only**: This command allows reading context and writing plan files, but **NEVER modify production code**

## Command Syntax

```bash
/multi-plan <feature description>
```

<ParamField path="feature description" type="string" required>
  Description of what needs to be planned
</ParamField>

## Execution Workflow

### Phase 1: Full Context Retrieval

1. **Prompt Enhancement** - Call `mcp__ace-tool__enhance_prompt`
2. **Context Retrieval** - Call `mcp__ace-tool__search_context`
3. **Completeness Check** - Ensure complete definitions
4. **Requirement Alignment** - Clarify ambiguities

### Phase 2: Multi-Model Collaborative Analysis

1. **Distribute Inputs** - Parallel call Codex and Gemini
   - **Codex**: Technical feasibility, architecture, risks
   - **Gemini**: UI/UX impact, visual design
2. **Cross-Validation** - Integrate perspectives
3. **Dual-Model Plan Draft** (Optional) - Both models output plan drafts
4. **Generate Implementation Plan** - Claude synthesizes final plan

## Model Roles

| Model | Authority | Focus |
|-------|-----------|-------|
| **Codex** | Backend | Technical feasibility, architecture impact, performance |
| **Gemini** | Frontend | UI/UX impact, user experience, visual design |
| **Claude** | Orchestrator | Synthesize plans, coordinate workflow |

## Plan Output

```markdown
## Implementation Plan: <Task Name>

### Task Type
- [ ] Frontend (→ Gemini)
- [x] Backend (→ Codex)
- [ ] Fullstack (→ Parallel)

### Technical Solution
<Optimal solution synthesized from Codex + Gemini analysis>

### Implementation Steps
1. <Step 1> - Expected deliverable
2. <Step 2> - Expected deliverable
...

### Key Files
| File | Operation | Description |
|------|-----------|-------------|
| path/to/file.ts:L10-L50 | Modify | Description |

### Risks and Mitigation
| Risk | Mitigation |
|------|------------|

### SESSION_ID (for /multi-execute use)
- CODEX_SESSION: <session_id>
- GEMINI_SESSION: <session_id>
```

## Plan Delivery

After planning:

1. Present complete implementation plan
2. Save plan to `.claude/plan/<feature-name>.md`
3. Output prompt:

```
**Plan generated and saved to `.claude/plan/feature-name.md`**

**Please review the plan above. You can:**
- **Modify plan**: Tell me what needs adjustment
- **Execute plan**: Copy the following command to a new session

```bash
/multi-execute .claude/plan/feature-name.md
```
```

4. Immediately terminate (no auto-execution)

## Absolutely Forbidden

- Ask user "Y/N" then auto-execute
- Any write operations to production code
- Automatically call `/multi-execute`
- Continue triggering model calls without explicit request

## Examples

```bash
/multi-plan Add real-time notifications when markets resolve
```

## Related

- **Commands**: `/multi-execute`, `/multi-workflow`, `/plan`
