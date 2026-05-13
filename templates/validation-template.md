# Specification Validation Report

**Ticket**: `[TICKET_ID]`
**Date**: [DATE]
**Threshold**: [PASS_THRESHOLD]/100
**Status**: [OVERALL_STATUS]

## Output Schema

The validation agent MUST produce `artifacts/validation.json` matching this exact key schema:

```json
{
  "metadata": {
    "ticket_id": "string|null",
    "doc_type": "jira|prd|enhancement|null",
    "pass_threshold": 80,
    "output_mode": "json_only|json_plus_summary",
    "weights_applied": { "completeness": 0.6, "quality": 0.4 }
  },
  "validation_results": {
    "completeness_score": 0,
    "quality_score": 0,
    "overall_score": 0,
    "overall_status": "PASS|NEEDS_REVISION|BLOCKED",
    "missing_elements": ["string"],
    "quality_issues": [
      {
        "type": "Ambiguity|Testability|Sizing|Consistency",
        "quote": "string",
        "suggestion": "string"
      }
    ],
    "cert_manager_ecosystem": {
      "api_lifecycle_complete": false,
      "rbac_blast_radius_documented": false,
      "webhook_tls_and_failure_modes": false,
      "install_uninstall_semantics_clear": false,
      "platform_matrix_addressed": false,
      "observability_status_documented": false,
      "upgrade_skew_addressed": false,
      "gaps": ["string"]
    },
    "blockers": ["string"],
    "non_blockers": ["string"]
  }
}
```

### Field Rules

- `cert_manager_ecosystem` booleans: set `true` ONLY if the spec text substantively covers that area. Put questions and missing details in `gaps` even when boolean is `false`.
- `blockers`: issues preventing safe implementation or causing spec self-contradiction.
- `non_blockers`: improvements that do not necessarily stop initial implementation.
- `missing_elements`: core completeness pillars that are absent from the spec.
- `quality_issues`: each must include a direct `quote` from the spec and a concrete `suggestion` for how to fix it.

### Scoring Math

- `completeness_score`: 0-100. If any core completeness pillar is missing, cap at 60.
- `quality_score`: 0-100 from ambiguity/testability/sizing/consistency checks.
- `overall_score`: `round(0.6 * completeness_score + 0.4 * quality_score)` unless user provides custom weights.
- `overall_status`:
  - `PASS`: overall_score >= pass_threshold AND no items in `blockers`
  - `NEEDS_REVISION`: overall_score < pass_threshold OR non-fatal gaps present
  - `BLOCKED`: severe contradictions even if scores are high (mutually exclusive behaviors, API described two ways, uninstall semantics contradict CR lifecycle)

---

## Few-Shot Calibration Examples

### Example 1: Well-Written Spec (PASS)

**Input spec text:**
> **Title**: Add certificate rotation support for webhook serving certs
>
> **Motivation**: Cluster admins currently must manually restart the operator pod when the serving certificate expires, causing 15-minute outages on average. This impacts all clusters running cert-manager-operator v1.13+.
>
> **User Persona**: Cluster administrator managing OpenShift 4.14+ clusters with cert-manager-operator installed.
>
> **Acceptance Criteria**:
> 1. Given a webhook serving cert within 30 days of expiry, When the reconciler runs, Then a new Certificate CR is created targeting the serving-cert Secret.
> 2. Given cert-manager issues a new certificate, When the Secret is updated, Then the webhook configuration is patched with the new CA bundle within 60 seconds.
> 3. Given cert-manager is unavailable, When certificate rotation is attempted, Then the operator logs a warning event, sets a Degraded status condition, and continues serving with the existing cert.
>
> **Scope**: Only webhook serving certs. Mutual TLS and client certs are out of scope. No changes to the CRD API.
>
> **Dependencies**: Requires cert-manager v1.12+ with Certificate CRD. No database migrations.
>
> **Impacted Repos**: openshift/cert-manager-operator (operator logic), openshift/cert-manager-operator (e2e tests).
>
> **RBAC**: Operator ServiceAccount needs `get/create/update` on `certificates.cert-manager.io` in the operator namespace. No cluster-wide secret access added.
>
> **Upgrade**: Existing clusters without rotation get it automatically on operator upgrade. No migration needed. Downgrade: rotation CRs are ignored by older operator versions (no cleanup needed).

