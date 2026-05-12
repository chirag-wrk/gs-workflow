---
description: "Stage 4: Produce tasks.md with phased, actionable implementation tasks from the approved plan."
---

## Prerequisites

Verify all prior artifacts exist:
- `artifacts/specs.md` (from Stage 1)
- `artifacts/constitution.md` (from Stage 2)
- `artifacts/plan.md` (from Stage 3)

If any is missing:
```
Error: Required artifacts not found.
- artifacts/specs.md: [found/missing]
- artifacts/constitution.md: [found/missing]
- artifacts/plan.md: [found/missing]
Run the prior stages first: /specify, /constitute, /plan.
```

## Execution

Follow Stage 4 (Task Creation) from `CLAUDE.md`:

1. Read all three approved artifacts and `templates/tasks-template.md`.
2. Generate `artifacts/tasks.md` per the Stage 4 instructions in CLAUDE.md.
3. **GATE 4**: Summarize tasks.md (total tasks, per-story breakdown, MVP scope) and ask the user for approval using AskUserQuestion.
   - On approve: report completion. Suggest running `/implement` next.
   - On reject: revise based on feedback and re-present.
