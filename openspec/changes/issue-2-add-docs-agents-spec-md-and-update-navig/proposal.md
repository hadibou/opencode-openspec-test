# Proposal

## Why

Issue #2 asks for a dedicated `docs/agents-spec.md` and for `docs/README.md` navigation that exposes it. The documentation set currently explains what the project is, how its pieces fit together, and how a change flows, but it never states which agents participate in that flow, what each one consumes and produces, or where one role stops and the next begins. Readers have to infer the roles from tooling. A written role contract makes the pipeline reviewable and gives later documentation a stable target to extend.

## What Changes

- **Create `docs/agents-spec.md`.** One H1, with H2 sections for purpose, agent roles, handoffs and artifacts, and boundaries and guardrails. Each role gets an H3 subsection that names its inputs, its outputs, and where its authority ends.
- **Update `docs/README.md`.** Add one H2 section, "Documentation Set", that lists every `docs/*.md` file with a repository-relative link, including the new `agents-spec.md`. Add one sentence in the existing "OpenSpec Workflow" section that links to `docs/agents-spec.md`. The existing H1 and H2 sections are retained.
- **Cross-link, do not duplicate.** `docs/agents-spec.md` links back to `docs/README.md` and `docs/architecture.md`. `docs/architecture.md` is not edited: it owns structure and change flow, while the new file owns roles and handoffs.
- **No tooling changes.** `scripts/test-md.sh`, `.opencode/`, and `openspec/config.yaml` are unchanged; the existing test command and strict OpenSpec validation are the acceptance gate.

## Capabilities

### New Capabilities

None.

### Modified Capabilities

- `project-documentation`: adds requirements for the agent specification document and for README navigation across the documentation set, and updates the Markdown validity requirement so it covers the new file and the modified README.

## Impact

- **Files created:** `docs/agents-spec.md`.
- **Files modified:** `docs/README.md`.
- **Files intentionally untouched:** `docs/architecture.md`, `scripts/test-md.sh`, `.opencode/`, `openspec/config.yaml`.
- **Code, APIs, dependencies:** none.
- **Validation:** `./scripts/test-md.sh` from the repository root, and `openspec validate issue-2-add-docs-agents-spec-md-and-update-navig --strict`.

## Assumptions

- The issue has no body text; the title is the full request. The deliverables are therefore the two named documentation changes, not tooling or configuration.
- `agents-spec.md` describes the pipeline roles that this environment actually runs: planning (issue to OpenSpec change), implementation (tasks applied in a worktree), integration (branch, commit, pull request), review (audit against the approved change), and validation (test command and strict OpenSpec validation). Roles are described by responsibility rather than by persona or identity.
- The document states what each role consumes and produces, and where its authority ends. It does not enumerate per-agent tool permissions; those live in tooling and would go stale in prose.
- Handoffs are documented through artifacts that outlive a conversation: the GitHub issue, the OpenSpec change directory, the issue-specific branch and worktree, commits and pull requests, review comments, and validation output.
- The document avoids model or provider identifiers, absolute filesystem paths, the GitHub Project number, board status names, and credentials. This mirrors the constraint already established for the documentation set.
- `docs/README.md` keeps its single H1 and every existing H2 section; navigation is additive.
- `docs/architecture.md` stays unchanged in this change. The new file adds links to it and to `README.md`, so the documentation set remains connected without editing it.
- The documented test command stays exactly `./scripts/test-md.sh`, run from the repository root.
- Detailed failure handling and recovery procedures are out of scope here. The new document only states that a blocked role stops and reports rather than guessing.
- Plan status is reported from `tasks.md` alone: the Plan block on the issue reproduces the checkbox lines of `tasks.md` verbatim, in order, with their checked state, so the issue never carries a paraphrased or stale task list. The completed implementation tasks stay checked and are not reopened or reordered by this revision.

## Open questions

- Should `docs/agents-spec.md` become the normative contract that tooling must match, or remain descriptive documentation? This plan assumes descriptive: no validation enforces agreement between the document and `.opencode/` configuration.
- Should the documentation name the individual agents as configured in the harness? This plan describes the five responsibilities generically so the document survives renames.
- Is the intended audience contributors, pipeline operators, or both? This plan assumes both and keeps operational mechanics (worktrees, branches) at a conceptual level.
- These questions do not change the proposed file set or acceptance criteria; they can be answered during review without reshaping the tasks.
