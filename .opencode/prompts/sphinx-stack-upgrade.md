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
| `reference-generic-agentic-workflows` | Markdown documentation and related assets exposed by the OpenCode `generic-agentic-workflows` reference | Standalone Sphinx Stack fixture generated from a real-world Markdown source corpus |

Treat the configured reference directory and cache as read-only. Record its
resolved commit and identify the relevant Markdown documentation and assets. A
reference is valid input even when it has no Sphinx configuration, Makefile,
dependency declaration, or explicit Sphinx navigation.

Copy the relevant source corpus into the reference scenario directory while
preserving its relative layout and source content. Create clearly test-owned
standalone Sphinx and Sphinx Stack scaffolding around it, including the
configuration, build entry point, dependencies, source mapping, Markdown
parser, and navigation adapter needed for a coherent build. A generated index
or toctree must be derived deterministically from the copied files.

Generating fixture scaffolding and release-required support files is not
inventing documentation. Do not replace, rewrite, or fabricate the referenced
content. Adapt embedding-specific links or navigation only when required for a
standalone build, keep changes minimal, and record the delta. Mark this
scenario `blocked` only if the reference cannot be resolved, has no usable
documentation source, or cannot build after bounded fixture-local adaptation.
The absence of an existing Sphinx project is not a blocker.

## Fixture workspace

Perform both scenarios in disposable, independent directories:

- `.agentic-work/local-rst/`
- `.agentic-work/reference-generic-agentic-workflows/`

Treat this repository's original `source/`, root `Makefile`, and configured
reference paths as read-only inputs. Copy the local source and build files into
the local scenario before testing. Other than `agentic-test-report.md`, do not
write outside `.agentic-work/`. Install dependencies only in scenario-local
virtual environments. Never commit, push, tag, mutate a Git remote, or edit a
reference cache.

## Workflow per scenario

1. Select the two latest consecutive stable releases and record the evidence,
   version-specific material, and exact-transition guidance required by
	`sphinx-stack-release-selection` once, before either scenario. If no valid
	previous release exists, stop without modifying the repository. Explain any
	ordering or stability ambiguity and otherwise use the most defensible pair.
2. Create the scenario from its read-only inputs. Capture pre-migration build
	evidence where an original build entry point exists; for a Markdown-only
	source corpus, record that no original Sphinx build was defined and proceed
	to construct the older-release standalone fixture. Apply the inspection and
	preservation procedures from
   `sphinx-stack-migration-validation`.
3. Adopt and validate the older release as a realistic baseline using material
   belonging to that release. For a source corpus, this constructed fixture is
   the required baseline. Create minimal fixture-owned support files required
   by that release and record them; missing original Sphinx configuration is
   not a baseline failure. Preserve the required conceptual checkpoint.
4. Before further edits, determine the expected migration steps and then
   upgrade that baseline in place to the latest release.
5. Validate and compare the latest-release state with the baseline. Check
   whether the release notes and upgrade instructions agree with the actual
   required changes, including steps that are redundant, out of order,
   impossible, or dependent on unstated repository structure.
6. After a successful latest-release build, run all bounded cases from
   `sphinx-stack-build-fuzzing`. Restore and confirm the clean latest-release
   build after every case.
7. Record the scenario result, remove its complete disposable directory, and
   verify original inputs remain unchanged before starting the next scenario.

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
