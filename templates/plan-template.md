# Technical Implementation Plan

**Feature**: [FEATURE_SUMMARY]
**Date**: [DATE]
**Spec**: `artifacts/specs.md`
**Repo Assessment**: `artifacts/repo-assessment.md`
**Constitution**: `artifacts/constitution.md`

---

## 0. Inputs Acknowledged

<!--
  ACTION REQUIRED: Record every upstream artifact this plan depends on.
  Copy coordinates from the actual artifacts produced in earlier stages.
  If an input was NOT provided, say so explicitly — do not silently omit it.
  The constitution status field is critical: if constitution.md was not provided
  or uses placeholder rules, the plan must note that and list the provisional
  guardrails it assumed instead.
-->

| Input | Status |
|-------|--------|
| Spec source | [TICKET_ID or enhancement name from `artifacts/specs.md`] |
| Repo assessment pin | [REPO_URL], branch [BRANCH], commit [COMMIT_SHA] (tooling_status: [FULL\|PARTIAL] from `repo-assessment.md` Section 0) |
| `agents.md` | [PROVIDED / NOT PROVIDED — if not provided, state that phases use provisional capability taxonomy] |
| `validation.json` | [PROVIDED / NOT PROVIDED — optional] |
| `constitution.md` | [PROVIDED / CONSTITUTION_PLACEHOLDER — if placeholder, list the provisional guardrails assumed below] |

**Provisional guardrails (only if constitution.md is CONSTITUTION_PLACEHOLDER)**:
<!-- Delete this block entirely when a real constitution.md is provided -->

- [GUARDRAIL_1]
<!-- Example: "Prefer smallest change that meets the spec; do not refactor unrelated controllers." -->
- [GUARDRAIL_2]
<!-- Example: "All behavior changes must be covered by automated tests where the repo already has suites for that area." -->

---

## 1. Architectural Strategy

<!--
  ACTION REQUIRED: Synthesize the high-level integration approach from:
    - spec requirements (artifacts/specs.md)
    - constitution principles or provisional guardrails (artifacts/constitution.md)
    - repo assessment guardrails and reusable assets (artifacts/repo-assessment.md Sections 3-4)

  This is a prose section. State WHAT the approach is and WHY it was chosen.
  Do not describe individual tasks — that is Stage 4's job.

  Include a "Repo-grounded reality check" paragraph that cross-references the
  repo-assessment.md Key Finding for Planning (Section 0) to determine whether
  this is greenfield work, delta/hardening work, or a mix of both.
-->

[ARCHITECTURAL_STRATEGY_DESCRIPTION]

**Repo-grounded reality check** (from `repo-assessment.md`): [REALITY_CHECK_PARAGRAPH]
<!-- Example: "master already contains substantial trust-manager implementation surfaces (API types, dedicated controller package, bindata tree, hack/update-trust-manager-manifests.sh, e2e tests). Therefore this plan is written to support both delivery/GA hardening work aligned to the enhancement's graduation criteria, and spec delta work (upstream API migration risks, tightening RBAC scope, documentation/upgrade policy)." -->

---

## 2. Persistence & State

<!--
  ACTION REQUIRED: Describe the state model for this feature.

  For Kubernetes operator work: list Kubernetes objects as "source of truth"
  vs "derived/reconciled", external/platform-injected state, and operand
  runtime state. Reference specific CRs, ConfigMaps, Secrets, Deployments.

  For web/CLI/library projects: describe DB schemas, session stores, file
  state, caches, or configuration persistence as applicable.

  If the feature is purely stateless (e.g., a refactoring or a CLI flag),
  state "N/A — no new persistence introduced" and briefly explain why.
-->

[PERSISTENCE_AND_STATE_DESCRIPTION]

---

## 3. Interfaces & Contracts

<!--
  ACTION REQUIRED: Define every interface boundary that downstream tasks
  must implement. Only include subsections that apply to this feature —
  delete the rest. Each subsection defines a "contract surface" that
  tasks will code against.

  Derive contract details from:
    - spec requirements (artifacts/specs.md functional requirements)
    - repo assessment target files (artifacts/repo-assessment.md Section 1)
    - repo assessment reference context (artifacts/repo-assessment.md Section 2)
-->

### 3.1 APIs
<!-- CRDs, REST endpoints, gRPC services, CLI commands, library public interfaces -->

[API_CONTRACTS]

### 3.2 Controller / Runtime Interfaces
<!-- Internal reconcile semantics, event handlers, manager registration, startup gating -->
<!-- Delete this subsection if the feature does not involve a controller or runtime -->

[CONTROLLER_CONTRACTS]

### 3.3 Webhooks / Admission
<!-- Validating/mutating webhooks, TLS contracts, failure modes -->
<!-- Delete this subsection if not applicable -->

[WEBHOOK_CONTRACTS]

### 3.4 RBAC / Security Boundaries
<!-- Roles, ClusterRoles, ServiceAccount permissions, blast radius documentation -->
<!-- Delete this subsection if no RBAC changes -->

[RBAC_CONTRACTS]

