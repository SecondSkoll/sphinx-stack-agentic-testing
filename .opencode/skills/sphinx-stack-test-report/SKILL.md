---
name: sphinx-stack-test-report
description: Produce a concise, versioned, machine-checkable Markdown report for multi-scenario Sphinx Stack adoption and upgrade tests.
license: MIT
compatibility: opencode
metadata:
  audience: test-maintainers
  workflow: reporting
---

# Write the agentic test report

Write the final report to `agentic-test-report.md`, replacing any report from a
previous run. The report is the durable result; keep raw narration and long
logs out of it. Use exactly this structure and heading order:

```text
# Sphinx Stack <adoption|upgrade> test

- **Contract:** sphinx-stack-<adoption|upgrade>-report-v1
- **Overall outcome:** successful | partially successful | blocked
- **Release(s):** exact tag(s) and commit(s)
- **Scenarios:** N passed / N run

## Release evidence
## Scenario results
## Fuzz results
## Findings
## Repository state
```

Use these exact table columns:

- Scenario results: `Scenario | Input | Input commit | Baseline | Migration |
  Final build | Output verified | Outcome`
- Fuzz results: `Scenario | Case | Mutation | Initial diagnostic | Attempts |
  Final result | Usability`
- Findings: `Severity | Scenario / step | Evidence | Impact | Recommendation |
  Owner`

Rules:

- Use scenario IDs `local-rst` and `reference-generic-agentic-workflows`.
- Use only `successful`, `partially successful`, or `blocked` for scenario and
  overall outcomes; the worst scenario determines the overall outcome.
- Deduplicate findings, include at most ten, and sort them `blocker`, `high`,
  `medium`, then `low`.
- Keep evidence concrete: command plus result, file/setting, URL, or short
  diagnostic. Link or summarize long evidence rather than embedding it.
- In Repository state, state what was restored or retained, whether the
  reference remained read-only, and unresolved risks. Use `None` explicitly
  when there are none.
- Keep the report concise: no command transcript, no repeated narrative, and
  no section other than the six required headings.

After writing the file, return the same Markdown as the final response.