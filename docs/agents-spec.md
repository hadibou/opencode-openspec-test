# Agent Specification

This document describes the roles that carry an issue from planning through merge in this repository, the artifacts they exchange, and the limits of each role's authority. It complements [README.md](README.md), which covers setup and the documented commands, and [architecture.md](architecture.md), which covers the structure of the repository and how a change flows. The roles are described by responsibility rather than by harness configuration, so the document stays accurate when tooling changes and applies equally to contributors and to automation.

## Purpose

The purpose of this specification is to make the pipeline reviewable. Anyone reading the documentation set can answer three questions without inspecting tooling: which role acts next, what that role consumes and produces, and where one role's responsibility stops and another's begins. Handoffs are defined through artifacts that persist outside any conversation, so a handoff can be checked after the fact instead of being inferred from chat history.

This document does not describe tool permissions, model selection, or provider configuration. Those are tooling concerns and change independently of the responsibilities described here.

## Agent Roles

A change passes through five roles in order: planning, implementation, integration, review, and validation. The roles are cumulative in intent but separate in authority; each one stops at its boundary and hands its output to the next.

### Planning

- **Inputs:** a GitHub issue describing the requested change, the existing documentation set, and the current main specifications.
- **Outputs:** an OpenSpec change directory containing a proposal, a design, specification deltas, and a task list. The change name encodes the issue number so later roles can trace the work back to its origin.
- **Authority boundary:** planning decides what the change should contain and how it will be verified, but does not write documentation deliverables or modify repository files outside the change directory. When the plan is complete and internally consistent, the role stops and hands the change directory to implementation.

### Implementation

- **Inputs:** the approved OpenSpec change directory, the repository state on the default branch, and any review feedback returned from a later pass.
- **Outputs:** the documentation changes described by the change's tasks, with each completed task ticked in the task list, plus the validation results needed to show the work is complete.
- **Authority boundary:** implementation applies tasks from the change as written. When a task cannot be completed as specified, or when the specification is ambiguous or contradictory, the role stops and reports the problem rather than guessing or rewriting the plan. It does not decide architecture, merge work, or record board state.

### Integration

- **Inputs:** the implementation results in the issue-specific branch and worktree, together with the OpenSpec change directory that describes them.
- **Outputs:** commits on the issue-specific branch and a pull request that contains the change for review.
- **Authority boundary:** integration manages branches, commits, and the pull request; it does not alter the documentation content, reinterpret the plan, or approve its own work. Once the pull request is open and linked to the issue, the role stops and hands the work to review.

### Review

- **Inputs:** the pull request, the approved OpenSpec change directory, and the implementation diff.
- **Outputs:** review comments that state a verdict against the approved change and identify any required corrections.
- **Authority boundary:** review audits the work against the specification and the acceptance criteria in the change. It does not plan new work, edit the implementation, or merge outside the conditions set by the workflow. When the work meets the change, the role hands it to validation; otherwise it returns the work to implementation with its comments.

### Validation

- **Inputs:** the reviewed work, the project test command, and the OpenSpec change name under validation.
- **Outputs:** validation output showing the result of the project test command and of the strict OpenSpec validation of the change.
- **Authority boundary:** validation reports whether the documented checks pass. It does not fix failures itself or waive a gate, and a failing check stops the workflow until the responsible role corrects it. Validation output is the evidence a reviewer and the merge step rely on.

## Handoffs and Artifacts

Every handoff in the pipeline is carried by an artifact that outlives the conversation in which it was produced. A reader can verify a handoff by inspecting the artifact rather than replaying a session.

- **Issue to planning:** the GitHub issue carries the request, its scope, and the discussion that shaped it.
- **Planning to implementation:** the OpenSpec change directory carries the proposal, design, specification deltas, and task list, and is the source of truth for what to build.
- **Implementation isolation:** each issue is implemented on an issue-specific branch in its own Git worktree created from the default branch, never in the primary checkout, so the main working tree stays clean and parallel work cannot collide.
- **Implementation to integration:** commits on the issue-specific branch carry the completed work and reference the change.
- **Integration to review:** the pull request carries the diff, the linked issue, and the change name, and is the review surface.
- **Review to implementation or validation:** review comments carry the verdict and the corrections required, or the confirmation that the gates may proceed.
- **Validation to merge:** validation output carries the result of the project test command and of the strict OpenSpec validation, and is the evidence required before merge.
- **Merge to archive:** the archived change carries the accepted specification deltas into the main specifications, so the documentation set reflects the merged behavior.

Because every artifact persists in the repository or in the issue tracker, a role can be re-entered with the same inputs, and the state of the work is never held only in memory.

## Boundaries and Guardrails

- **Review gate:** a change is reviewed against its OpenSpec change before it reaches the default branch. Merging work that the review has not accepted is out of bounds for every role.
- **Validation gate:** before merge, validation runs the project test command, `./scripts/test-md.sh`, from the repository root and runs strict OpenSpec validation of the change. Both must report success; no role may substitute a weaker check.
- **Blocked means stop:** a role that cannot complete its work as specified stops and reports the problem. Guessing, silently widening scope, or editing the specification to match the implementation are not permitted.
- **Separation of authority:** planning does not implement, implementation does not review its own work, integration does not approve content, and validation does not repair failures. Each role hands off rather than absorbing the next role's decisions.
- **Stable documentation:** the documentation describes responsibilities and artifacts, not environment-specific values. It contains no absolute filesystem paths, no model or provider identifiers, no project or board identifiers, and no credentials. Links are repository-relative so the set stays portable.
- **Connected set:** this document links back to [README.md](README.md) for setup and commands and to [architecture.md](architecture.md) for structure and change flow. Roles and handoffs belong here; components and flow belong there.
