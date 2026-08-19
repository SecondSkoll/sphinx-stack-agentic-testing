---
name: sphinx-stack-build-fuzzing
description: Run bounded deterministic Sphinx configuration fuzz cases, repair each failure, and evaluate diagnostic and correction usability.
license: MIT
compatibility: opencode
metadata:
  audience: documentation-adopters
  workflow: build-fuzzing
---

# Fuzz Sphinx builds and evaluate recovery

Run this only after the scenario has a successful migrated build. Before
fuzzing, create a fixture-local byte-for-byte backup of every configuration
file that may be changed. Restore from that backup and compare the restored
file after every case. Change one value per case; do not delete documentation,
relax warning policies, or make unrelated changes.

All mutations, backups, builds, and repairs must remain under the current
`.agentic-work/<scenario>/` directory. Never fuzz an original repository input
or a configured reference directory.

## Required deterministic cases

Run these four cases in order, adapted to the actual configuration keys used by
the selected Stack release:

| ID | Mutation | Expected result |
|---|---|---|
| `valid-unicode-metadata` | Set the project title to `Fuzz café 🚀 — "docs"` | Build succeeds and the value remains represented in output. |
| `wrong-option-type` | Change one list-valued path or pattern option to a string | Build fails or warns with a useful configuration diagnostic. |
| `missing-static-path` | Add a clearly nonexistent static directory | Build fails or warns and identifies the missing path or setting. |
| `unknown-extension` | Add `sphinx_stack_testing.nonexistent` to extensions | Build fails and identifies the import/configuration problem. |

If a case is inapplicable, mark it `not-applicable` with the exact reason; do
not silently substitute an easier case.

## Procedure per case

1. Confirm the clean scenario build succeeded.
2. Apply exactly one mutation and record the exact file, setting, old value,
   and new value.
3. Run the normal Stack build once. Record exit status and the smallest useful
   diagnostic excerpt.
4. Judge whether the diagnostic identifies the file or setting, bad value,
   accepted form, and a next action.
5. Attempt at most two corrections, using official documentation if the
   diagnostic alone is insufficient. Record every attempt and source used.
6. Restore the exact clean configuration and rebuild successfully before the
   next case. A repair that merely removes unrelated content is invalid.

Rate correction usability as one of:

- `clear`: the diagnostic directly enables the correction;
- `discoverable`: one official-documentation lookup is needed;
- `difficult`: multiple lookups or substantial inference is needed;
- `misleading`: the diagnostic points toward an incorrect correction;
- `not-recoverable`: two bounded attempts do not restore a clean build;
- `not-applicable`: the case cannot coherently target this release.

The intentionally failing build is not itself a test failure. Failure to
restore the original configuration and clean build is a scenario failure.