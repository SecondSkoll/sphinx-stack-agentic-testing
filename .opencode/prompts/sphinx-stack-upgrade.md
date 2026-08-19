# Upgrade between the two latest Canonical Sphinx Stack releases

Evaluate the released upgrade path for Canonical's Sphinx Stack
(https://github.com/canonical/sphinx-stack). First adopt the stable release
immediately preceding the latest stable release for the documentation in this
repository. Establish and validate that older release as a working baseline.
Then upgrade the same documentation to the latest stable release by following
the official upgrade guidance. Perform both stages rather than only describing
them, and critically evaluate the upgrade experience from the perspective of a
relatively inexperienced developer.

## Required skills

Before selecting releases or modifying files, load and follow these skills
with the skill tool:

1. `sphinx-stack-release-selection`, using **consecutive pair** selection mode.
2. `sphinx-stack-migration-validation`, using the two-stage upgrade workflow.

If either skill is unavailable, stop before modifying the repository and
report the configuration blocker. This prompt supplies the workflow-specific
requirements and deliverables; follow it where it is more specific.

## Workflow

1. Select the two latest consecutive stable releases and record the evidence,
   version-specific material, and exact-transition guidance required by
   `sphinx-stack-release-selection`. If no valid previous release exists, stop
   without modifying the repository. Explain any ordering or stability
   ambiguity and otherwise use the most defensible consecutive pair.
2. Apply the inspection and preservation procedures from
   `sphinx-stack-migration-validation`.
3. Adopt and validate the older release as a realistic baseline using material
   belonging to that release. Preserve the required conceptual checkpoint.
4. Before further edits, determine the expected migration steps and then
   upgrade that baseline in place to the latest release.
5. Validate and compare the latest-release state with the baseline. Check
   whether the release notes and upgrade instructions agree with the actual
   required changes, including steps that are redundant, out of order,
   impossible, or dependent on unstated repository structure.
6. Revert all changes to the repository afterwards.

## Deliverables

Leave the repository in the latest-release state if the upgrade succeeds. If it
does not, leave the most coherent diagnosable state possible and clearly state
which release that state represents. Then provide a concise report containing:

1. **Release pair** — exact older and latest release/tag/commit, source URLs,
	release ordering, stability evidence, and any selection ambiguity.
2. **Older baseline** — material changes made to adopt the previous release,
	preserved repository behavior, baseline build result, and verified output.
3. **Expected upgrade path** — the official migration guidance found, its
	applicability to this exact release pair, and the required steps identified
	before the upgrade.
4. **Upgrade changes** — files and settings added, removed, moved, or modified
	relative to the older baseline, with the purpose of each material change;
	explicitly identify undocumented changes and behavior that could not be
	preserved.
5. **Validation comparison** — baseline and post-upgrade commands, outcomes,
	relevant diagnostics, and which output was actually inspected or verified.
6. **Upgrade log** — important expected-versus-observed steps and every
	workaround, clearly separated from initial baseline-adoption friction.
7. **Findings** — prioritize upgrade findings as `blocker`, `high`, `medium`,
	or `low`. For each finding, state:
	- the affected release and migration step;
	- the concrete evidence and source;
	- expected behavior versus observed behavior;
	- likely impact on an existing adopter;
	- whether it is a Stack upgrade issue, baseline-adoption issue,
	  repository-specific issue, or environment limitation;
	- a specific recommended improvement and likely owner.
8. **Outcome** — `successful`, `partially successful`, or `blocked`, with a
	brief justification, the release represented by the final repository state,
	and unresolved compatibility, maintenance, or rollback risks.

Apply the success criteria defined by `sphinx-stack-migration-validation`,
including the requirement for a valid older-release baseline.
