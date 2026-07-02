---
name: update-history-memo
description: Summarize the current session's work and update the bilingual PROJECT_HISTORY memo files (PROJECT_HISTORY.en.md and PROJECT_HISTORY.zh-cn.md). Use at the end of a working session for software, hardware, or embedded development projects to record what was done, key decisions, pitfalls, references, and next steps so a future AI session can pick up the context. Always presents a draft for the user to review before writing.
license: MIT
compatibility: opencode
metadata:
  audience: developers
  scope: software-hardware-embedded
---

## What I do

I maintain two AI-facing context memo files that capture the evolving history of a development project:

- `PROJECT_HISTORY.en.md` — English version
- `PROJECT_HISTORY.zh-cn.md` — Simplified Chinese version

These files exist so a future session (AI or human) can quickly understand what
the project is, what has been done, why decisions were made, what to avoid, and
what comes next. I summarize the **current session's** work and propose updates
to both files. The user reviews and approves before anything is written.

This skill applies to **general development projects**:

- Software development
- Hardware design (schematics, PCB, component selection)
- Embedded design (firmware + hardware, register config, peripherals, timing)
- Mixed hardware + software projects
- Tooling development such as this skill itself (skills, agents, commands,
  prompts, and other AI-assistant configuration)

## When to use me

Use me at (or near) the end of a working session, when the user asks to
"update the history", "record this session", "update the memo", or similar.

## Workflow (follow strictly)

1. **Determine the project type** (software / hardware / embedded / tooling / mixed).
   Only populate sections that are actually relevant. All template sections and
   their sub-content are OPTIONAL — omit anything with no substantive content.
   Do not invent content just to fill a section.

2. **Read the existing files**: `PROJECT_HISTORY.en.md` and
   `PROJECT_HISTORY.zh-cn.md`.
   - If they do NOT exist, treat this as first-time initialization: create both
     from the template structure below and fill in what this session establishes.

3. **Get the current date** by running a shell command (do NOT guess the date).
   Pick the command that matches the current shell:
   - PowerShell (Windows):
     ```
     Get-Date -Format "yyyy-MM-dd"
     ```
   - bash / sh (Linux, macOS):
     ```
     date +%F
     ```

4. **Review the current session** by looking back over the conversation and the
   changes made in it. Do NOT use git. Rely on the session's actual work:
   files created/edited, features/circuits/firmware implemented, decisions made,
   problems hit and how they were solved.

5. **Draft the updates**:
   - Update or append only sections that have real, substantive content.
   - Append a new dated row to `Development History` summarizing this session.
   - Append any pitfalls encountered this session to `Pitfalls & Lessons Learned`
     (software pitfalls AND hardware pitfalls: timing, power, register traps,
     pull-up/pull-down, signal integrity, etc.).
   - **Both language versions MUST be updated together and stay in sync** — the
     English and Chinese content must correspond one-to-one (same dated entries,
     same sections, equivalent meaning).

6. **Hardware / embedded recording tips** (apply when relevant):
   - Do NOT log every detailed value or change. Record the *reason* a change was
     made (why a pin/component/register/timing choice was adopted), not an
     exhaustive dump of what changed.
   - For references (datasheets, reference designs, web research), record the
     part number and/or link so it can be found again.

7. **Mandatory review before writing** (this is the whole point — do NOT skip):
   - First, present the FULL proposed content/changes for BOTH files as text in
     your reply so the user can read and review them.
   - Then explicitly ask the user to confirm or request modifications.
   - Only AFTER the user confirms, use the Write/Edit tools to save the files.
   - If the user requests changes, revise the draft and ask again.

8. **AGENTS.md suggestion (do NOT modify it)**:
   - After writing, check whether an `AGENTS.md` exists in the project.
   - If it does (or the user might want one), SUGGEST — but do not apply — adding
     a line instructing the AI to read `PROJECT_HISTORY.en.md` at the start of a
     session, so the memo is actually loaded as context. Never edit `AGENTS.md`
     yourself.

## Template structure (all sections optional)

```
# Project History
<!-- All sections and their sub-content are OPTIONAL. Fill in only what applies
     to this project; omit the rest. This file is written for AI context. -->

## Project Overview
- Goals, project type (software / hardware / embedded), scope

## Current Status
- Overall progress, active branch / milestone / PCB revision

## Environment & Toolchain
- Toolchain, dev board, compiler / EDA versions, programmer/debugger

## Design & Key Decisions
- Software architecture / circuit topology / component selection /
  pin assignment, with rationale
- Known constraints and tradeoffs

## Pitfalls & Lessons Learned
- What went wrong and how it was fixed
- Software pitfalls and hardware pitfalls (timing, power, register traps,
  pull-up/down, signal integrity, etc.)
- Things to avoid; non-obvious gotchas

## Key References & Datasheets
- Chip datasheets, reference designs, docs and web links (with part numbers)

## Open Questions
- Items to confirm or to verify by testing

## Development History
| Date | Summary |
|------|---------|
| YYYY-MM-DD | ... |

## Next Steps
- Planned tasks; blocked items

## Conventions & Standards
- Naming rules, versioning, net-label conventions, code style, etc.

## Others
- Useful information that does not fit any section above. Keep it brief;
  do not use this as a dumping ground. Promote items to a proper section
  once they clearly belong there.
```

## Hard rules

- Do NOT use git.
- Do NOT guess the date — always read it from the shell.
- Keep the English and Chinese files in sync.
- Record only the SUCCESSFUL / final approach. Strip out failed attempts, dead
  ends, and their reasoning so they do not pollute future context. The one
  exception: if a failed approach yields a durable "what to avoid" lesson, put a
  brief note in `Pitfalls & Lessons Learned` — but never carry over the failed
  logic itself.
- NEVER write the files before the user has reviewed and confirmed the draft.
- Do NOT modify `AGENTS.md`; only suggest changes.
- All sections are optional — never fabricate content to fill them.
