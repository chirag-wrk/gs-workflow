---
description: "Stage 5: Execute implementation tasks in the target repo."
---

## Prerequisites

Verify all prior artifacts exist:
- `artifacts/specs.md` (from Stage 1)
- `artifacts/constitution.md` (from Stage 2)
- `artifacts/plan.md` (from Stage 3)
- `artifacts/tasks.md` (from Stage 4)

If any is missing:
```
Error: Required artifacts not found.
- artifacts/specs.md: [found/missing]
- artifacts/constitution.md: [found/missing]
- artifacts/plan.md: [found/missing]
- artifacts/tasks.md: [found/missing]
Run the prior stages first: /specify, /constitute, /plan, /tasks.
```

## Execution

Follow Stage 5 (Code Generation) from `CLAUDE.md`:

1. Read all approved artifacts from `artifacts/`.
<!-- TODO: Uncomment when ready to enable branch/PR creation
2. Create a feature branch in the target repo.
-->
2. Execute tasks phase-by-phase per the Stage 5 instructions in CLAUDE.md.
<!-- TODO: Uncomment when ready to enable branch/PR creation
3. Commit, push, and create a draft PR.
-->
3. Produce a final report (tasks completed, files changed, test results, deviations).
4. After reporting, evaluate quality using `evaluate_rubric` per `.ambient/rubric.md`.
