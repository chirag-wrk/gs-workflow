---
description: "Stage 1: Read a Jira ticket and produce specs.md with user stories, requirements, and success criteria."
---

## User Input

```text
$ARGUMENTS
```

## Parse Input

Extract **JIRA_KEY** from `$ARGUMENTS` (e.g., `PROJ-123`, `TEAM-456`).

If JIRA_KEY is missing or empty:
```
Error: Jira ticket key is required.
Usage: /specify <JIRA-KEY>
Example: /specify PROJ-123
```

## Execution

Follow Stage 1 (Spec Understanding) from `CLAUDE.md`:

1. Fetch Jira ticket **JIRA_KEY** using the available Jira MCP tools.
2. Read `templates/spec-template.md`.
3. Generate `artifacts/specs.md` per the Stage 1 instructions in CLAUDE.md.
4. Run spec quality validation.
5. **GATE 1**: Summarize specs.md and ask the user for approval using AskUserQuestion.
   - On approve: report completion. Suggest running `/constitute <REPO-URL>` next.
   - On reject: revise based on feedback and re-present.
