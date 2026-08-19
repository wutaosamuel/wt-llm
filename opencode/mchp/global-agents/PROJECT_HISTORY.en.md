# Project History

## Project Overview
- This folder (`opencode/mchp/global-agents`) hosts the global `AGENTS.md`
  rules intended for OpenCode, targeted at Microchip MCU development
  workflows (MPLAB X IDE and the MPLAB X VS Code extension).
- Project type: tooling / AI-assistant configuration.

## Design & Key Decisions
- Top-level heading of `AGENTS.md` is `# WorkStation rules`, so that future,
  unrelated rule sets (other tools/environments) can be added as sibling
  `##` sections without restructuring the file.
- MPLAB X project detection rule: treat the environment as an MPLAB X
  project if the current working directory name ends with `.X`, OR if the
  current working directory contains a subdirectory ending with `.X`.
- Protection scope for `mcc_generated_files`: limited to the
  `mcc_generated_files` directory found directly under the `.X` project
  root (not any arbitrarily nested directory with the same name), but the
  restriction covers the entire subtree of files under it.
- Enforcement mechanism: before editing/creating/deleting any file under
  `mcc_generated_files/`, the assistant must ask the user for confirmation
  every single time (no session-level "already approved" carry-over),
  because MCC regeneration can silently overwrite manual edits.
- Content language: written in English (the file is consumed by the LLM,
  not end users), per user's choice.

## Development History
| Date | Summary |
|------|---------|
| 2026-08-19 | Created `AGENTS.md` in `opencode/mchp/global-agents` with a `WorkStation rules` top-level section, containing MPLAB X project detection rules and a policy that protects `mcc_generated_files` from unconfirmed edits. |

## Next Steps
- Consider adding more `##` sections under `WorkStation rules` for other
  Microchip tools/environments as needed (e.g. other IDEs, build systems).

## Others
- This file lives in `opencode/mchp/global-agents`, separate from the
  repo-root history (if any), scoped specifically to this rules folder.
