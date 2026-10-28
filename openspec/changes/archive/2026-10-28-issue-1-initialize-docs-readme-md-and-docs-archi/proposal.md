# Proposal

## Why

The repository currently contains only the OpenSpec and agent-workflow scaffolding. There is no human-readable entry point explaining what the project is, how its output is validated, or how changes flow from a GitHub issue to merged documentation. Issue #1 asks for an initial `docs/README.md` and `docs/architecture.md` that describe the test setup so contributors and automation agents can work from a shared, written baseline.

## What Changes

- Create `docs/README.md` as the project entry point. It documents the project purpose, prerequisites, repository layout, the exact test command, and how to run the OpenSpec workflow.
- Create `docs/architecture.md` describing the documentation-only system: its components (`docs/`, `openspec/`, `.opencode/`, `scripts/`), the Markdown validation test flow, and the issue-to-change workflow.
- Document the test command exactly as `./scripts/test-md.sh`, run from the repository root, and describe the checks that script performs.
- Cross-link the two documents with repository-relative Markdown links.
- Do not change source code, test code, or configuration. `scripts/test-md.sh` already exists on the default branch and is out of scope for this change; no runtime behavior changes.

## Capabilities

### New Capabilities

- `project-documentation`: the project's human-readable documentation, covering purpose, layout, test setup, and architecture, with valid Markdown structure and cross-references.

### Modified Capabilities

None.

## Impact

- **Files created:** `docs/README.md`, `docs/architecture.md`.
- **Files modified:** none.
- **Code/APIs/dependencies:** none.
- **Validation:** `./scripts/test-md.sh` run from the repository root, and `openspec validate issue-1-initialize-docs-readme-md-and-docs-archi --strict`.

## Assumptions

- Per `openspec/config.yaml`, the only deliverables for this project are Markdown files in `docs/`.
- `scripts/test-md.sh` already exists on the default branch and is out of scope for this change. This change documents it and does not create or modify it.
- The documented test command is exactly `./scripts/test-md.sh`, executed from the repository root. The Windows/Git Bash wrapper in `.opencode/pipeline.json` is environment-specific and is not copied into the documentation.
- The checks performed by the test script are: `docs/` exists; every `docs/*.md` is non-empty; every `docs/*.md` contains a top-level `#` header; `shellcheck` runs on `scripts/*.sh` when it is installed.
- `docs/README.md` is the primary entry point and `docs/architecture.md` holds the deeper structural description; neither duplicates the other.
- The audience is both human contributors and automation agents, so commands are written verbatim and paths are repository-relative.
- Repository-relative links (for example, `architecture.md` from `README.md`) are the expected cross-reference style.
- The GitHub Project board is described generically, without naming its project number or status values, so the documentation does not go stale when the board changes.

## Open questions

None. The owner resolved the earlier questions about the test script, its checks, the board description, and the exact test command.
