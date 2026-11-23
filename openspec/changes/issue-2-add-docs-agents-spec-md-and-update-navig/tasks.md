# Tasks

## 1. Agent specification document (`docs/agents-spec.md`)

- [x] 1.1 Create `docs/agents-spec.md` with a single H1 and H2 sections named "Purpose", "Agent Roles", "Handoffs and Artifacts", and "Boundaries and Guardrails"; verify the file starts with exactly one `# ` heading and no heading level skips a step.
- [x] 1.2 Under "Agent Roles", add one H3 subsection for each of planning, implementation, integration, review, and validation, each naming the role's inputs, outputs, and the point where its authority ends; verify all five roles are present and each subsection states inputs and outputs.
- [x] 1.3 Under "Handoffs and Artifacts", list every handoff with the artifact that carries it forward - GitHub issue, OpenSpec change directory, issue-specific branch and Git worktree, commits and pull request, review output, and validation output - and state that implementation runs in an isolated worktree rather than the primary checkout; verify each handoff names an artifact.
- [x] 1.4 Under "Boundaries and Guardrails", state the review and validation gates required before merge and that a blocked role stops and reports instead of guessing; link to `README.md` and `architecture.md` with repository-relative paths; verify both links resolve and that the file contains no absolute path, model or provider identifier, project number, board status name, or credential.

## 2. README navigation (`docs/README.md`)

- [x] 2.1 Add an H2 "Documentation Set" section to `docs/README.md` listing `README.md`, `architecture.md`, and `agents-spec.md` with repository-relative links; verify every `docs/*.md` file is listed exactly once and each link resolves to an existing file.
- [x] 2.2 Add one sentence to the existing "OpenSpec Workflow" section that links to `agents-spec.md`; verify the link resolves and that `docs/README.md` still has exactly one H1 and all of its existing H2 sections.

## 3. Validation

- [x] 3.1 Review `docs/README.md` and `docs/agents-spec.md` for a single H1 per file, heading levels that do not skip a level, and fenced code blocks with a language identifier; fix any violation and re-check the affected file.
- [x] 3.2 Run `openspec validate issue-2-add-docs-agents-spec-md-and-update-navig --strict` from the repository root and verify it reports no problems.
- [x] 3.3 Run `./scripts/test-md.sh` from the repository root and verify it exits with status 0.

## Workflow follow-up

- Archive the change after review and merge, and verify the archived delta updates `project-documentation` without unresolved requirements.
- Report progress from this file: every plan announcement reproduces these checkbox lines verbatim, once each and in this order, with the checked state shown here, so the issue snapshot and `tasks.md` never disagree. Tasks 1.1 through 3.3 are complete and stay checked.
