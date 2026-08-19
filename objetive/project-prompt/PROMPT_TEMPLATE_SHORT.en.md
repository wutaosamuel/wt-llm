# Prompt Template · Short (for coding agents)

> For everyday small tasks. Copy the whole block below, fill in the blanks, and send it to a coding agent that can edit files.
> Keys: give real examples, make acceptance criteria verifiable, state the boundaries clearly.

---

## Goal
I want to build a <one-line description of what it is> to <problem it solves>.

## Environment / Stack
- Language & version:
- Framework / key dependencies:
- Platform / existing files: <path, or "brand-new project">

## Requirements
- Must do:
- Do NOT do (constraints):

## Input / Output Example
Input:
```
<real example>
```
Expected output:
```
<real example>
```

## Acceptance Criteria + Boundaries
- Done means: <runs a command / passes tests / meets a metric>
- Boundaries: only edit <dir/files>; do not delete, do not push; if unsure, ask me first instead of deciding on your own.
