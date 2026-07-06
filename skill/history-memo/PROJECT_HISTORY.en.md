# Project History

<!-- This file is AI-facing context for a development project (software /
     hardware / embedded / tooling / mixed).
     All sections and their sub-content are OPTIONAL — fill in only what applies
     to this project and omit the rest. Do not fabricate content.
     Keep this file in sync with PROJECT_HISTORY.zh-cn.md. -->

## Project Overview
- Tooling project: an OpenCode/Claude "history memo" system that records
  AI-facing project context across sessions.
- Deliverables: a manually-invoked skill (`update-history-memo`), an
  initialization command (`/init-history-memo`), and bilingual context
  templates (`PROJECT_HISTORY.en.md` / `.zh-cn.md`).
- Scope: general development projects — software, hardware, embedded, tooling,
  and mixed.

## Current Status
- Skill, command, and both template files are created and functional.
- Templates live under `template/`; the active context files live in the project
  root.

## Design & Key Decisions
- Split into two independent skills by project nature; this repo implements the
  development-project skill only (general-project skill deferred).
- Bilingual context files distinguished by suffix (`.en` / `.zh-cn`); both must
  stay in sync one-to-one.
- Manual invocation (no auto-trigger); a mandatory human review step precedes
  every write.
- Do not use git for session review; do not auto-modify `AGENTS.md` (suggest only).
- All template sections are optional — fill only what applies, never fabricate.
- Added a final `Others` catch-all section so useful info that fits no section
  is not lost; constrained to stay brief and not become a dumping ground.

## Pitfalls & Lessons Learned
- OpenCode does NOT auto-load `PROJECT_HISTORY.*.md` (only `AGENTS.md` is
  auto-read). To use these as session context, add a line to `AGENTS.md`
  pointing the AI to read `PROJECT_HISTORY.en.md` at session start.
- The shell here is Windows PowerShell 5.1: `&&` is unsupported and `ls -la`
  fails. Use `Get-ChildItem`; date via `Get-Date -Format "yyyy-MM-dd"`.

## Key References & Datasheets
- OpenCode Skills docs: https://opencode.ai/docs/skills/
- OpenCode Commands docs: https://opencode.ai/docs/commands/

## Open Questions
- Possibly author a separate skill for general (non-development) projects.

## Development History

| Date | Summary |
|------|---------|
| 2026-07-02 | Created the `update-history-memo` skill, `/init-history-memo` command, and bilingual `PROJECT_HISTORY` templates. Scoped to general development (software / hardware / embedded / tooling). Added dual PowerShell+bash date commands, a "record only successful approaches" rule, and simplified hardware tips to record rationale only. Renamed project-type label to `hardware`. |
| 2026-07-02 | Added an `Others` catch-all section (with an anti-dumping-ground constraint) across both templates, both root context files, the skill, and the command. |
| 2026-07-06 | Reviewed the skill/command for any effect on the active session's conversation language; confirmed their bilingual wording scopes only the generated `PROJECT_HISTORY.*.md` files, not the chat language. Verified `skills/update-history-memo/SKILL.md` matches the `.opencode/` copy byte-for-byte. Established the directory access convention: `./skills/` and `./commands/` are read/write, `.opencode/` is read-only. |

## Next Steps
- Optionally add a line to `AGENTS.md` so the memo is auto-loaded each session.
- Possibly author a separate skill for general (non-development) projects.

## Conventions & Standards
- Skill file `SKILL.md` written in English; context files bilingual.
- Skill name and command name in lowercase-hyphen form: `update-history-memo`,
  `init-history-memo`.
- Skill/command language scope: bilingual wording inside the skill and command
  governs ONLY the language of generated memo files; it never dictates the
  conversation language of a session.
- Directory access convention for this project: the source dirs `./skills/` and
  `./commands/` are read/write; `.opencode/` holds the installed copy and is
  READ-ONLY.

## Others
<!-- Useful information that does not fit any section above.
     Keep it brief; do not use this as a dumping ground. Promote items to a
     proper section once they clearly belong there. -->
