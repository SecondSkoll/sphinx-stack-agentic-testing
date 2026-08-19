# Adopt the latest Canonical Sphinx Stack release

Adopt the latest stable published version of Canonical's Sphinx Stack
(https://github.com/canonical/sphinx-stack) for the documentation in this
repository. Perform the adoption rather than only describing how it could be
done, and critically evaluate the experience from the perspective of a
relatively inexperienced developer.

## Required skills

Before selecting a release or modifying files, load and follow these skills
with the skill tool:

1. `sphinx-stack-release-selection`, using **latest** selection mode.
2. `sphinx-stack-migration-validation`, using the direct-adoption workflow.

If either skill is unavailable, stop before modifying the repository and
report the configuration blocker. This prompt supplies the workflow-specific
requirements and deliverables; follow it where it is more specific.

## Workflow

1. Select the latest stable published release and record the release-selection
   evidence required by `sphinx-stack-release-selection`. If no stable release
   is unambiguous, explain the ambiguity and use the most defensible published
   version.
2. Apply the inspection, preservation, minimal-migration, evidence-log, build
   validation, guardrail, and product-experience procedures from
   `sphinx-stack-migration-validation`.
3. Make the adoption changes directly in this repository and revert it afterwards.

## Deliverables

Make the adoption changes directly in this repository. Then provide a concise
report containing:

1. **Adopted release** — exact release/tag/commit, source URL, and why it
	qualifies as the latest stable version.
2. **Changes made** — files added, moved, or modified and the purpose of each
	material change; explicitly note any existing behavior that could not be
	preserved.
3. **Validation** — commands attempted, their outcomes, relevant diagnostics,
	and which output was actually inspected or verified.
4. **Adoption log** — the important expected-versus-observed steps and all
	workarounds.
5. **Findings** — prioritized as `blocker`, `high`, `medium`, or `low`. For each
	finding, state:
	- the affected adoption step;
	- the concrete evidence and source;
	- expected behavior versus observed behavior;
	- likely impact on a new adopter;
	- whether it is a Stack issue, repository-specific issue, or environment
	  limitation;
	- a specific recommended improvement and likely owner.
6. **Outcome** — `successful`, `partially successful`, or `blocked`, with a
	brief justification and any unresolved risks.

Apply the success criteria defined by `sphinx-stack-migration-validation`.
