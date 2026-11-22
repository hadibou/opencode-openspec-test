# Documentation

This repository is a test project for validating multi-agent execution and Git worktree automation. Its deliverables are Markdown files in `docs/`; the rest of the repository is supporting tooling. See [architecture.md](architecture.md) for how the pieces fit together and how a change flows from issue to merge.

## Overview

The project exists to exercise an OpenSpec-based workflow with GitHub issues, Git worktrees, and automated agents. The documentation in `docs/` is the only thing the project produces. Each documentation change starts as an issue, is planned as an OpenSpec change, implemented, validated, reviewed, and then archived.

## Prerequisites

- Git, including the ability to create and use worktrees.
- A Bash-compatible shell. On Windows, Git Bash is sufficient.
- The OpenSpec CLI, used to validate and archive changes.
- ShellCheck is optional. When it is installed, the documentation test script also lints the shell scripts.

No application runtime, package manager, or build step is required.

## Repository Layout

| Path | Purpose |
| --- | --- |
| `docs/` | The project deliverables: human-readable Markdown documentation. |
| `openspec/` | OpenSpec configuration, main specs, and per-change planning artifacts. |
| `.opencode/` | Agent skills, commands, and pipeline configuration. |
| `scripts/` | Test and validation scripts, including `scripts/test-md.sh`. |

## Running the Tests

Run the documentation test from the repository root:

```bash
./scripts/test-md.sh
```

The command exits with status 0 when the documentation checks pass. It confirms that `docs/` exists, that every `docs/*.md` file is non-empty and has a top-level `#` header, and, when ShellCheck is installed, lints `scripts/*.sh`. The [architecture document](architecture.md) describes the validation flow in more detail.

## Documentation Set

Every file below is part of the documentation set and is checked by the test script.

| File | Purpose |
| --- | --- |
| [README.md](README.md) | The entry point: project purpose, prerequisites, repository layout, and how to run the tests. |
| [architecture.md](architecture.md) | Repository structure, test architecture, and how a change flows from issue to merge. |
| [agents-spec.md](agents-spec.md) | The pipeline roles, what each consumes and produces, and the artifacts that carry handoffs. |

## OpenSpec Workflow

Work is tracked in GitHub issues. For each issue, an OpenSpec change is created under `openspec/changes/` with a proposal, design, specification deltas, and a task list. The implementation updates the Markdown deliverables in `docs/`, after which the change is validated with the project test command and `openspec validate --strict`, reviewed, merged, and archived. The [architecture document](architecture.md) explains the change workflow and how progress is tracked. The [agent specification](agents-spec.md) describes the roles that carry out this workflow, the artifacts they exchange, and where each role's authority ends.