### 3.5 Packaging / Distribution
<!-- OLM bundle, Helm chart, container images, CSV updates, relatedImages -->
<!-- Delete this subsection if no packaging changes -->

[PACKAGING_CONTRACTS]

---

## 4. Dependencies & Sequencing Graph

<!--
  ACTION REQUIRED: Identify the critical path through the implementation,
  what can be parallelized, and what depends on external teams or systems.

  Derive from:
    - spec dependencies and acceptance criteria ordering
    - repo-assessment.md Section 5 (Risks & Downstream Impacts)
    - repo-assessment.md Section 4 (Architectural Guardrails)

  The sequencing graph drives Phase ordering in Section 5.
-->

### Critical Path

1. [STEP_1]
2. [STEP_2]
3. [STEP_3]

### Parallelizable Streams

- [STREAM_A] vs [STREAM_B] (after [PREREQUISITE])

### External Dependencies

- [EXTERNAL_DEPENDENCY]: [DESCRIPTION_AND_IMPACT]

---

## 5. Implementation Phases

<!--
  ACTION REQUIRED: Break the architectural strategy into logical phases.
  Phases are architecture-level groupings, NOT individual tasks — task
  granularity belongs to Stage 4 (artifacts/tasks.md).

  Each phase must include:
    - Goal: what is true when this phase completes
    - Dependencies: which prior phases (or external events) must finish first
    - Target files: sourced from repo-assessment.md Section 1
    - Required capabilities: provisional labels until agents.md is provided
    - Verification hooks: how to confirm the phase is done (tests, scripts, manual checks)

  Number phases sequentially. Typical patterns:
    - Phase 1: Contracts / API stabilization
    - Phase 2: Core implementation
    - Phase 3: Integration / wiring
    - Phase 4: Testing
    - Phase 5: Packaging / docs
  Adapt to the feature's actual structure.
-->

### Phase 1: [PHASE_NAME]

**Goal**: [WHAT_IS_TRUE_WHEN_DONE]

**Dependencies**: [PRIOR_PHASES_OR_NONE]

**Target files**:
- [FILE_PATH] — [RATIONALE]

**Required capabilities**: [CAPABILITY_LABELS]
<!-- Example: OperatorController + API (provisional) -->

**Verification hooks**: [HOW_TO_CONFIRM_DONE]

---

### Phase 2: [PHASE_NAME]

**Goal**: [WHAT_IS_TRUE_WHEN_DONE]

**Dependencies**: Phase 1

**Target files**:
- [FILE_PATH] — [RATIONALE]

**Required capabilities**: [CAPABILITY_LABELS]

**Verification hooks**: [HOW_TO_CONFIRM_DONE]

---

<!-- Add more phases as needed, following the same structure -->

---

## 6. Verification Matrix

<!--
  ACTION REQUIRED: Map spec acceptance criteria to test categories.
  Each row states the test type, what it covers, and where the tests
  live (or will live) in the repo. Source file paths from
  repo-assessment.md Sections 1-2.

  If a category does not apply, include it with "N/A" and a brief reason.
-->

| Category | Coverage | Files / Suites |
|----------|----------|----------------|
| Unit | [WHAT_UNIT_TESTS_COVER] | [FILE_PATHS] |
| Integration | [WHAT_INTEGRATION_TESTS_COVER] | [FILE_PATHS] |
| E2E | [WHAT_E2E_TESTS_COVER] | [FILE_PATHS] |
| Manual / Cluster | [MANUAL_VERIFICATION_STEPS] | [RUNBOOK_COMMANDS] |
| N/A | [WHAT_IS_NOT_TESTED_AND_WHY] | - |

---

## 7. Risks, Migrations & Operational Follow-ups

<!--
  ACTION REQUIRED: Surface every risk that could affect implementation
  or downstream consumers. Derive from:
    - repo-assessment.md Section 5 (Risks & Downstream Impacts)
    - repo-assessment.md Section 5.1 (UNVERIFIED items)
    - spec gaps or areas where constitution principles are strained
    - upgrade/migration concerns from the spec

  Each risk has a name and a description. If the risk has a mitigation
  or follow-up action, state it.
-->

- **[RISK_NAME]**: [RISK_DESCRIPTION_AND_MITIGATION]
- **[RISK_NAME]**: [RISK_DESCRIPTION_AND_MITIGATION]

---

## 8. Open Questions / SME Decisions

<!--
  ACTION REQUIRED: List decisions the plan cannot make without additional
  input. These are blockers or near-blockers for task creation. Each item
  should state:
    - The question
    - Who or what can answer it (SME, constitution.md, agents.md, downstream repo)
    - What the plan assumes if no answer is provided before Stage 4

  If there are no open questions, state "None — all decisions resolved
  in this plan."
-->

- [OPEN_QUESTION]: [WHO_CAN_ANSWER] — assumed [DEFAULT_ASSUMPTION] if unresolved.
- [OPEN_QUESTION]: [WHO_CAN_ANSWER] — assumed [DEFAULT_ASSUMPTION] if unresolved.
