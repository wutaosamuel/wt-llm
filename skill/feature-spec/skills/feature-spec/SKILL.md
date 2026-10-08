---
name: feature-spec
description: Turn rough feature requests or project-level requests into implementation-ready, verifiable requirements for another coding AI. Use for project-level requirements decomposition, feature specifications, requirements gathering, clarification, acceptance criteria, or implementation handoff, including when the user describes the feature or asks to organize requirements in Chinese (e.g. 整理需求, 功能需求, 技术规格书). Works across Python, Go, Bash, embedded, and other projects; does not implement code.
license: MIT
compatibility: opencode
metadata:
  audience: developers
  scope: requirements-specification
---

# Feature Specification

## Purpose

Turn an informal feature idea or project-level request into verifiable
requirements that another AI can implement. For a project-level request,
first decompose the project into bounded features or work items; write detailed
technical specifications for selected items as needed. This skill is
technology-neutral: do not presume a language, framework, operating system,
or hardware platform.

Use this skill regardless of whether the request is in English or Chinese. In
particular, a Chinese description of a feature or a request to "整理需求" is
just as much a trigger as an English request for a feature specification. Write
the specification in the user's language unless the user requests another
language. This SKILL.md itself is in English.

A detailed feature specification describes one bounded change. A project
breakdown describes the overall goal and how the proposed work is divided;
it is not a substitute for detailed feature specifications. Do not put
feature-specific requirements in `AGENTS.md` (project-wide rules) or in this
skill file. Do not write implementation code as part of this workflow.

## Workflow

1. **Understand the request.** Extract the goal, current and desired behavior,
   known constraints, and whether the task is a new feature, behavior change,
   bug fix, or migration. Preserve the user's terminology and avoid expanding
   scope without approval.

2. **Inspect available context.** If the project is accessible, read relevant
   project instructions, docs, interfaces, tests, and nearby code. Use relevant
   research and decisions from the current session as context. If no project
   is available, say which project details remain unverified. Do not invent
   paths, signatures, versions, hardware parameters, existing behavior, or
   test commands.

3. **Classify scope and decompose project-level requests.** Decide whether
   the request describes one bounded change or a project with multiple
   deliverables. For a project-level request, identify the overall goal,
   shared constraints, project-wide acceptance outcomes, and major
   capabilities. Propose bounded features or work items with clear scope and
   completion conditions; note known dependencies without requiring every
   item to be independently deployable. Distinguish user-confirmed scope from
   proposed decomposition. Do not invent priorities, dependencies, or
   requirements. Present the breakdown before drafting detailed feature
   specifications. If no item has been selected for detailed specification,
   deliver the breakdown rather than forcing specifications for every item.
   Ask only when a decision materially affects the boundaries or acceptance
   outcomes.

4. **Distinguish certainty.** Mark consequential information as confirmed
   (stated by the user or verified against a source), proposed (a recommendation
   not yet accepted), or unknown. For external references, record the source,
   applicable version, and whether applicability to this project is verified.
   Never silently promote a proposal or inference into a requirement.

5. **Identify gaps and ask consequential questions.** Check functional behavior,
   inputs and outputs, errors, compatibility, and relevant non-functional needs
   such as performance, latency, security, reliability, resource limits, and
   portability. Determine how important behavior could be verified by tests,
   existing commands, manual steps, or a device/environment. Ask concise,
   grouped questions only when an unknown could materially affect the external
   contract, core behavior, safety/security, compatibility, measurable targets,
   or acceptance criteria. Do not invent numeric targets. Leave incidental
   implementation choices to the coding AI.

6. **Preserve useful research.** Summarize only findings that affect decisions
   or boundaries, including relevant findings already obtained in this session.
   Give each finding a source and verification status. Do not include a
   chronological search log, irrelevant results, or search keywords.

7. **Draft the specification when appropriate.** For a single change or a
   selected item from a project breakdown, describe observable conditions
   and results rather than prescribing code. Cover normal, boundary, and
   failure behavior; distinguish mandatory constraints from optional
   suggestions; identify existing behavior that must remain unchanged. Give
   each important behavior a testable acceptance criterion and a verification
   method. Omit irrelevant template sections instead of filling them with
   guesses.

8. **Plan only when complexity warrants it.** For multi-module work,
   migrations, external dependencies, or substantial risks, provide
   milestone-level implementation phases with dependencies, deliverables, and
   completion criteria. A project breakdown defines *what* is to be delivered;
   implementation phases describe *when and in what order* to deliver it. Do
   not specify every code edit, substitute phases for the behavioral contract,
   or force phases onto simple features.

9. **Assess readiness.** Mark a detailed specification "Ready to implement"
   only if no unresolved issue could materially change its implementation or
   acceptance results. Otherwise mark it "Draft - decisions needed" and
   identify blocking questions and their effects. For a project breakdown,
   state whether its feature boundaries are confirmed or proposed and identify
   decisions needed before detailing affected items. Do not claim a project
   fact was checked, or a test passed, unless it was actually checked or run.

