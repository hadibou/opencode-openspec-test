# Design

## Context

See `proposal.md` - Why. The working tree contains only `openspec/` and `.opencode/` scaffolding: there is no `docs/` directory, no application source, and no `scripts/test-md.sh` even though `.opencode/pipeline.json` configures that script as the test command. The documentation therefore has to describe the intended test setup from the configuration while remaining honest about the parts that are not present in the repository. Project constraints are a documentation-only deliverable, a single H1 per file, clear H2 sections, and issue/project-board tracking.

## Goals / Non-Goals

**Goals:**

- Produce two documents with non-overlapping roles: `docs/README.md` for onboarding and day-to-day commands, `docs/architecture.md` for structure and flow.
- Quote the configured test command verbatim and state the working directory.
- Make every cross-reference a repository-relative link that works on GitHub and locally.
- Keep claims about the test script limited to what the configuration and issue state.

**Non-Goals:**

- Creating or modifying `scripts/test-md.sh`, `.opencode/pipeline.json`, or any other tooling.
- Documenting the GitHub Project board's internal field values or status names.
- Adding application code, dependencies, or CI configuration.

## Decisions

1. **Two documents with distinct audiences.** `README.md` answers "what is this and how do I run it"; `architecture.md` answers "how is it put together and how does a change flow". Alternative: one large README. Rejected because the issue explicitly requests both files and a single file would blur onboarding from architecture.
2. **Treat `.opencode/pipeline.json` as the source of truth for the test command.** The README repeats the command and working directory instead of paraphrasing it, so the documented command cannot drift from configuration without an obvious mismatch. Alternative: describe tests abstractly. Rejected because "detailing test setup" requires concrete commands.
3. **Describe expected validation checks, not a specific script implementation.** The spec requires single H1, ordered heading levels, language-tagged fences, and resolvable relative links; the docs present these as the checks the test command is expected to enforce. This avoids inventing behavior for a script that is not in the tree.
4. **Use repository-relative links.** `README.md` links to `architecture.md` and vice versa, relative to `docs/`. Alternative: absolute GitHub URLs. Rejected because they break in forks and local checkouts.
5. **Record the missing test script as a prerequisite and an open question, not as work in this change.** Creating `scripts/test-md.sh` would violate the documentation-only deliverable constraint. The validation task runs the configured command and reports a blocker if the script is absent instead of silently substituting another check.
6. **Keep the board description generic.** The architecture document explains the issue -> OpenSpec change -> review flow without naming board columns that may change.

## Risks / Trade-offs

- **The configured test command cannot run because `scripts/test-md.sh` is absent** -> Documents list the script as a prerequisite; implementation reports the missing script as a blocker rather than creating it. The open question records the decision for the issue owner.
- **The real test script may enforce rules not described here** -> The docs describe the expected checks from the spec and avoid claiming implementation details; a later change can refine them.
- **Documentation may drift from configuration** -> Both documents point at `.opencode/pipeline.json` as the authoritative source for the test command.
- **Duplicated content between the two files** -> Each section owns one concern and links to the other file for detail.

## Migration Plan

Not applicable. This change adds two documentation files with no runtime, data, or deployment impact. Rollback is deleting `docs/README.md` and `docs/architecture.md`.

## Open Questions

- Should `scripts/test-md.sh` be added by this change or supplied by the pipeline harness? Planning keeps it out of scope; the documentation approach does not depend on the answer.
- Should the architecture document name the GitHub Project board number from `.opencode/pipeline.json`? Planning omits it to avoid stale board details.