**Expected output:**

```json
{
  "metadata": {
    "ticket_id": "CM-801",
    "doc_type": "jira",
    "pass_threshold": 80,
    "output_mode": "json_plus_summary",
    "weights_applied": { "completeness": 0.6, "quality": 0.4 }
  },
  "validation_results": {
    "completeness_score": 92,
    "quality_score": 88,
    "overall_score": 90,
    "overall_status": "PASS",
    "missing_elements": [],
    "quality_issues": [
      {
        "type": "Testability",
        "quote": "patched with the new CA bundle within 60 seconds",
        "suggestion": "Clarify whether 60 seconds is measured from Secret update or from reconciler detecting the change. Consider specifying the metric to assert on in e2e tests."
      }
    ],
    "cert_manager_ecosystem": {
      "api_lifecycle_complete": true,
      "rbac_blast_radius_documented": true,
      "webhook_tls_and_failure_modes": true,
      "install_uninstall_semantics_clear": true,
      "platform_matrix_addressed": false,
      "observability_status_documented": true,
      "upgrade_skew_addressed": true,
      "gaps": [
        "Platform matrix: Does this apply to MicroShift or only full OpenShift? Are there FeatureGate requirements?"
      ]
    },
    "blockers": [],
    "non_blockers": [
      "Platform matrix coverage for MicroShift could be explicitly stated"
    ]
  }
}
```

---

### Example 2: Poor Spec (NEEDS_REVISION)

**Input spec text:**
> **Title**: Make the dashboard faster
>
> We need to improve the dashboard performance. Users are complaining it's slow. The table should load fast and be user-friendly. We should also add some new charts and maybe a dark mode toggle.

**Expected output:**

```json
{
  "metadata": {
    "ticket_id": "DASH-456",
    "doc_type": "jira",
    "pass_threshold": 80,
    "output_mode": "json_plus_summary",
    "weights_applied": { "completeness": 0.6, "quality": 0.4 }
  },
  "validation_results": {
    "completeness_score": 20,
    "quality_score": 15,
    "overall_score": 18,
    "overall_status": "NEEDS_REVISION",
    "missing_elements": [
      "Context & Motivation: No business impact quantified, no user pain point beyond 'slow'",
      "User Personas: No target user defined (admin? end-user? internal team?)",
      "Acceptance Criteria: No conditions for 'done' exist",
      "Scope Boundaries: 'maybe a dark mode toggle' is undefined scope",
      "Dependencies: No systems, APIs, or data sources identified",
      "Impacted Repositories: No repos listed"
    ],
    "quality_issues": [
      {
        "type": "Ambiguity",
        "quote": "The table should load fast",
        "suggestion": "Replace 'load fast' with a measurable target, e.g., 'table renders in under 500ms with 10,000 rows'."
      },
      {
        "type": "Ambiguity",
        "quote": "be user-friendly",
        "suggestion": "Define what 'user-friendly' means: specific interactions, accessibility standards (WCAG 2.1 AA), or usability test pass rates."
      },
      {
        "type": "Sizing",
        "quote": "improve the dashboard performance... add some new charts and maybe a dark mode toggle",
        "suggestion": "This ticket combines 3 independent deliverables (performance, charts, dark mode). Split into separate tickets or create an Epic."
      },
      {
        "type": "Testability",
        "quote": "Users are complaining it's slow",
        "suggestion": "Add Given/When/Then acceptance criteria. E.g., 'Given a dataset of 10k rows, When the user opens the dashboard, Then the table renders within 500ms as measured by Lighthouse CI'."
      }
    ],
    "cert_manager_ecosystem": {
      "api_lifecycle_complete": true,
      "rbac_blast_radius_documented": true,
      "webhook_tls_and_failure_modes": true,
      "install_uninstall_semantics_clear": true,
      "platform_matrix_addressed": true,
      "observability_status_documented": true,
      "upgrade_skew_addressed": true,
      "gaps": []
    },
    "blockers": [],
    "non_blockers": [
      "Performance target not quantified",
      "Scope includes unrelated features (charts, dark mode)"
    ]
  }
}
```

