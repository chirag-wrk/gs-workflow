# GS Workflow Quality Rubric

Evaluate the overall workflow execution quality after all stages complete. Read each criterion, score it, then call `evaluate_rubric` with your scores and reasoning.

---

## Spec Completeness (1-5)

**Score 1**: Spec is a near-copy of the Jira ticket with no added structure. Missing user stories, requirements, or success criteria.
**Score 2**: Spec has basic structure but user stories lack acceptance scenarios, requirements are vague, or success criteria are not measurable.
**Score 3**: All mandatory sections present. User stories have Given/When/Then scenarios. Requirements are testable. A few gaps in edge cases or assumptions.
**Score 4**: Thorough spec with prioritized user stories, complete acceptance scenarios, measurable success criteria, and documented assumptions. Minor gaps only.
**Score 5**: Comprehensive spec that adds significant value beyond the Jira ticket. Every requirement is unambiguous and testable. Edge cases covered. Clear priority ordering enables MVP delivery.

---

## Repo Understanding Accuracy (1-5)

**Score 1**: Constitution is generic boilerplate unrelated to the actual repository.
**Score 2**: Mentions the correct tech stack but principles do not reflect actual repo conventions.
**Score 3**: Accurately captures tech stack and major patterns. Some conventions missed or inferred incorrectly.
**Score 4**: Constitution faithfully reflects repo conventions, testing approach, and architecture patterns with specific evidence from the codebase.
**Score 5**: Constitution is grounded in concrete examples from the repo. Every principle maps to observable patterns. Identifies how the new feature fits into existing architecture.

---

## Plan Quality (1-5)

**Score 1**: Plan is a restatement of the spec with no technical decisions.
**Score 2**: Has a technical context section but architecture decisions lack rationale or ignore constitution principles.
**Score 3**: Solid plan with technical context, project structure, and constitution check. Research phase addressed unknowns. Some decisions lack alternatives-considered reasoning.
**Score 4**: Well-structured plan where every decision traces to spec requirements or constitution principles. Data model and contracts are defined. Clear phasing.
**Score 5**: Exceptional plan with thorough research, justified decisions with alternatives considered, complete data model, interface contracts, and a project structure that matches the repo's existing patterns exactly.

---

## Task Actionability (1-5)

**Score 1**: Tasks are vague descriptions without file paths or IDs.
**Score 2**: Tasks have IDs but descriptions are too broad for an LLM to execute without additional context.
**Score 3**: Tasks follow the checklist format with IDs, file paths, and story labels. Some tasks are still ambiguous or missing dependencies.
**Score 4**: Every task is specific enough for immediate execution. Proper phase ordering, parallel markers, and story organization. Dependencies are clear.
**Score 5**: Tasks are perfectly ordered, every requirement has coverage, parallel opportunities are maximized, and the MVP-first strategy is clearly actionable. An LLM could execute each task with zero additional context.

---

## Implementation Fidelity (1-5)

**Score 1**: Code does not match the plan or spec. Wrong files modified, missing features.
**Score 2**: Partial implementation that covers some requirements but deviates from the plan structure.
**Score 3**: Implementation follows the plan and covers core requirements. Code conventions from the constitution are mostly followed. Some tasks incomplete.
**Score 4**: All planned tasks completed. Code matches repo conventions. Tests pass. PR is well-structured with a clear description.
**Score 5**: Complete implementation with all tasks checked off. Follows every constitution principle. Clean commit history referencing the Jira ticket. PR description links artifacts. Test coverage matches plan expectations.
