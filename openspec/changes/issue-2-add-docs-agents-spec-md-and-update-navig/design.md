# Design

## Context

See `proposal.md` - Why. The repository is documentation-only. `openspec/config.yaml` defines the deliverables as Markdown in `docs/`, and `docs/README.md` plus `docs/architecture.md` already exist on the default branch. The default branch also contains `scripts/test-md.sh`, which checks that `docs/` exists, that every `docs/*.md` is non-empty and has a top-level `#` header, and optionally lints shell scripts. The existing main specification `project-documentation` already fixes the README structure and the Markdown quality rules, so this change extends that capability rather than introducing a new one.

The reusable facts for the new document come from what the pipeline actually does: an issue becomes an OpenSpec change, the change's tasks are implemented in an isolated worktree on an issue-specific branch, integration commits and opens a pull request, review audits the result against the approved change, and validation runs the project test command plus strict OpenSpec validation before merge and archive. The repository does not document agent roles today.

## Goals / Non-Goals

**Goals:**

- Give the documentation set one place that explains the roles in the pipeline, what each consumes and produces, and where its authority ends.
- Define handoffs by persistent artifacts so readers and agents can verify a handoff without replaying a conversation.
- Make the new document reachable from `docs/README.md` without disturbing the existing README structure.
- Keep the document stable across harness changes by describing responsibilities instead of configuration.

**Non-Goals:**

- Editing `docs/architecture.md`. It keeps ownership of components and change flow; the new document links to it.
- Documenting tool permissions, model selection, or provider configuration.
- Recording the GitHub Project number, status names, or credentials.
- Describing detailed failure handling or recovery procedures; the new file only states that a blocked role stops and reports.
- Changing `scripts/test-md.sh`, `.opencode/`, or `openspec/config.yaml`.

## Decisions

1. **A separate document instead of a new section in `architecture.md`.** The issue names `docs/agents-spec.md`, and roles plus handoffs are a different concern from structure and test setup. Alternative: extend `architecture.md`. Rejected because it would make one file answer two audiences and would collide with the planned navigation work in the architecture document.
2. **Describe role contracts, not agents as configured.** Each role subsection states inputs, outputs, and the authority boundary (for example, the planning role does not implement, and the review role does not plan). Alternative: mirror harness configuration, including model or provider names. Rejected because configuration changes frequently and would make the document stale on every harness edit.
3. **Five roles: planning, implementation, integration, review, validation.** These cover the phases the repository already exercises, in the order a change passes through them. Alternative: a finer split, such as separate branch creation and commit roles. Rejected because a reader wants the responsibility boundaries, and finer splits map to tool steps that are already documented by the workflow commands.
4. **Handoffs are listed as artifacts, not messages.** Each transition names the artifact that carries work forward: the GitHub issue and OpenSpec change, the issue-specific branch and worktree, commits and the pull request, review comments, and validation output, then the archived change. Alternative: describe handoffs as "the agent reports to the next agent". Rejected because conversation state is not durable and cannot be reviewed.
5. **Navigation as a dedicated README section plus a workflow link.** The README gains an H2 "Documentation Set" listing every `docs/*.md` file, and the existing OpenSpec workflow section gains one sentence linking to the agent specification. Alternative: add a single row to the repository layout table. Rejected because that table lists directories, and a per-file index keeps the documentation set discoverable as it grows.
6. **Additive README edit only.** The single H1 and all existing H2 sections are preserved so the existing specification for the README keeps holding. Alternative: restructure the README around the new document. Rejected because the issue asks only for navigation, and restructuring would enlarge the review surface.
7. **Present-tense, descriptive prose in the new document.** The agent specification describes what happens in each role rather than instructing a particular human reader, so it works for both contributors and automation. Alternative: write an operating manual with imperative steps. Rejected because it would duplicate the workflow commands and drift.

## Risks / Trade-offs

- **Documentation drifts from the pipeline** -> Roles are described by responsibility and handoff artifacts, with no model, provider, or path values that change often.
- **Overlap with `architecture.md`** -> Ownership is explicit: architecture covers components, test setup, and flow; the agent specification covers who acts, with what inputs and outputs, and where responsibility stops.
- **Navigation goes stale as `docs/` grows** -> The new "Documentation Set" section is a simple list of files, so adding a file is a one-line edit, and the section is called out in the README requirement.
- **A reader mistakes the document for a normative contract** -> The proposal records this as an open question; the document states responsibilities, and no tooling validates agreement with it.
- **Empty issue body leaves scope ambiguous** -> The file set and acceptance criteria come from the issue title; the proposal records assumptions and open questions so review can correct them before implementation.

## Migration Plan

Not applicable. The change adds one Markdown file and edits another. Rollback deletes `docs/agents-spec.md` and reverts `docs/README.md` to its previous state; no runtime, data, or deployment impact.

## Open Questions

See `proposal.md` - Open questions. They concern whether the document should be normative, whether agents should be named individually, and who the audience is. None of them changes the file set, the specification, or the task breakdown.