---

### Example 3: Contradictory Spec (BLOCKED)

**Input spec text:**
> **Title**: Add new TrustPolicy CRD for cross-namespace certificate issuance
>
> **Description**: Add a cluster-scoped TrustPolicy CRD that allows namespaces to reference issuers from other namespaces. The CRD should be namespace-scoped so tenants can manage their own policies. On uninstall, all TrustPolicy CRs must be preserved for audit. The operator finalizer must delete all TrustPolicy CRs on uninstall to avoid orphans.

**Expected output:**

```json
{
  "metadata": {
    "ticket_id": "CM-999",
    "doc_type": "enhancement",
    "pass_threshold": 80,
    "output_mode": "json_plus_summary",
    "weights_applied": { "completeness": 0.6, "quality": 0.4 }
  },
  "validation_results": {
    "completeness_score": 45,
    "quality_score": 30,
    "overall_score": 39,
    "overall_status": "BLOCKED",
    "missing_elements": [
      "User Personas: Who creates TrustPolicies—cluster admin or namespace admin?",
      "Acceptance Criteria: No testable conditions defined",
      "Scope Boundaries: No out-of-scope items listed",
      "Impacted Repositories: No repos identified",
      "RBAC: Cross-namespace access model not specified"
    ],
    "quality_issues": [
      {
        "type": "Consistency",
        "quote": "cluster-scoped TrustPolicy CRD... should be namespace-scoped",
        "suggestion": "CRD scope is mutually exclusive: choose cluster-scoped OR namespace-scoped and document the rationale."
      },
      {
        "type": "Consistency",
        "quote": "TrustPolicy CRs must be preserved for audit... must delete all TrustPolicy CRs on uninstall",
        "suggestion": "Uninstall behavior contradicts itself. Define one policy: either preserve CRs (remove finalizer, leave CRs) or clean up CRs (finalizer deletes them). Cannot do both."
      }
    ],
    "cert_manager_ecosystem": {
      "api_lifecycle_complete": false,
      "rbac_blast_radius_documented": false,
      "webhook_tls_and_failure_modes": false,
      "install_uninstall_semantics_clear": false,
      "platform_matrix_addressed": false,
      "observability_status_documented": false,
      "upgrade_skew_addressed": false,
      "gaps": [
        "API lifecycle: CRD scope contradiction must be resolved before API can be designed",
        "RBAC: Cross-namespace issuer reference implies cluster-wide read on Issuers—blast radius not documented",
        "Install/uninstall: Contradictory CR lifecycle on uninstall",
        "Webhooks: Will this CRD have validation/mutation webhooks? TLS issuance path?",
        "Platform matrix: OpenShift/MicroShift/Hypershift applicability not stated",
        "Observability: Status conditions for TrustPolicy not defined",
        "Upgrade: Migration path from no-TrustPolicy to TrustPolicy not addressed"
      ]
    },
    "blockers": [
      "CRD scope contradiction: spec says both cluster-scoped and namespace-scoped",
      "Uninstall semantics contradiction: spec says both preserve and delete CRs"
    ],
    "non_blockers": [
      "Missing acceptance criteria (fixable)",
      "Missing impacted repositories (fixable)"
    ]
  }
}
```

---

## User Message Template

When invoking the validator manually, use this format:

```
metadata:
  ticket_id: <OPTIONAL e.g. CM-624>
  doc_type: enhancement
  pass_threshold: 80
  output_mode: json_plus_summary

specification:
<PASTE SPEC TEXT HERE>
```
