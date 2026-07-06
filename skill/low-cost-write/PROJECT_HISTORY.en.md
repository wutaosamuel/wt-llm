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
- A Command must not be designed to "enter a mode and then wait for the user to
  paste content separately". When the content was already produced by the
  higher-capability model in the same session, it should proactively look back
  through the session for the content and target path rather than idling on an
  empty `$ARGUMENTS`; otherwise an argument-less `/low-cost-write` has nothing to
  write and just stalls in a waiting state.
- Whether a Command/Skill file's body is in English or Chinese only affects the
  file's own content, not the language used in the current session. English is
  chosen purely to follow the existing convention, not to avoid a language
  effect.
- When the target file already exists, the Write tool requires a Read first
  before overwriting (even if the file is empty). The low-cost executor flow
  should treat "read before write" as a fixed step to avoid the first write
  being blocked.

## Development History
| Date | Summary |
|------|---------|
| 2026-07-06 | Designed a low-cost verbatim-write workflow (expensive model generates, cheap model writes). Created the `low-cost-write` Skill (`.opencode/skills/low-cost-write/SKILL.md`) and Command (`.opencode/commands/low-cost-write.md`), both enforcing character-for-character copying, no rewriting, single-file scope, and mandatory read-back verification, using a `<<<CONTENT>>>...<<<END>>>` delimiter convention. Initialized this project history memo. |
| 2026-07-06 | Fixed `/low-cost-write` only "entering a waiting mode" instead of executing. The Command and SKILL were built entirely around `$ARGUMENTS` and told the model to wait for the user to paste content separately, so an argument-less invocation had nothing to write. Changed to: by default look back through the current session, take the higher-capability model's most recent final content plus the target path it named, and write it verbatim; if the path is ambiguous, STOP and ask (never guess); the `Path/Operation/<<<CONTENT>>>` manual format is demoted to an optional fallback. |
| 2026-07-06 | Test-ran the new `/low-cost-write` workflow: entered low-cost executor mode, pulled the higher-capability model's already-generated content from this session, wrote it to `tmp.txt`, confirmed write with read-back verification; followed up with byte-level audit confirming 75 bytes, LF line endings, zero differences. Passed. |
| 2026-07-06 | Refined the target path resolution in `low-cost-write`: when a filename plus working directory can uniquely identify a file, write it directly without asking; only STOP and ask when the path is genuinely ambiguous (same filename in multiple directories, or directory cannot be inferred). Reduced tedious confirmations. |

## Next Steps
- (Done) Validated the `low-cost-write` workflow on `tmp.txt` with a byte-level
  read-back check. A follow-up negative test (deliberately altered content) could
  confirm the read-back verification actively reports differences.
- Nail down the trailing-newline convention: whether the content ends with a
  newline is decided by the delivered content; the executor preserves it
  verbatim and neither adds nor removes it.
- Consider whether an `AGENTS.md` is warranted for this project.

## Conventions & Standards
- Skill/Command files use English content (following the existing convention; the
  file language does not affect the session's conversation language), with
  frontmatter following the existing `update-history-memo` style (`name`,
  `description`, `license: MIT`, `compatibility: opencode`, `metadata`).
- `/low-cost-write` by default extracts the higher-capability model's
  already-generated content from the current session and writes it to the target
  file it named; if the target path is ambiguous it stops and asks, never
  guessing. The manual `Path/Operation/<<<CONTENT>>>` format is an optional
  fallback.
