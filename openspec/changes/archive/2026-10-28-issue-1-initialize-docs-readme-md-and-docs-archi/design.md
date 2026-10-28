# Design

## Context

See `proposal.md` - Why. The repository is a documentation-only test project: `openspec/config.yaml` states that the deliverables are Markdown files in `docs/`, while `openspec/`, `.opencode/`, and `scripts/` are supporting tooling. The default branch already contains `scripts/test-md.sh`, which validates the documentation and is out of scope for this change. There is no `docs/` directory yet, so the two documents must establish the human-readable entry point. Project constraints are a documentation-only deliverable, a single H1 per file, clear H2 sections, and issue/project-board tracking.

## Goals / Non-Goals

**Goals:**

- Produce two documents with non-overlapping roles: `docs/README.md` for onboarding and day-to-day commands, `docs/architecture.md` for structure and flow.
- Document the test command exactly as `./scripts/test-md.sh`, run from the repository root.
- Describe precisely what `scripts/test-md.sh` checks, based on the script in the repository.
- Make every cross-reference a repository-relative link that works on GitHub and locally.
- Describe issue and project-board tracking generically, without project numbers or status names.

**Non-Goals:**

- Creating or modifying `scripts/test-md.sh`, `.opencode/pipeline.json`, or any other tooling.
- Copying the Windows/Git Bash wrapper from `.opencode/pipeline.json` into the documentation.
- Naming the GitHub Project board number or its status values.
- Adding application code, dependencies, or CI configuration.

## Decisions

1. **Two documents with distinct audiences.** `README.md` answers "what is this and how do I run it"; `architecture.md` answers "how is it put together and how does a change flow". Alternative: one large README. Rejected because the issue explicitly requests both files and a single file would blur onboarding from architecture.
2. **Document the portable test command, not the pipeline wrapper.** The test command is written exactly as `./scripts/test-md.sh` and the working directory is stated as the repository root. Alternative: copy the Windows/Git Bash wrapper from `.opencode/pipeline.json`. Rejected because that wrapper is a Windows-specific harness detail and does not belong in contributor documentation.
3. **Describe the checks that the script actually performs.** The documents state: `docs/` must exist; every `docs/*.md` must be non-empty; every `docs/*.md` must contain a top-level `#` header; `shellcheck` runs on `scripts/*.sh` when it is installed. Alternative: document generic "Markdown validation" without specifics. Rejected because the issue asks for the test setup to be detailed precisely and the script is now available as the source of truth.
4. **Use repository-relative links.** `README.md` links to `architecture.md` and vice versa, relative to `docs/`. Alternative: absolute GitHub URLs. Rejected because they break in forks and local checkouts.
5. **Treat `scripts/test-md.sh` as out of scope.** The script exists on the default branch; this change only documents it. Alternative: recreate or adjust the script here. Rejected because the owner explicitly placed it out of scope and the change is documentation-only.
6. **Keep the board description generic.** The architecture document explains the issue -> OpenSpec change -> review flow without naming the board's project number or status values.

## Risks / Trade-offs

- **The test script may evolve and its checks drift from the docs** -> The docs describe the script as it exists today; a later documentation change can update the list when the script changes.
- **Documentation may drift from configuration** -> The documents use the portable command `./scripts/test-md.sh` and do not depend on harness-specific wrappers.
- **`shellcheck` is optional, so local results can vary** -> The docs state that shellcheck runs only when installed; the Markdown checks always run.
- **Duplicated content between the two files** -> Each section owns one concern and links to the other file for detail.

## Migration Plan

Not applicable. This change adds two documentation files with no runtime, data, or deployment impact. Rollback is deleting `docs/README.md` and `docs/architecture.md`.

## Open Questions

None. The owner resolved the questions about test-script scope, the checks to document, the board description, and the exact test command.
