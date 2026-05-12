---
description: "Run all 5 stages end-to-end: specify, constitute, plan, tasks, implement."
---

## User Input

```text
$ARGUMENTS
```

## Parse Input

Extract from `$ARGUMENTS`:
- **JIRA_KEY**: The Jira ticket key (e.g., `PROJ-123`, `TEAM-456`). This is the first argument.
- **REPO_URL**: The GitHub repository URL (e.g., `https://github.com/org/repo`). This is the second argument.

If JIRA_KEY is missing or empty:
```
Error: Jira ticket key is required.
Usage: /start <JIRA-KEY> <GITHUB-REPO-URL>
Example: /start PROJ-123 https://github.com/org/repo
```

If REPO_URL is missing or empty:
```
Error: GitHub repository URL is required.
Usage: /start <JIRA-KEY> <GITHUB-REPO-URL>
Example: /start PROJ-123 https://github.com/org/repo
```

## Execution

Run all 5 stages sequentially per `CLAUDE.md`. Each stage pauses at its approval gate before proceeding.

### Stage 1: Spec Understanding
Follow Stage 1 from CLAUDE.md using **JIRA_KEY**. Write `artifacts/specs.md`. Present summary and ask for approval via AskUserQuestion. Wait for approval before proceeding.

### Stage 2: Repo Understanding
Follow Stage 2 from CLAUDE.md using **REPO_URL**. Write `artifacts/constitution.md`. Present summary and ask for approval via AskUserQuestion. Wait for approval before proceeding.

### Stage 3: Planning
Follow Stage 3 from CLAUDE.md. Write `artifacts/plan.md`. Present summary and ask for approval via AskUserQuestion. Wait for approval before proceeding.

### Stage 4: Task Creation
Follow Stage 4 from CLAUDE.md. Write `artifacts/tasks.md`. Present summary and ask for approval via AskUserQuestion. Wait for approval before proceeding.

### Stage 5: Code Generation
Follow Stage 5 from CLAUDE.md. Create feature branch, execute tasks, commit, push, create draft PR. Produce final report.

After all stages complete, evaluate quality using `evaluate_rubric` per `.ambient/rubric.md`.
