---
description: Initialize the bilingual PROJECT_HISTORY memo files for a development project
---

Initialize the AI-facing project history memo files for this project.

This project may be a **software**, **hardware**, **embedded** design, or
a **tooling** project (skills, agents, commands) — or a mix. Follow these steps:

1. **Analyze the project** to understand what it is: read the directory
   structure, any `README`, existing docs, source/schematic files, and config.
   Determine the project type and only include sections that are relevant.

2. **Get the current date** from the shell (do NOT guess). Use the command that
   matches the current shell:
   - PowerShell (Windows): `Get-Date -Format "yyyy-MM-dd"`
   - bash / sh (Linux, macOS): `date +%F`

3. **Draft two files** using the template below — one English, one Chinese —
   keeping their content in sync (one-to-one correspondence):
   - `PROJECT_HISTORY.en.md`
   - `PROJECT_HISTORY.zh-cn.md`

   Fill in ONLY what you can confidently determine about the project right now.
   All sections and sub-content are OPTIONAL — leave out or leave blank anything
   you cannot determine. Do not fabricate content.

4. **Review before writing**: present the full proposed content of BOTH files as
   text and ask the user to confirm or request changes. Only write the files
   after the user confirms.

5. **AGENTS.md suggestion**: after writing, if an `AGENTS.md` exists (or might be
   useful), SUGGEST adding a line telling the AI to read `PROJECT_HISTORY.en.md`
   at the start of a session. Do NOT modify `AGENTS.md` yourself.

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