10. **Deliver or save.** By default, present the project breakdown or full
    Markdown feature specification in the response without changing project
    files. When saving is requested and file edits are permitted, first
    confirm the project root and follow any existing documentation convention.
    If none applies, use
    `<project-root>/docs/specs/<project-slug>-breakdown.md` for a project
    breakdown and `<project-root>/docs/specs/<feature-slug>.md` for a detailed
    feature specification. Use short, stable, lowercase hyphenated slugs.
    Check whether each target already exists; do not overwrite it without the
    user's direction. Create only the directories needed for documents actually
    being saved; do not initialize a documentation skeleton, empty directories,
    or an index by default. If the project root is unknown or writing is
    unavailable, provide the document and a suggested path instead. Follow any
    higher-priority restrictions on protected or generated files.

## Project breakdown outline

Use this only for project-level requests. Keep it concise and adapt the
sections to the available evidence:

- **Status and sources:** target project, inspected sources, and whether the
  proposed boundaries are confirmed or still need decisions.
- **Project goal and shared constraints:** desired overall outcome,
  project-wide acceptance outcomes, and constraints that apply across items.
- **Proposed items:** for each item, a stable ID, goal, scope boundary,
  observable completion condition, and status (confirmed or proposed).
- **Relationships:** known dependencies, shared interfaces, or requirements
  spanning items; mark unverified relationships as proposed.
- **Open decisions:** questions that materially affect item boundaries or
  project-wide acceptance, with their impact.

Do not invent priorities or schedules. Do not turn the breakdown into a
detailed specification for every item. A detailed specification derived from
the breakdown should identify its parent project and item ID, and carry
forward applicable shared constraints.

## Specification outline

Use these sections as needed; omit irrelevant subsections. Keep confirmed facts,
proposals, and open questions distinct throughout.

### 0. Document status

- Status: Ready to implement / Draft - decisions needed
- Target project or module; sources inspected; unverified assumptions
- For an item from a project breakdown: parent project and item ID;
  applicable shared constraints and known dependencies

### 1. Goal and background

- Problem, current behavior, desired outcome

### 2. Scope

- Must implement; out of scope; existing behavior that must remain unchanged

### 3. Environment and constraints

- Verified stack, runtime/platform or hardware, relevant entry points
- Dependencies, compatibility, security, resource or timing constraints
- Protected files or directories

### 4. External contract

- Entry point (function, CLI, API, event, device interface, etc.)
- Input types, formats, ranges and defaults; outputs and side effects
- Error behavior, exit codes or recovery; backwards compatibility

### 5. Behavior rules

| ID | Given / condition | When / trigger | Then / observable result |
|----|-------------------|----------------|--------------------------|
| R1 | ...               | ...            | ...                      |

### 6. Edge and failure cases

- Missing/invalid input, repeated execution, partial failure, timeout or
  cancellation; concurrency, permissions, network loss or restart if relevant

### 7. Non-functional requirements (only relevant dimensions)

| Dimension | Requirement or target | Verification | Status |
|-----------|-----------------------|--------------|--------|
| ...       | ...                   | ...          | Confirmed / proposed / unknown |

Do not turn unspecified metrics into arbitrary numeric requirements.

### 8. Implementation boundaries

- Mandatory constraints; choices left to the implementer; optional suggestions

### 9. Acceptance criteria

- [ ] AC1: Given ..., when ..., then ...
- [ ] AC2: Given ..., when ..., then ...
- [ ] Existing ... behavior remains unchanged.

### 10. Verification plan

| Acceptance criterion | Method | Command or manual steps | Environment |
|----------------------|--------|-------------------------|-------------|
| AC1                  | ...    | ...                     | ...         |

- Distinguish verified existing commands from proposed tests and checks.
- Identify device/environment-dependent checks that cannot be run here.
- A documented command is not evidence it has been executed.

### 11. Evidence and research (if relevant)

| Finding | Source and applicable version | Verification status |
|---------|-------------------------------|---------------------|
| ...     | ...                           | Verified / unverified |

### 12. Implementation phases (complex work only)

| Phase | Deliverable | Dependencies | Completion criteria |
|-------|-------------|--------------|---------------------|
| ...   | ...         | ...          | ...                 |

### 13. Open questions

| Question | Impact on implementation or acceptance | Blocking? |
|----------|----------------------------------------|-----------|
| ...      | ...                                    | Yes / No  |

## Technology-specific checks

Apply only where relevant:

- Python: supported versions, public signatures, exceptions, dependencies,
  sync/async behavior.
- Go: public API, concurrency, context cancellation, error handling, Go version.
- Bash: target shell and OS, arguments, environment variables, stdout/stderr,
  exit codes, quoting and paths with spaces, repeatability.
- Embedded: MCU and toolchain, peripherals, timing, memory, fault behavior,
  hardware validation, and generated-code boundaries.
- Services/APIs: schema, authentication, timeouts, retries, persistence,
  migration, backwards compatibility.

## Final check

- Important mandatory behaviors map to observable acceptance criteria.
- Relevant non-functional requirements have evidence or are marked open.
- Research is concise, attributable, and not confused with user requirements.
- Verification steps are actionable and not misrepresented as already run.
- Readiness agrees with remaining blocking questions.
- For project-level requests, the breakdown records bounded items,
  project-wide outcomes, and known cross-item relationships without inventing
  priorities or treating proposed boundaries as confirmed.
- Detailed specifications derived from a breakdown identify their parent
  item and preserve applicable shared constraints.
