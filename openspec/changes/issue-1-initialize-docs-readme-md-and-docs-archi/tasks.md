# Tasks

## 1. README

- [x] 1.1 Create `docs/README.md` with exactly one H1 and H2 sections for overview, prerequisites, repository layout, running the tests, and the OpenSpec workflow; verify the file exists and contains a single H1.
- [x] 1.2 Add the exact test command `./scripts/test-md.sh` and state that it runs from the repository root; do not copy the Windows/Git Bash wrapper from `.opencode/pipeline.json`. Also add a repository-relative link to `architecture.md`; verify the command text and that the link target exists.

## 2. Architecture

- [x] 2.1 Create `docs/architecture.md` with exactly one H1 and H2 sections for purpose, components, test architecture, and change workflow; verify the file exists and contains a single H1.
- [x] 2.2 In `docs/architecture.md`, document the roles of `docs/`, `openspec/`, `.opencode/`, and `scripts/`, the documentation-only constraint, the test flow, and a repository-relative link back to `README.md`; verify `scripts/test-md.sh` is described as out of scope for this change.
- [x] 2.3 In the test-architecture section, state that `./scripts/test-md.sh` run from the repository root checks that `docs/` exists, that every `docs/*.md` is non-empty, that every `docs/*.md` contains a top-level `#` header, and that `shellcheck` runs on `scripts/*.sh` when it is installed; verify each statement against `scripts/test-md.sh`.
- [x] 2.4 Describe the issue-to-change workflow and project-board tracking generically, without naming the project number or specific status values; verify no board number or status name appears in the file.

## 3. Validation

- [x] 3.1 Check both documents for heading levels that skip a level, fenced code blocks without a language identifier, and relative links that do not resolve; fix any violations and re-check the affected file.
- [x] 3.2 Run `openspec validate issue-1-initialize-docs-readme-md-and-docs-archi --strict` from the repository root and verify it exits successfully.
- [x] 3.3 Run `./scripts/test-md.sh` from the repository root and verify it exits with status 0.
