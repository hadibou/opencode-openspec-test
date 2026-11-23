# Spec Delta

## MODIFIED Requirements

### Requirement: README documents purpose and test setup

The repository SHALL provide `docs/README.md` as the primary entry point. It SHALL describe the project purpose, prerequisites, repository layout, and the exact documentation test command. It SHALL list every file in the documentation set with a repository-relative link, and SHALL link to `docs/agents-spec.md`.

#### Scenario: README structure

- **WHEN** a reader opens `docs/README.md`
- **THEN** the file starts with exactly one H1 title and contains H2 sections for overview, prerequisites, repository layout, running the tests, the documentation set, and the OpenSpec workflow

#### Scenario: Exact test command is documented

- **WHEN** a reader looks for how to validate the documentation
- **THEN** `docs/README.md` shows the test command exactly as `./scripts/test-md.sh` and states that it is run from the repository root
- **AND** the Windows/Git Bash wrapper from `.opencode/pipeline.json` does not appear in the documented command

#### Scenario: README links to the architecture document

- **WHEN** a reader follows the architecture link in `docs/README.md`
- **THEN** the link resolves to `docs/architecture.md` using a repository-relative path

#### Scenario: README navigation covers the documentation set

- **WHEN** a reader opens the documentation set section in `docs/README.md`
- **THEN** every Markdown file in `docs/` is listed with a repository-relative link
- **AND** following the `agents-spec.md` entry resolves to `docs/agents-spec.md`

#### Scenario: README workflow links to the agent specification

- **WHEN** a reader reads the OpenSpec workflow section in `docs/README.md`
- **THEN** it links to `docs/agents-spec.md` using a repository-relative path for the roles that execute the workflow

### Requirement: Documentation uses valid Markdown structure and links

All documentation files created or modified by this change SHALL use valid Markdown: exactly one H1 per file, heading levels that do not skip a level, fenced code blocks annotated with a language, and repository-relative links that resolve to existing paths.

#### Scenario: Heading hierarchy is valid

- **WHEN** any documentation file created or modified by this change is checked
- **THEN** it has exactly one H1 and every heading level increases by at most one from the previous heading

#### Scenario: Code blocks declare a language

- **WHEN** any documentation file created or modified by this change contains a fenced code block
- **THEN** the opening fence is followed by a language identifier such as `bash`, `text`, or `markdown`

#### Scenario: Relative links resolve

- **WHEN** a relative link in any documentation file created or modified by this change is resolved from that file's directory
- **THEN** the target file exists in the repository

#### Scenario: Documentation cross-references stay connected

- **WHEN** the documentation set is checked after this change
- **THEN** `docs/README.md` links to `docs/agents-spec.md`, and `docs/agents-spec.md` links back to `docs/README.md` and `docs/architecture.md` using repository-relative paths

#### Scenario: Repository test command succeeds

- **WHEN** `./scripts/test-md.sh` is run from the repository root after this change
- **THEN** it exits with status 0 after confirming that `docs/` exists and that every `docs/*.md` file is non-empty and contains a top-level `#` header, and that `shellcheck` passes on `scripts/*.sh` when it is installed

## ADDED Requirements

### Requirement: Agent specification documents each pipeline role

`docs/agents-spec.md` SHALL document every role in the issue-to-merge pipeline: planning, implementation, integration, review, and validation. For each role, it SHALL state the inputs consumed, the outputs produced, and where the role's authority ends.

#### Scenario: Agent specification structure

- **WHEN** a reader opens `docs/agents-spec.md`
- **THEN** the file starts with exactly one H1 title and contains H2 sections for purpose, agent roles, handoffs and artifacts, and boundaries and guardrails

#### Scenario: Roles cover the whole pipeline

- **WHEN** a reader looks for which roles take part in a change
- **THEN** the document describes planning, implementation, integration, review, and validation as separate roles

#### Scenario: Every role states inputs and outputs

- **WHEN** a reader checks any role subsection in the agent specification
- **THEN** it names what that role consumes, what it produces, and the point at which it stops or hands off to another role

### Requirement: Agent handoffs are defined by persistent artifacts

`docs/agents-spec.md` SHALL define every handoff between roles in terms of artifacts that persist outside a conversation: the GitHub issue, the OpenSpec change directory, the issue-specific branch and Git worktree, commits and pull requests, review output, and validation output. It SHALL state that implementation runs in an isolated worktree rather than the primary checkout.

#### Scenario: Handoffs name their artifacts

- **WHEN** a reader follows the handoffs section of the agent specification
- **THEN** each transition between roles names the artifact that carries the work forward

#### Scenario: Worktree isolation is stated

- **WHEN** a reader checks how implementation work is isolated
- **THEN** the document states that each issue is implemented on an issue-specific branch in its own Git worktree, not in the primary checkout

#### Scenario: Review and validation gates are described

- **WHEN** a reader checks how work reaches the default branch
- **THEN** the document states that a change is reviewed against its OpenSpec change and that validation runs the project test command and strict OpenSpec validation before merge

### Requirement: Agent specification excludes environment-specific configuration

`docs/agents-spec.md` SHALL describe roles and handoffs without model or provider identifiers, absolute filesystem paths, the GitHub Project number, board status names, or credentials. All links in the file SHALL be repository-relative.

#### Scenario: No environment-specific values are documented

- **WHEN** `docs/agents-spec.md` is checked for environment-specific values
- **THEN** it contains no model or provider identifier, no absolute path such as a `C:` drive path, no project number, no board status name, and no credential

#### Scenario: Links are repository-relative

- **WHEN** a link in `docs/agents-spec.md` is resolved
- **THEN** it is a repository-relative path and its target exists in the repository
