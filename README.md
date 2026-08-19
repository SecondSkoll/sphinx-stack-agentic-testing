# sphinx-stack-agentic-testing

A repository that tests adoption and upgrade pathways of Canonical's Sphinx Stack.

This repository contains a minimal vanilla Sphinx deployment of test documenation for use by AI agents in assessing releases of the main Sphinx Stack.

## Local usage

This repository contains a workshop file that provides two main actions, `adoption-test` and `upgrade-test`. These tests use an agent to analyse initial
adoption and upgrade functionality of Canonical's Sphinx Stack. To run these actions you need the following:

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

Workflows use [generic agentic workflows](https://github.com/SecondSkoll/generic-agentic-workflows) which use strict security boundaries to prevent possible abuse by AI agents.

Configuration of prompts / agents / skills are contained in the [generic agentic workflows config](https://github.com/SecondSkoll/generic-agentic-workflows-config) repo, or defaults provided by the main workflow repository.
