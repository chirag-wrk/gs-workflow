---
description: "Stage 2: Analyze a GitHub repository and produce constitution.md and repo-assessment.md."
---

## User Input

```text
$ARGUMENTS
```

## Parse Input

Extract **REPO_URL** from `$ARGUMENTS` (e.g., `https://github.com/org/repo`).

If REPO_URL is missing or empty:
```
Error: GitHub repository URL is required.
Usage: /constitute <GITHUB-REPO-URL>
Example: /constitute https://github.com/org/repo
```

## Prerequisites

Verify `artifacts/specs.md` exists (produced by Stage 1). If missing:
```
Error: artifacts/specs.md not found. Run /specify <JIRA-KEY> first.
```

## Execution

Follow Stage 2 (Repo Understanding) from `CLAUDE.md`:

1. Analyze the repository at **REPO_URL** (available under `/workspace/repos/`). If not already cloned, clone it.
2. Read `templates/constitution-template.md` and `templates/repo-assessment-template.md`.
3. Generate `artifacts/constitution.md` per the Stage 2 instructions in CLAUDE.md.
4. Generate `artifacts/repo-assessment.md` per the Stage 2 instructions in CLAUDE.md — populate target files, reference context, reusable assets, guardrails, and risks from the repo analysis.
5. **GATE 2**: Summarize both constitution.md and repo-assessment.md and ask the user for approval using AskUserQuestion.
   - On approve: report completion. Suggest running `/plan` next.
   - On reject: revise based on feedback and re-present.
