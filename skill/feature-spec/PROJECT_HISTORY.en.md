# Project History

## Project Overview
- `feature-spec` is a reusable skill for turning informal feature requests or project-level requests into verifiable requirements for a separate coding AI.
- It is technology-neutral and applies to projects such as Python, Go, Bash, and embedded firmware.

## Design & Key Decisions
- Requests written in Chinese, including “整理需求”, should trigger the skill. The generated specification defaults to the user's language unless another language is requested.
- The skill separates confirmed facts, proposals, and unknowns; it does not invent project details or write implementation code.
- Specifications cover observable behavior, relevant non-functional requirements, acceptance criteria, verification, and concise, attributable research findings.
- Project-level requests first produce a breakdown of the overall goal, shared constraints, bounded work items, completion conditions, and known dependencies. Each detailed feature specification still describes one bounded change.
- A project breakdown defines what to deliver. Optional recommended phases group existing item IDs by known dependencies only, showing a proposed execution order and completion conditions without repeating detailed requirements or inventing priorities, schedules, or work items. Skip phases if all items are independent or there is only one item; mark items waiting on open decisions as `Blocked`. The user may later detail any item separately without following the phases first.
- P0 is intended as an anytime, repeatable prototype and reference track, not a dependency-ordered phase or a required prerequisite for Phase 1. It may validate feasibility, build an end-to-end skeleton, or produce rough feature implementations for later reference. The skill specifies P0 work; a separate coding AI implements the prototype.
- An overall reference prototype should cover the main flow and module boundaries at minimal depth, then investigate uncertain features more deeply where needed. The draft skill distinguishes document checks (V0), real-environment probes (V1), skeleton integration (V2), measurement against a user-confirmed target (V3), and rough feature implementation. P0 deliverables should identify their targets, permitted shortcuts, code disposition, evidence, assumptions, and remaining gaps.
- P0 code does not by itself confirm requirements or replace an approved implementation. Confirmed core business rules within its scope must be preserved or explicitly marked as not covered; other behavior remains proposed until accepted by the user.
- By default, the specification or project breakdown is returned in the conversation. If saving is requested and permitted, follow existing project documentation conventions; otherwise use `<project-root>/docs/specs/<project-slug>-breakdown.md` for a breakdown or `<project-root>/docs/specs/<feature-slug>.md` for a feature specification. Create only directories needed for documents being saved; do not initialize a documentation skeleton.
- Core business rules stated or confirmed by the user may only be changed with the user's explicit approval of the specific change. Both the specification AI and implementation AI must preserve them; technical conflicts must be reported with their impacts and options, then wait for a decision. Affected work is blocked while independent work may continue. Specifications and project breakdowns must carry rule IDs, sources, decision status, and instructions for the implementation AI; a code/specification mismatch alone does not authorize rewriting a rule.

## Development History
| Date | Summary |
|------|---------|
| 2026-09-29 | Created the English `feature-spec` skill with Chinese-language triggering, verification planning, research evidence, and optional phased planning. |
| 2026-10-08 | Added project-level requirements decomposition, a project breakdown outline, and on-demand document-saving rules. |
| 2026-10-08 | Added core business rule change control for both specification and implementation AIs; conflicts require reporting and an explicit user decision, and rules plus implementation instructions must travel in specifications and project breakdowns. |
| 2026-10-14 | Simplified phases into optional dependency-based groupings in project breakdowns; marked items awaiting decisions as `Blocked`, removed phases from single-item specifications, and clarified that any item may be detailed separately. |
| 2026-10-23 | Defined P0 as an anytime prototype/reference track and added a draft P0 section, workflow references, and a breakdown example to the source skill. The source changes are not yet synced to the loaded skill. |

## Next Steps
- Finalize the P0 instructions in the source skill, then sync them to the location from which the skill is actually loaded.
- Try the skill on a real P0 request and a real feature request; refine it based on the resulting specifications.
