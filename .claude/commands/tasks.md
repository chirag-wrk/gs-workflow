---
description: "Stage 4: Produce an Execution Backlog (tasks.md) with dependency graph, agent routing, complexity, and per-task payloads."
---

## Prerequisites

Verify all prior artifacts exist:
- `artifacts/specs.md` (from Stage 1)
- `artifacts/constitution.md` (from Stage 2)
- `artifacts/repo-assessment.md` (from Stage 2)
- `artifacts/plan.md` (from Stage 3)

If any is missing:
```
Error: Required artifacts not found.
- artifacts/specs.md: [found/missing]
- artifacts/constitution.md: [found/missing]
- artifacts/repo-assessment.md: [found/missing]
- artifacts/plan.md: [found/missing]
Run the prior stages first: /specify, /constitute, /plan.
```

## Execution

Follow Stage 4 (Task Creation) from `CLAUDE.md`:

1. Read all four approved artifacts and `templates/tasks-template.md`.
2. Adopt the Sub-Task Creation Agent (TPM mode) role per CLAUDE.md.
3. Generate `artifacts/tasks.md` per the Stage 4 instructions in CLAUDE.md — populate all 6 sections (Input Coverage, Dependency Graph, Linear Order, Task Manifest, Task Payloads, Orchestration Notes).
4. **GATE 4**: Summarize tasks.md — highlight total task count, tasks per phase, agent distribution, critical-path length, total complexity points, and any tasks marked `Evidence: PARTIAL`. Ask the user for approval using AskUserQuestion.
   - On approve: report completion. Suggest running `/implement` next.
   - On reject: revise based on feedback and re-present.
