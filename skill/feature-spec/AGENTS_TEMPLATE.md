# `AGENTS.md` Template for Python and Go Script Projects

Use this as a starting point for a project-level `AGENTS.md`. Replace every
placeholder with verified project facts. Keep only the language section(s) that
apply, and remove rules or tools the project does not use.

```markdown
# Project rules

## Project facts
- Language and version: <Python 3.x | Go 1.xx> (source: <pyproject.toml | go.mod>)
- Entry points: <e.g. scripts/foo.py, cmd/foo/main.go>
- Supported OS: <Windows / Linux / macOS / other verified platforms>
- Test command: <verified project command>
- Lint/format/type-check commands: <only tools already configured>

## Specification and business rule compliance
- Before implementing from a specification, read the complete specification,
  including its business rules and change-control section.
- Do not change, weaken, remove, or reinterpret confirmed business rules to fit
  existing code, technical constraints, or implementation convenience.
- If a business rule conflicts with another requirement, existing code, an
  interface, a library, the platform, or another technical constraint, stop the
  affected work. Report the conflicting items and sources, explain the impact,
  present options and trade-offs, and wait for the user's explicit decision.
- Silence or an ambiguous instruction to proceed is not approval. If the user
  cannot be asked, report the blocker instead of choosing an option.
- Do not hide a conflict by changing tests, acceptance criteria, defaults,
  fallbacks, or placeholder behavior. Change tests only to accurately verify
  the approved specification, not to weaken it.
- Continue only work that does not depend on a pending decision. Report which
  work is paused and which continues.
- Do not implement parts of a specification marked "Draft - decisions needed"
  that are affected by its blocking decisions.

## Script contract
- Treat command-line arguments, environment variables, configuration formats,
  stdout/stderr output formats, output files, and exit codes as public
  interfaces. Do not change them unless the user or approved specification
  requires it.
- Preserve the project's existing stdout/stderr conventions. If none exist,
  keep machine-readable output on stdout and diagnostics on stderr.
- Preserve the project's exit-code conventions. If none exist, use zero for
  success and non-zero for failure; do not swallow errors.
- Handle paths containing spaces and non-ASCII characters. Do not hard-code
  absolute or user-specific paths.
- Do not add destructive operations (such as deleting, overwriting, or writing
  outside the project) without an explicit requirement. Preserve existing
  confirmation and dry-run behavior.
- Never hard-code or log secrets, tokens, or passwords.

## Dependencies and toolchain
- Follow the language and toolchain versions declared by the project.
- Do not add, remove, or upgrade dependencies, or change language/toolchain
  versions, without user approval.
- Prefer the standard library when it meets the approved requirements.

## Python (keep only for Python projects)
- Follow the Python version declared by the project; do not use unsupported
  syntax or modules.
- Use the existing environment and dependency files; do not install packages
  globally.
- Open text files with an explicit encoding (normally `encoding="utf-8"`);
  use `pathlib` for filesystem paths.
- Put executable behavior behind `if __name__ == "__main__":` so modules can
  be imported in tests.
- Use the CLI library already present in the project (for example,
  `argparse`, `click`, or `typer`); do not switch without approval.
- Handle expected failures specifically; do not use bare `except:` or silently
  ignore errors.
- Add type hints to new public functions if that matches existing project
  conventions.

## Go (keep only for Go projects)
- Follow the Go version in `go.mod`; do not edit `go.mod` or `go.sum` except for
  approved dependency or toolchain changes.
- Format Go code with `gofmt`; run `go vet ./...` if configured or required by
  the project.
- Return errors rather than panicking for expected failures; wrap errors with
  context using `%w` when appropriate.
- Keep logic in testable functions; use `os.Exit` only at the process boundary
  when needed.
- Propagate `context.Context` for cancellable or network operations and avoid
  goroutine leaks.
- Use `filepath` for operating-system paths and handle Windows path semantics
  when Windows is supported.

## Verification
- Add or update tests for changed behavior and map them to specification
  acceptance-criterion IDs where available.
- Run the configured test, lint, and format-check commands relevant to changed
  code.
- Report exactly which commands were run and their results. Do not claim a
  command was run or passed if it was not; identify checks that could not be
  run and why.
```

## Writing Notes

1. **Verify project facts.** Record versions and commands from files such as
   `pyproject.toml`, `requirements.txt`, `go.mod`, CI workflows, or existing
   project documentation. Mark anything unverified instead of guessing.
2. **Keep only applicable sections.** A Python-only project should not carry Go
   rules, and vice versa. For a mixed project, retain both language sections.
3. **List only configured tools.** Do not prescribe `pytest`, `ruff`, `mypy`,
   `golangci-lint`, or other tools unless the project actually uses them or the
   user has approved adding them. Otherwise an agent may install tools or add
   configuration unnecessarily.
4. **Preserve established contracts.** Do not impose generic stdout, stderr,
   exit-code, CLI, or dry-run behavior if the project already has a different
   convention. Document the verified convention and preserve it.
5. **Treat scripts as interfaces.** Arguments, environment variables, config
   formats, output files, output formats, and exit codes may be consumed by
   other scripts or CI. Change them only when explicitly required and approved.
6. **Account for real path and encoding requirements.** In particular, test
   paths with spaces on supported platforms. Specify text encoding explicitly
   where relevant; do not assume every script runs under the same locale.
7. **Keep the file concise and project-wide.** `AGENTS.md` should contain rules
   that apply across the project. Put feature-specific behavior in its
   specification, and move extensive specialized workflows into a separate
   skill if one becomes necessary.
8. **Avoid rules that cause unapproved scope expansion.** A format, lint, or
   type-check command should not imply permission to add that tool or reformat
   unrelated files.
