# Project History

## Project Overview
- Goal: produce a reusable set of prompt templates addressing "how to get an
  LLM / coding agent to write a script or piece of software".
- Project type: Tooling (prompt templates / AI collaboration conventions),
  not a specific software product.

## Current Status
- Completed Short and Full prompt templates, each in Chinese and English
  (4 files total).

## Design & Key Decisions
- Templates split into "Short" (everyday small tasks) and "Full" (complex /
  larger projects).
- The Full version additionally includes "Filling Tips" and a "Capability
  Boundaries" reference table for the user; these are not meant to be pasted
  into the agent prompt verbatim.
- Bilingual file naming convention: `<name>.zh-cn.md` / `<name>.en.md`, with
  content kept in one-to-one correspondence.
- Three core principles emphasized: provide real input/output examples, make
  acceptance criteria verifiable, and state boundaries clearly (scope,
  permissions, stop conditions, when to ask).

## Key References
- No external datasheets/reference designs; content is based on general
  prompt-engineering best practices.

## Development History
| Date | Summary |
|------|---------|
| 2026-07-28 | Initial creation: authored `PROMPT_TEMPLATE_SHORT.zh-cn.md`, `PROMPT_TEMPLATE_SHORT.en.md`, `PROMPT_TEMPLATE_FULL.zh-cn.md`, `PROMPT_TEMPLATE_FULL.en.md`, and set up the PROJECT_HISTORY memo mechanism. |

## Next Steps
- Optional: wrap the templates into a custom command/Skill for this tool so
  they can be invoked with one line.
- Optional: create domain-specific variants (e.g., embedded/PIC MCU
  development).

## Conventions & Standards
- Template files live in the project root (currently the `tmp` directory).
- Bilingual files must stay in one-to-one sync; updating one requires
  updating the other.
