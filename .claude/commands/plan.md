---
description: "Stage 3: Produce a Technical Implementation Plan (plan.md) with architecture, contracts, phases, and risks."
---

## Prerequisites

Verify all Stage 2 artifacts exist:
- `artifacts/specs.md` (from Stage 1)
- `artifacts/constitution.md` (from Stage 2)
- `artifacts/repo-assessment.md` (from Stage 2)

If any is missing:
```
Error: Required artifacts not found.
- artifacts/specs.md: [found/missing]
- artifacts/constitution.md: [found/missing]
- artifacts/repo-assessment.md: [found/missing]
Run /specify and /constitute first.
```

## Execution

Follow Stage 3 (Planning) from `CLAUDE.md`:

1. Read approved `artifacts/specs.md`, `artifacts/constitution.md`, and `artifacts/repo-assessment.md`.
2. Read `templates/plan-template.md`.
3. Generate `artifacts/plan.md` per the Stage 3 instructions in CLAUDE.md — populate all 9 sections (Inputs, Strategy, Persistence, Interfaces, Dependencies, Phases, Verification, Risks, Open Questions).
4. **GATE 3**: Summarize plan.md — highlight architectural strategy, number of phases, critical-path dependencies, top risks, and open questions. Ask the user for approval using AskUserQuestion.
   - On approve: report completion. Suggest running `/tasks` next.
   - On reject: revise based on feedback and re-present.
