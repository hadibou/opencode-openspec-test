# Proposal

## Why

The repository currently contains only the OpenSpec and agent-workflow scaffolding. There is no human-readable entry point explaining what the project is, how its output is validated, or how changes flow from a GitHub issue to merged documentation. Issue #1 asks for an initial `docs/README.md` and `docs/architecture.md` that describe the test setup so contributors and automation agents can work from a shared, written baseline.

## What Changes

- Create `docs/README.md` as the project entry point. It documents the project purpose, prerequisites, repository layout, the exact test command, and how to run the OpenSpec workflow.
- Create `docs/architecture.md` describing the documentation-only system: its components (`docs/`, `openspec/`, `.opencode/`, `scripts/`), the Markdown validation test flow, and the issue-to-change workflow.
- Cross-link the two documents with repository-relative Markdown links.
- Do not change source code, test code, or configuration. No runtime behavior changes.

## Capabilities

### New Capabilities

- `project-documentation`: the project's human-readable documentation, covering purpose, layout, test setup, and architecture, with valid Markdown structure and cross-references.

### Modified Capabilities

None.

## Impact

- **Files created:** `docs/README.md`, `docs/architecture.md`.
- **Files modified:** none.
- **Code/APIs/dependencies:** none.
- **Validation:** the configured Markdown test command from `.opencode/pipeline.json` (`'C:\Program Files\Git\bin\bash.exe' ./scripts/test-md.sh`) and `openspec validate` for this change.

## Assumptions

- Per `openspec/config.yaml`, the only deliverables for this project are Markdown files in `docs/`.
- The project's test setup is the command configured in `.opencode/pipeline.json`, run from the repository root.
- `docs/README.md` is the primary entry point and `docs/architecture.md` holds the deeper structural description; neither duplicates the other.
- The audience is both human contributors and automation agents, so commands are written verbatim and paths are repository-relative.
- Repository-relative links (for example, `architecture.md` from `README.md`) are the expected cross-reference style.
- `scripts/test-md.sh` is expected to be supplied by the pipeline/harness; this change only documents it and does not create it.

## Open questions

- `scripts/test-md.sh` referenced by `.opencode/pipeline.json` is not present in the repository. Should this change add it, or will it be provided outside this repository? Planning assumes it is out of scope.
- The exact Markdown rules enforced by `scripts/test-md.sh` are unknown. The documents describe the expected checks (single H1, ordered H2 sections, valid relative links) rather than claiming a specific implementation.
- Should the documentation name the GitHub Project board number (`4` from `.opencode/pipeline.json`) and board statuses explicitly? Planning assumes a generic description of the issue-to-change workflow to avoid stale board details.
