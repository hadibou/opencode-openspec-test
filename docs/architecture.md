# Architecture

This document describes the structure and workflow of this documentation-only test project. For setup and day-to-day commands, see [README.md](README.md).

## Purpose

The project validates multi-agent execution and Git worktree automation. Its only deliverables are Markdown files in `docs/`. The `openspec/` and `.opencode/` directories are tooling that supports planning and execution; they are not project deliverables. There is no application code, runtime, or deployment step.

## Components

### docs/

The `docs/` directory holds the project deliverables. Every Markdown file here is part of the documentation set and is checked by the test script. New documentation content belongs in this directory.

### openspec/

The `openspec/` directory contains the OpenSpec configuration in `openspec/config.yaml`, the main specifications under `openspec/specs/`, and one directory per active change under `openspec/changes/`. Each change directory contains its proposal, design, specification deltas, and task list. This directory drives the planning workflow; it does not ship as a deliverable.

### .opencode/

The `.opencode/` directory holds the agent-facing tooling: skills, custom commands, and the pipeline configuration that wires issues, worktrees, and agents together. It supports how work is executed and is not a deliverable.

### scripts/

The `scripts/` directory contains validation tooling. The primary script, `scripts/test-md.sh`, verifies the Markdown documentation and optionally lints the shell scripts. The script already exists on the default branch and is out of scope for this change; the documentation only describes it.

## Test Architecture

The documentation test command is run from the repository root:

```bash
./scripts/test-md.sh
```

The script performs these checks:

- When ShellCheck is installed, it runs `shellcheck` against `scripts/*.sh`.
- It verifies that the `docs/` directory exists.
- It verifies that every `docs/*.md` file is non-empty.
- It verifies that every `docs/*.md` file contains a top-level `#` header.
- It exits with a non-zero status when a check fails, and with status 0 when every check passes.

ShellCheck is optional, so its lint step only runs on machines where the tool is available. The Markdown checks always run. The script itself already exists on the default branch and is out of scope for this change.

A change is considered validated when `./scripts/test-md.sh` succeeds and `openspec validate <change-name> --strict` reports no problems.

## Change Workflow

Work begins as a GitHub issue. The issue is turned into an OpenSpec change with planning artifacts: a proposal explaining why the change is needed, a design recording decisions and trade-offs, specification deltas describing required behavior, and a task list. Implementation then updates the Markdown deliverables in `docs/` and ticks off tasks as they are completed.

Before a change is finished, validation runs the project test command and the strict OpenSpec validation. The completed work is reviewed, merged, and the change is archived into the main specifications.

GitHub issues and the GitHub Project board track the progress of each item generically. The board provides a visual overview of where an item stands, while the issue and the OpenSpec change directory hold the authoritative detail. The documentation deliberately avoids naming the board project number or its column names so that this file does not go stale when the board is reconfigured.
