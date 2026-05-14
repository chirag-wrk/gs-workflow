---
description: "Stage 5: Execute tasks from the Execution Backlog in the target repo."
---

## Prerequisites

Verify all prior artifacts exist:
- `artifacts/specs.md` (from Stage 1)
- `artifacts/constitution.md` (from Stage 2)
- `artifacts/repo-assessment.md` (from Stage 2)
- `artifacts/plan.md` (from Stage 3)
- `artifacts/tasks.md` (from Stage 4)

If any is missing:
```
Error: Required artifacts not found.
- artifacts/specs.md: [found/missing]
- artifacts/constitution.md: [found/missing]
- artifacts/repo-assessment.md: [found/missing]
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
2. Execute tasks following the Linear Execution Order (tasks.md Section 2) or DAG (Section 1). For each task, read its Task Specification payload (Section 4) for target files, acceptance criteria, and non-goals. Respect Parallel OK flags from the Task Manifest (Section 3).
<!-- TODO: Uncomment when ready to enable branch/PR creation
3. Commit, push, and create a draft PR.
-->
3. Produce a final report (Task IDs completed vs. planned, files changed vs. payload targets, test results, deviations).
4. After reporting, evaluate quality using `evaluate_rubric` per `.ambient/rubric.md`.
