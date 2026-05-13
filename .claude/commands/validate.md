---
description: "Stage 0: Validate a Jira ticket's specification quality before entering the development pipeline."
---

## User Input

```text
$ARGUMENTS
```

## Parse Input

Extract from `$ARGUMENTS`:
- **JIRA_KEY**: The Jira ticket key (e.g., `PROJ-123`, `TEAM-456`). This is the first argument (required).
- **PASS_THRESHOLD**: Optional second argument — integer score threshold (default: 80).
- **DOC_TYPE**: Optional third argument — one of `jira`, `prd`, `enhancement` (default: `jira`).

If JIRA_KEY is missing or empty:
```
Error: Jira ticket key is required.
Usage: /validate <JIRA-KEY> [THRESHOLD] [DOC-TYPE]
Example: /validate PROJ-123
Example: /validate PROJ-123 85 enhancement
```

## Execution

Follow Stage 0 (Spec Validation) from `CLAUDE.md`:

1. Fetch Jira ticket **JIRA_KEY** using the available Jira MCP tools.
2. Read `templates/validation-template.md` for the JSON schema and few-shot examples.
3. Evaluate the ticket against the completeness and quality rubrics per Stage 0 in CLAUDE.md.
4. Write `artifacts/validation.json` matching the exact schema.
5. Apply gate behavior based on `overall_status`:
   - **PASS**: Present executive summary (up to 8 bullets). Report completion. Suggest running `/specify <JIRA-KEY>` next.
   - **NEEDS_REVISION**: Present missing elements, quality issues, and non-blockers. Ask via AskUserQuestion: "Proceed to Stage 1 anyway?" or "Stop and revise the ticket?" If stop, offer to comment on the Jira ticket with feedback.
   - **BLOCKED**: Present blocking issues. Halt. Do not offer a proceed option. Offer to comment on the Jira ticket with the blockers.
