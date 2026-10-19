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
- **THEN** `docs/README.md` shows the test command exactly as configured in `.opencode/pipeline.json`, including the working directory from which it is run

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

#### Scenario: Test architecture is described

- **WHEN** a reader checks how documentation is validated
- **THEN** `docs/architecture.md` identifies the configured test command, the directory it runs from, the checks it is expected to perform (Markdown structure and relative links), and what happens when validation fails

#### Scenario: Architecture links back to the README

- **WHEN** a reader follows the README link in `docs/architecture.md`
- **THEN** the link resolves to `docs/README.md` using a repository-relative path

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

#### Scenario: Configured test command succeeds

- **WHEN** the test command configured in `.opencode/pipeline.json` is run from the repository root
- **THEN** it exits with status 0 and reports no Markdown validation errors
