# Upgrade between the two latest Canonical Sphinx Stack releases

Evaluate the released upgrade path for Canonical's Sphinx Stack
(https://github.com/canonical/sphinx-stack) in each scenario below. First adopt
the stable release immediately preceding the latest stable release and
validate it as a working baseline. Then upgrade the same documentation in
place to the latest stable release, run controlled build fuzzing, and
critically evaluate the experience from the perspective of a relatively
inexperienced developer.

## Required skills

Before selecting releases or modifying files, load and follow these skills
with the skill tool:

1. `sphinx-stack-release-selection`, using **consecutive pair** selection mode.
2. `sphinx-stack-migration-validation`, using the two-stage upgrade workflow.
3. `sphinx-stack-build-fuzzing`.
4. `sphinx-stack-test-report`, using the upgrade report contract.

If any skill is unavailable, stop before modifying the repository and
report the configuration blocker. This prompt supplies the workflow-specific
requirements and deliverables; follow it where it is more specific.

## Scenario matrix

Run both scenarios independently against the same selected release pair:

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

1. Select the two latest consecutive stable releases and record the evidence,
   version-specific material, and exact-transition guidance required by
	`sphinx-stack-release-selection` once, before either scenario. If no valid
	previous release exists, stop without modifying the repository. Explain any
	ordering or stability ambiguity and otherwise use the most defensible pair.
2. Capture the scenario's clean starting state and pre-migration build evidence
	where its original build entry point is available. Apply the inspection and
	preservation procedures from
   `sphinx-stack-migration-validation`.
3. Adopt and validate the older release as a realistic baseline using material
   belonging to that release. Preserve the required conceptual checkpoint.
4. Before further edits, determine the expected migration steps and then
   upgrade that baseline in place to the latest release.
5. Validate and compare the latest-release state with the baseline. Check
   whether the release notes and upgrade instructions agree with the actual
   required changes, including steps that are redundant, out of order,
   impossible, or dependent on unstated repository structure.
6. After a successful latest-release build, run all bounded cases from
   `sphinx-stack-build-fuzzing`. Restore and confirm the clean latest-release
   build after every case.
7. Record the scenario result, then restore the repository to its clean
   pre-test state before starting the next scenario. Never commit or push.

After both scenarios, verify that only `agentic-test-report.md` may remain as a
test result. If restoration cannot be verified with available tools, say so
without claiming it succeeded.

## Deliverables

Apply the success criteria defined by `sphinx-stack-migration-validation`,
including the requirement for a valid older-release baseline. Use
`sphinx-stack-test-report` to write `agentic-test-report.md` with contract
`sphinx-stack-upgrade-report-v1`, including one scenario row per required
scenario, one fuzz row per required case and scenario, prioritized findings,
and exact repository-state disclosure. Return that same concise report as the
final response.
