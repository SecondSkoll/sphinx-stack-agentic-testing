# Adopt the latest Canonical Sphinx Stack release

Adopt the latest stable published version of Canonical's Sphinx Stack
(https://github.com/canonical/sphinx-stack) in each scenario below. Perform the
adoptions rather than only describing them, then run controlled build fuzzing
and critically evaluate the experience from the perspective of a relatively
inexperienced developer.

## Required skills

Before selecting a release or modifying files, load and follow these skills
with the skill tool:

1. `sphinx-stack-release-selection`, using **latest** selection mode.
2. `sphinx-stack-migration-validation`, using the direct-adoption workflow.
3. `sphinx-stack-build-fuzzing`.
4. `sphinx-stack-test-report`, using the adoption report contract.

If any skill is unavailable, stop before modifying the repository and
report the configuration blocker. This prompt supplies the workflow-specific
requirements and deliverables; follow it where it is more specific.

## Scenario matrix

Run both scenarios independently against the same selected Stack release:

| ID | Input | Coverage |
|---|---|---|
| `local-rst` | This repository's original `source/` documentation and root build configuration | Standalone reStructuredText site |
| `reference-generic-agentic-workflows` | The documentation fixture exposed by the OpenCode `generic-agentic-workflows` reference | Real-world embedded documentation, including its original syntax, navigation, assets, and surrounding constraints |

Treat the reference as read-only. Record its resolved commit and relevant
documentation root. Reproduce its documentation fixture in this ephemeral
repository for migration without editing the reference cache or unrelated
application files. If the reference cannot be resolved or does not contain a
coherent pre-Stack fixture, mark that scenario `blocked` with evidence; do not
replace it with invented content.

## Workflow per scenario

1. Select the latest stable published release and record the release-selection
   evidence once, before either scenario. If no stable release is unambiguous,
   explain the ambiguity and use the most defensible published version.
2. Capture the scenario's clean starting state and pre-migration build evidence
   where its original build entry point is available.
3. Apply the inspection, preservation, minimal-migration, evidence-log, build
   validation, guardrail, and product-experience procedures from
   `sphinx-stack-migration-validation`.
4. After a successful adopted build, run all bounded cases from
   `sphinx-stack-build-fuzzing`. Restore and confirm the clean adopted build
   after every case.
5. Record the scenario result, then restore the repository to its clean
   pre-test state before starting the next scenario. Never commit or push.

After both scenarios, verify that only `agentic-test-report.md` may remain as a
test result. If restoration cannot be verified with available tools, say so
without claiming it succeeded.

## Deliverables

Apply the success criteria in `sphinx-stack-migration-validation`. Use
`sphinx-stack-test-report` to write `agentic-test-report.md` with contract
`sphinx-stack-adoption-report-v1`, including one scenario row per required
scenario, one fuzz row per required case and scenario, prioritized findings,
and exact repository-state disclosure. Return that same concise report as the
final response.
