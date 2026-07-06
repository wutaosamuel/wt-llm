# Project History
<!-- All sections and their sub-content are OPTIONAL. Fill in only what applies
     to this project; omit the rest. This file is written for AI context. -->

## Project Overview
- Project type: tooling (OpenCode AI-assistant configuration).
- Goal: build reusable OpenCode skills and commands, primarily around a
  cost-optimization workflow where a higher-capability model generates content
  and a cheaper model persists it to disk verbatim.

## Current Status
- Two artifacts implemented under `.opencode/`: a `low-cost-write` Skill and a
  matching `low-cost-write` Command.
- A pre-existing `update-history-memo` Skill and `init-history-memo` Command are
  present and used as the style/format reference.

## Environment & Toolchain
- OpenCode with `@opencode-ai/plugin` 2.1.3 (see `.opencode/package.json`).
- Windows / PowerShell environment.

## Design & Key Decisions
- Cost-optimization workflow: expensive model (Opus) generates content; a cheaper
  model (Haiku/Sonnet) writes it, to reduce cost.
- Model split rationale: whole-file verbatim writes and short content suit Haiku;
  precise edits, long content, and multi-file/multi-step work favor Sonnet for
  reliability.
- The user drives model switching manually, so the enforcement mechanism was
  designed as directives (Skill + Command) rather than an automated router.
- Both a Skill (auto-loaded by matching its description) and a Command (manually
  invoked via `/low-cost-write`) were created so the same rules cover both the
  automatic and the manual trigger paths.
- Naming was standardized to `low-cost-write`.
- A content-delimiter convention (`<<<CONTENT>>>...<<<END>>>`) is used so the
  executor treats wrapped text strictly as data, never as instructions.

## Pitfalls & Lessons Learned
- The biggest hidden cost of using a cheaper executor model is not tokens but
  silent content alteration causing expensive rework. Mitigation: hard rules
  (verbatim copy, no rewriting) plus mandatory read-back verification.
- The system prompt reported "no skills available", but the actual project does
  support skills (an existing skills directory was found). Lesson: verify the
  real project environment rather than trusting the ambient system prompt.

## Development History
| Date | Summary |
|------|---------|
| 2026-07-06 | Designed a low-cost verbatim-write workflow (expensive model generates, cheap model writes). Created the `low-cost-write` Skill (`.opencode/skills/low-cost-write/SKILL.md`) and Command (`.opencode/commands/low-cost-write.md`), both enforcing character-for-character copying, no rewriting, single-file scope, and mandatory read-back verification, using a `<<<CONTENT>>>...<<<END>>>` delimiter convention. Initialized this project history memo. |

## Next Steps
- Optionally validate the `low-cost-write` Command/Skill on a real "expensive
  generates -> cheap writes" task and confirm the read-back verification catches
  alterations.
- Consider whether an `AGENTS.md` is warranted for this project.

## Conventions & Standards
- Skill/Command files use English content with frontmatter following the existing
  `update-history-memo` style (`name`, `description`, `license: MIT`,
  `compatibility: opencode`, `metadata`).
