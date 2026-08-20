# AGENTS.md

This is a flat collection of standalone quality-of-life executables in `src/`, installed into `~/.local/bin`. No build, no test suite, no package. Each file in `src/` is self-contained and independently runnable — there is no shared library, and scripts never source or import each other.

`README.md` holds a one-line summary per executable. Adding or removing a script means updating that table.

## Commands

```bash
mise run install                    # copy all of src/ into ~/.local/bin
mise run install --symlink          # symlink instead (for local iteration)
mise run install <name> [<name>...] # just these
```

Run a script directly from `src/` to test it: `./src/pdf-watermark --help`. Python scripts resolve their own dependencies through `uv` on first run.

## Script conventions

Two flavors, both marked executable (`chmod +x`) and both starting with `# -*- coding: utf-8 -*-` plus the author/copyright pair.

**Bash** — `#!/usr/bin/env bash`, then:

- `set -euo pipefail` and `IFS=$'\n\t'`
- A `## Usage: ...` / `## Options:` comment block that doubles as help text, printed by a `usage()` function that greps it back out of `$0` (`sed -n '/^##/,/^$/s/^## \{0,1\}//p' "$0"`)
- Hand-rolled `while [[ "$1" =~ ^- ... ]]; case $1 in` option loop, uppercase globals for parsed values
- Tab indentation; `# === Section ===` banners separating phases

**Python** — `#!/usr/bin/env -S uv run --script` with a PEP 723 `# /// script` inline metadata block declaring `requires-python` and `dependencies`. Prefer `typer` for the CLI (`typer.run(main)` for a single command, `typer.Typer(no_args_is_help=True)` when subcommands or richer help are wanted); `argparse` is acceptable for a script with no other dependencies to justify typer. Errors print to `stderr` and exit via `typer.Exit(<code>)` with a meaningful non-zero status. 4-space indentation.

Distinct exit codes carry meaning (e.g. `ecs-tail`: 1 bad args, 2 timeout, 3 container failure) — keep that habit.

## Commit style

`type(scope): Subject` where scope is the executable name, e.g. `feat(pdf-watermark): New executable`, `fix(git-amend): Stash to allow rebasing`. Repo-wide changes drop the scope.
