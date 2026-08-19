# sphinx-stack-agentic-testing

A repository that tests adoption and upgrade pathways of Canonical's Sphinx Stack.

This repository contains a minimal vanilla Sphinx deployment of test documentation for use by AI agents in assessing releases of the main Sphinx Stack.

## Local usage

This repository contains a workshop file that provides two main actions,
`adoption-test` and `upgrade-test`. Each action runs two independent scenarios:

* the local standalone reStructuredText fixture;
* the real-world documentation fixture from the OpenCode
	`generic-agentic-workflows` reference.

Both scenarios migrate and build the documentation, run bounded configuration
fuzz cases, evaluate recovery usability, and restore the starting state. The
agent writes the concise result to `agentic-test-report.md`.

To run these actions you need the following:

* Workshop installed on your system.
* An OpenRouter key in plaintext, `.key` is currently ignored and will not be committed to the repository.

WARNING: Do not commit keys to repositories.

With the requirements met, you can run:

```
workshop run -- adoption-test
```

Or:

```
workshop run -- upgrade-test
```

## Workflows

The adoption and upgrade workflows run the local OpenCode agent, prompts, and
skills under `.opencode/`. GitHub issues contain only the validated concise
report; the complete OpenCode transcript is retained as a workflow artifact.
The workflow fails for an invalid report, a failed process, or a semantically
`blocked` result.

The separate Sphinx Stack setup review uses
[generic agentic workflows](https://github.com/SecondSkoll/generic-agentic-workflows)
with the read-only bundle under `.opencode/configuration/sphinx-stack-setup/`.
That review is distinct from the mutable adoption and upgrade tests, although
the latter also use the repository as a read-only real-world fixture.
