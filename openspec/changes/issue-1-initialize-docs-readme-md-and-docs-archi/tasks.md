# Tasks

## 1. README

- [ ] 1.1 Create `docs/README.md` with exactly one H1 and H2 sections for overview, prerequisites, repository layout, running the tests, and the OpenSpec workflow; verify the file exists and contains a single H1.
- [ ] 1.2 Add the exact test command and working directory from `.opencode/pipeline.json` to `docs/README.md`, plus a repository-relative link to `architecture.md`; verify the quoted command matches the configuration and the link targets an existing path.

## 2. Architecture

- [ ] 2.1 Create `docs/architecture.md` with exactly one H1 and H2 sections for purpose, components, test architecture, and change workflow; verify the file exists and contains a single H1.
- [ ] 2.2 In `docs/architecture.md`, document the roles of `docs/`, `openspec/`, `.opencode/`, and `scripts/`, the documentation-only constraint, the test flow, and a repository-relative link back to `README.md`; verify each statement matches `openspec/config.yaml`, `.opencode/pipeline.json`, or `proposal.md`.

## 3. Validation

- [ ] 3.1 Check both documents for heading levels that skip a level, fenced code blocks without a language identifier, and relative links that do not resolve; fix any violations and re-check the affected file.
- [ ] 3.2 Run `openspec validate issue-1-initialize-docs-readme-md-and-docs-archi --strict` from the repository root and verify it exits successfully.
- [ ] 3.3 Run the project test command `'C:\Program Files\Git\bin\bash.exe' ./scripts/test-md.sh` from the repository root and verify it exits with status 0; if `scripts/test-md.sh` is absent, stop and report it as a blocker instead of creating it.
