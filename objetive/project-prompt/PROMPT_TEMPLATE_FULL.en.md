# Prompt Template · Full (for coding agents)

> For larger / more complex projects. Copy the "Template" section, fill in the blanks, and send it to a coding agent that can edit files and run commands.
> For agent prompts, **boundaries and acceptance matter more than "how to implement"**: you state what you want, what's off-limits, and what "done" means — leave the implementation to the agent.

---

## Filling Tips (read these first)

1. **Give real examples, not just descriptions.** One input/output sample > three abstract paragraphs.
2. **Make acceptance criteria verifiable.** Not "make it good"; write "run `pytest`, all pass" / "process 10k rows in < 2s".
3. **Nail down the boundaries.** Scope + permissions + stop conditions + when-to-ask — these four keep the agent from doing harm.
4. **Plan before execute.** For big tasks, tell it to "give a plan, let me confirm, then start" so it doesn't go off track.

---

## Template

```markdown
# Goal
I want to build a <one-line description of what it is> to <problem it solves>.
End user / use case: <who uses it, where>.

# Environment / Stack
- Language & version:
- Framework / key dependencies:
- OS / runtime platform:
- Relevant existing files or dirs: <path, or "this is a brand-new project">

# Requirements
## Must do (hard)
-
-
## Nice to have (bonus)
-
## Explicitly do NOT do (constraints)
-

# Input / Output Example
Input:
​```
<paste a real example>
​```
Expected output:
​```
<paste a real example>
​```

# Acceptance Criteria (what "done" means)
- [ ] Can <run a command / pass tests / meet a metric>
- [ ]

# Boundaries & Collaboration (behavioral constraints for the agent)
- Change scope: only edit <dir/files>, do not touch <which>.
- Permissions: do not delete files, do not git push, do not change config, unless I explicitly agree.
- On architecture / trade-off decisions: stop and ask me, do not decide on your own.
- Work step by step: give a plan for me to confirm before writing.
- After each step, briefly explain what changed.
```

---

## How to Define "Capability Boundaries"

Capability boundary = **scope + permissions + stop conditions + when to ask** — all written explicitly in the "Boundaries & Collaboration" section above:

| Boundary type | How to write it |
|---|---|
| Scope | "Only edit files under `src/`, do not touch `config/`" |
| Permissions | "Do not delete, do not push, do not change git config" |
| Stop condition | "After doing X, stop and ask me; do not auto-continue to Y" |
| Ask-for-help | "On uncertain design choices, ask me before acting" |
| Verification | "Run tests after each change; stop on failure" |

Also remember LLMs' inherent weaknesses: they don't know your private/latest info, they may fabricate non-existent APIs, and long-chain calculations are error-prone.
Mitigations: provide real references, require "say you're unsure instead of guessing", and make it work step by step.
