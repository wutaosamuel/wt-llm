# Project History

## Project Overview
- `feature-spec` is a reusable skill for turning informal feature requests or project-level requests into verifiable requirements for a separate coding AI.
- It is technology-neutral and applies to projects such as Python, Go, Bash, and embedded firmware.

## Design & Key Decisions
- Requests written in Chinese, including “整理需求”, should trigger the skill. The generated specification defaults to the user's language unless another language is requested.
- The skill separates confirmed facts, proposals, and unknowns; it does not invent project details or write implementation code.
- Specifications cover observable behavior, relevant non-functional requirements, acceptance criteria, verification, and concise, attributable research findings.
- Project-level requests first produce a breakdown of the overall goal, shared constraints, bounded work items, completion conditions, and known dependencies. Each detailed feature specification still describes one bounded change.
- A breakdown defines what to deliver; implementation phases define when and in what order to deliver it. Items need not all be independently deployable, and priorities must not be invented.
- Implementation phases are included only for sufficiently complex work.
- By default, the specification or project breakdown is returned in the conversation. If saving is requested and permitted, follow existing project documentation conventions; otherwise use `<project-root>/docs/specs/<project-slug>-breakdown.md` for a breakdown or `<project-root>/docs/specs/<feature-slug>.md` for a feature specification. Create only directories needed for documents being saved; do not initialize a documentation skeleton.
- Core business rules stated or confirmed by the user may only be changed with the user's explicit approval of the specific change. Both the specification AI and implementation AI must preserve them; technical conflicts must be reported with their impacts and options, then wait for a decision. Affected work is blocked while independent work may continue. Specifications and project breakdowns must carry rule IDs, sources, decision status, and instructions for the implementation AI; a code/specification mismatch alone does not authorize rewriting a rule.

## Development History
| Date | Summary |
|------|---------|
| 2026-09-29 | Created the English `feature-spec` skill with Chinese-language triggering, verification planning, research evidence, and optional phased planning. |
| 2026-10-08 | Added project-level requirements decomposition, a project breakdown outline, and on-demand document-saving rules. |
| 2026-10-08 | Added core business rule change control for both specification and implementation AIs; conflicts require reporting and an explicit user decision, and rules plus implementation instructions must travel in specifications and project breakdowns. |

## Next Steps
- Place the skill where the intended AI assistant can discover it, if automatic discovery is needed.
- Try the skill on a real feature request and refine it based on the resulting specification.
