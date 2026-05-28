# claude-custom

A drop-in replacement for the built-in `claude` agent that supports injecting static files into the sandbox via the `files/` directory — something the built-in kit doesn't expose.

## Usage

```console
$ sbx run --kit ./claude-custom/ claude-custom
```

Or from this repo:

```console
$ sbx run --kit "git+https://github.com/docker/sbx-kits-contrib.git#dir=claude-custom" claude-custom
```

**Prerequisites:** `ANTHROPIC_API_KEY` must be set on the host.

## Customizing

Edit the files under `files/home/.claude/` before running:

| File | Purpose |
| --- | --- |
| `files/home/.claude/CLAUDE.md` | Global instructions applied to every project in the sandbox |
| `files/home/.claude/settings.json` | Claude Code settings (permissions, hooks, etc.) |

Both files are written to `~/.claude/` inside the sandbox at startup.

## How it works

This kit mirrors the built-in `claude` agent spec exactly, adding only the `files/` directory. The proxy injects the host's `ANTHROPIC_API_KEY` into outgoing `x-api-key` headers — the key never lives inside the VM.
