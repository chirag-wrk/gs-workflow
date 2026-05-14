# Repository Assessment Report

**Feature**: [FEATURE_SUMMARY]
**Repo**: [REPO_URL]
**Branch**: [BRANCH]
**Commit**: [COMMIT_SHA] ([COMMIT_DESCRIPTION])
**Date**: [DATE]

## 0. Inputs & Tooling

<!--
  ACTION REQUIRED: Record what was available during the assessment.
  tooling_status reflects how deeply the repo was analyzed:
    FULL   — local clone with full search, vendor/ read, test execution
    PARTIAL — remote API / selective file reads, no full ripgrep or deep vendor scan
  key_finding_for_planning is the single most important fact that downstream
  Planning (Stage 3) needs to know before it starts.
-->

| Field | Value |
|-------|-------|
| repo | [REPO_URL] |
| branch | [BRANCH] |
| commit | [COMMIT_SHA] |
| tooling_status | FULL\|PARTIAL |

**Key Finding for Planning**: [ONE_PARAGRAPH_SUMMARY]
<!-- Example: "On current master, trust-manager support already has substantial in-tree structure (API types, dedicated controller package, bindata tree). Planning should default to delta work (gaps vs the enhancement) unless your branch is behind this snapshot." -->

---

## 1. Target Files (Modification & Creation)

<!--
  ACTION REQUIRED: List every file the feature will likely MODIFY or CREATE.
  For each file, state:
    - The file path relative to repo root
    - A brief rationale (why this file is touched)
    - Evidence source (e.g., "GitHub contents API", "local grep", "commit history")

  "Target Files" means files that will receive new or changed lines of code.
  Files that are only READ for context belong in Section 2 (Reference Context).

  If a file is auto-generated (e.g., zz_generated.deepcopy.go, CRD YAML),
  note that it is regenerated via codegen — do not hand-edit.
-->

| File | Rationale | Evidence |
|------|-----------|----------|
| [FILE_PATH] | [WHY_MODIFIED] | [HOW_DISCOVERED] |
| [FILE_PATH] | [WHY_MODIFIED] | [HOW_DISCOVERED] |

---

## 2. Reference Context (Read-Only)

<!--
  ACTION REQUIRED: List files that provide important context or patterns
  but should NOT be modified by this feature. These are exemplars the
  Planning stage should read to understand conventions and mirror patterns.

  Group by purpose when helpful (e.g., "parallel controller patterns",
  "existing update scripts", "build targets").
-->

- [FILE_PATH] — [PURPOSE]
<!-- Example: pkg/controller/certmanager/ — Closest existing operand controller pattern to mirror -->
- [FILE_PATH] — [PURPOSE]
- [FILE_PATH] — [PURPOSE]

---

## 3. Reusable Assets (Anti-Duplication)

<!--
  ACTION REQUIRED: Identify existing code, patterns, or infrastructure
  that MUST be reused rather than reimplemented. Each item should be
  a clear "do not reinvent this" directive with a reason.

  Format: "Do not [BAD_APPROACH]: [GOOD_APPROACH] because [REASON]."
-->

- **[ASSET_NAME]**: Do not [BAD_APPROACH]. Instead, [REUSE_DIRECTIVE] because [REASON].
<!-- Example: "Reconciliation framework: Do not add a second reconciliation framework for trust-manager. Extend the existing pkg/controller/trustmanager split (deployments/rbac/webhooks) rather than introducing a parallel controller package." -->
- **[ASSET_NAME]**: Do not [BAD_APPROACH]. Instead, [REUSE_DIRECTIVE] because [REASON].

---

## 4. Architectural Guardrails

<!--
  ACTION REQUIRED: Document hard constraints from the repo's structure,
  build system, libraries, or conventions that the feature implementation
  MUST respect. These are not preferences — violating a guardrail would
  break the build, tests, or operational model.

  Derive these from the repo's actual code, not generic best practices.
-->

- **[GUARDRAIL_NAME]**: [CONSTRAINT_DESCRIPTION]
<!-- Example: "Library-go / OpenShift operator patterns: starter.go uses OpenShift config clients, library-go status/version patterns, and a unified controller-runtime manager — keep new work consistent with that approach." -->
- **[GUARDRAIL_NAME]**: [CONSTRAINT_DESCRIPTION]
- **[GUARDRAIL_NAME]**: [CONSTRAINT_DESCRIPTION]

---

## 5. Risks & Downstream Impacts

<!--
  ACTION REQUIRED: Identify risks that could affect Planning or
  implementation. Include cross-repo dependencies, upgrade/migration
  concerns, CI blast radius, and anything that might surprise the
  Planning stage.
-->

- **[RISK_NAME]**: [RISK_DESCRIPTION]
<!-- Example: "Spec vs repo maturity mismatch: If your local intent is 'greenfield implementation,' master may already implement much of the enhancement — Planning could waste effort re-building. Start from a gap analysis against your target release branch." -->
- **[RISK_NAME]**: [RISK_DESCRIPTION]

### 5.1 Assessment Limitations / UNVERIFIED

<!--
  ACTION REQUIRED: List anything the assessment could not verify due to
  tooling limitations, time constraints, or access restrictions. Planning
  must treat these as open questions and verify them before relying on
  assumptions.

  If tooling_status is FULL and everything was verified, this section
  can state "None — full verification completed."
-->

- [UNVERIFIED_ITEM]
<!-- Example: "Exact ControllerManager construction details live under pkg/operator/setup_manager.go (not opened in this pass) — verify when planning controller lifecycle changes." -->
- [UNVERIFIED_ITEM]
