# ~/.local/bin

This repository contains a number of quality-of-life executables, that one can
easily install by moving them into / symlink them from `~/.local/bin`.

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
