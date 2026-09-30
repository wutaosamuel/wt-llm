# Project History

## Project Overview
- `feature-spec` is a reusable skill for turning informal feature requests into verifiable technical specifications for a separate coding AI.
- It is technology-neutral and applies to projects such as Python, Go, Bash, and embedded firmware.

## Design & Key Decisions
- Requests written in Chinese, including “整理需求”, should trigger the skill. The generated specification defaults to the user's language unless another language is requested.
- The skill separates confirmed facts, proposals, and unknowns; it does not invent project details or write implementation code.
- Specifications cover observable behavior, relevant non-functional requirements, acceptance criteria, verification, and concise, attributable research findings.
- Implementation phases are included only for sufficiently complex work.
- By default, the specification is returned in the conversation. If saving is requested and permitted, the suggested location is `<project-root>/docs/specs/<feature-slug>.md`.

## Development History
| Date | Summary |
|------|---------|
| 2026-09-29 | Created the English `feature-spec` skill with Chinese-language triggering, verification planning, research evidence, and optional phased planning. |

## Next Steps
- Place the skill where the intended AI assistant can discover it, if automatic discovery is needed.
- Try the skill on a real feature request and refine it based on the resulting specification.
