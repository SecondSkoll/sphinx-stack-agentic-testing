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

1. Select the latest stable published release and record the release-selection
   evidence once, before either scenario. If no stable release is unambiguous,
   explain the ambiguity and use the most defensible published version.
2. Create the scenario from its read-only inputs. Capture pre-migration build
   evidence where an original build entry point exists; for a Markdown-only
   source corpus, record that no original Sphinx build was defined and proceed
   to construct the standalone fixture.
3. Apply the inspection, preservation, minimal-migration, evidence-log, build
   validation, guardrail, and product-experience procedures from
   `sphinx-stack-migration-validation`.
4. After a successful adopted build, run all bounded cases from
   `sphinx-stack-build-fuzzing`. Restore and confirm the clean adopted build
   after every case.
5. Record the scenario result, remove its complete disposable directory, and
   verify original inputs remain unchanged before starting the next scenario.

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
