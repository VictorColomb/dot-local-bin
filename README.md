# ~/.local/bin

This repository contains a number of quality-of-life executables, that one can
easily install by moving them into / symlink them from `~/.local/bin`.

| Executable | Summary |
| --- | --- |
| `cloudwatch-tail` | Tail a CloudWatch log group/stream, stripping the timestamp prefix; optionally filter JSON output with a jq expression |
| `ecr-build-push` | Build a Docker image, push it to ECR (tagged with the current git SHA), register a new ECS task definition revision, and optionally update an ECS service |
| `ecs-tail` | Tail the CloudWatch logs of all containers in a running ECS task and wait for it to finish, reporting each container's exit code |
| `elasticache-password` | Generate a short-lived IAM-authenticated password for an ElastiCache Valkey cluster |
| `git-amend` | Amend the latest commit in-place, or create a fixup commit for an older ref and immediately autosquash it |
| `git-main` | Switch to the main branch, pull the latest changes, and prune stale local branches |
| `git-wt` | Interactively create, open, or delete git worktrees using fzf; opens the result in Zed or VS Code |
| `pdf-watermark` | Overlay a diagonal semi-transparent text watermark on every page of a PDF |
| `pg-delete-from-table` | Delete all rows from a PostgreSQL table in configurable batches, with optional primary-key range bounds |
| `pg-update-table` | Set a column to a fixed value across an entire PostgreSQL table in configurable batches, with optional primary-key range bounds |
| `valkey-flush` | Scan an ElastiCache Valkey cluster and delete all keys whose name matches a regex, with dry-run support |

## ⬇️ Install

- Install [mise]
- Install [uv]

### Using [mise] (recommended)

```shell
mise run install

# Or, using symlink instead of copy
mise run install --symlink

# Just the one executable
mise run install <executable-name>
```

### Manually

```shell
for file in src/*; do \
  cp -f "$file" "$HOME/.local/bin/$(basename "$file")"; done

# Or, symlink
for file in src/*; do \
  ln -sf "$(realpath "$file")" "$HOME/.local/bin/$(basename "$file")"; done
```

## 🏗️ Development

### New executable

Create a new file in `src/`, add a shebang at the top of it and make it executable.

```shell
cat >src/my-new-executable <<EOF
#!/usr/bin/env bash
EOF

chmod +x src/my-new-executable
git add src/my-new-executable
```

[mise]: https://mise.jdx.dev
[uv]: https://docs.astral.sh/uv
