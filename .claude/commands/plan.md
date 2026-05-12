---
description: "Stage 3: Produce plan.md from approved specs and constitution with technical context and architecture decisions."
---

## Prerequisites

Verify both artifacts exist:
- `artifacts/specs.md` (from Stage 1)
- `artifacts/constitution.md` (from Stage 2)

If either is missing:
```
Error: Required artifacts not found.
- artifacts/specs.md: [found/missing]
- artifacts/constitution.md: [found/missing]
Run /specify and /constitute first.
```

## Execution

Follow Stage 3 (Planning) from `CLAUDE.md`:

1. Read approved `artifacts/specs.md` and `artifacts/constitution.md`.
2. Read `templates/plan-template.md`.
3. Generate `artifacts/plan.md` per the Stage 3 instructions in CLAUDE.md.
4. **GATE 3**: Summarize plan.md and ask the user for approval using AskUserQuestion.
   - On approve: report completion. Suggest running `/tasks` next.
   - On reject: revise based on feedback and re-present.
