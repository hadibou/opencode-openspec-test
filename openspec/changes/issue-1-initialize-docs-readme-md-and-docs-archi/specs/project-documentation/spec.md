# Spec Delta

## Purpose

Provide a human-readable entry point and architecture description for this documentation-only test project, including how the Markdown test setup works.

## ADDED Requirements

### Requirement: README documents purpose and test setup

The repository SHALL provide `docs/README.md` as the primary entry point. It SHALL describe the project purpose, prerequisites, repository layout, and the exact documentation test command, and SHALL link to `docs/architecture.md`.

#### Scenario: README structure

- **WHEN** a reader opens `docs/README.md`
- **THEN** the file starts with exactly one H1 title and contains H2 sections for overview, prerequisites, repository layout, running the tests, and the OpenSpec workflow

#### Scenario: Exact test command is documented

- **WHEN** a reader looks for how to validate the documentation
- **THEN** `docs/README.md` shows the test command exactly as `./scripts/test-md.sh` and states that it is run from the repository root
- **AND** the Windows/Git Bash wrapper from `.opencode/pipeline.json` does not appear in the documented command

#### Scenario: README links to the architecture document

- **WHEN** a reader follows the architecture link in `docs/README.md`
- **THEN** the link resolves to `docs/architecture.md` using a repository-relative path

### Requirement: Architecture document describes components and test flow

The repository SHALL provide `docs/architecture.md` describing the documentation-only system. It SHALL explain the roles of `docs/`, `openspec/`, `.opencode/`, and `scripts/`, how Markdown validation runs, and how a GitHub issue becomes an OpenSpec change. It SHALL link to `docs/README.md`.

#### Scenario: Architecture structure

- **WHEN** a reader opens `docs/architecture.md`
- **THEN** the file starts with exactly one H1 title and uses H2 sections for purpose, components, test architecture, and change workflow

#### Scenario: Documentation-only constraint is stated

- **WHEN** a reader checks what the project produces
- **THEN** `docs/architecture.md` states that the only deliverables are Markdown files in `docs/` and that the OpenSpec and `.opencode` folders are tooling rather than deliverables

#### Scenario: Test architecture is described precisely

- **WHEN** a reader checks how documentation is validated
- **THEN** `docs/architecture.md` states that `./scripts/test-md.sh` is run from the repository root and performs these checks:
  - `docs/` exists
  - every `docs/*.md` is non-empty
  - every `docs/*.md` contains a top-level `#` header
  - `shellcheck` runs on `scripts/*.sh` when it is installed

#### Scenario: Test script scope is stated

- **WHEN** a reader checks whether this change adds test tooling
- **THEN** `docs/architecture.md` states that `scripts/test-md.sh` already exists on the default branch and is out of scope for this change

#### Scenario: Architecture links back to the README

- **WHEN** a reader follows the README link in `docs/architecture.md`
- **THEN** the link resolves to `docs/README.md` using a repository-relative path

### Requirement: Issue and board tracking is described generically

`docs/architecture.md` SHALL describe the issue-to-change workflow and project-board tracking without naming the GitHub Project number or specific status values.

#### Scenario: No board identifiers are documented

- **WHEN** either documentation file is checked for project-board references
- **THEN** it does not name the project number from `.opencode/pipeline.json` or any board status value

### Requirement: Documentation uses valid Markdown structure and links

All documentation added by this change SHALL use valid Markdown: exactly one H1 per file, heading levels that do not skip a level, fenced code blocks annotated with a language, and repository-relative links that resolve to existing paths.

#### Scenario: Heading hierarchy is valid

- **WHEN** either documentation file is checked
- **THEN** it has exactly one H1 and every heading level increases by at most one from the previous heading

#### Scenario: Code blocks declare a language

- **WHEN** either documentation file contains a fenced code block
- **THEN** the opening fence is followed by a language identifier such as `bash`, `text`, or `markdown`

#### Scenario: Relative links resolve

- **WHEN** a relative link in either documentation file is resolved from that file's directory
- **THEN** the target file exists in the repository

#### Scenario: Repository test command succeeds

- **WHEN** `./scripts/test-md.sh` is run from the repository root after both documents are created
- **THEN** it exits with status 0 after confirming that `docs/` exists, that every `docs/*.md` is non-empty and contains a top-level `#` header, and that `shellcheck` passes on `scripts/*.sh` when it is installed
