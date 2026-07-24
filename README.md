# HiveMind

A fast, cost-optimized AI coding agent. This repo distributes pre-built
binaries only — there's no source here, and none is required to install or
run it.

Sign in and pay as you go with no account of your own to manage, or bring
your own HiveMind API key — see [Run](#run).

## Install

**macOS / Linux:**

```sh
curl -fsSL https://raw.githubusercontent.com/BibhabenduMukherjee/HiveMind-releases/main/install.sh | bash
```

Installs to `~/.local/bin` (override with `HIVEMIND_INSTALL_DIR`).

**Windows (PowerShell):**

```powershell
irm https://raw.githubusercontent.com/BibhabenduMukherjee/HiveMind-releases/main/install.ps1 | iex
```

Installs to `%LOCALAPPDATA%\hivemind` (override with `$env:HIVEMIND_INSTALL_DIR`) and
adds it to your user `PATH` — open a **new** PowerShell window afterward for that to
take effect.

Both scripts detect your OS/architecture and download the matching binary from the
[latest release](https://github.com/BibhabenduMukherjee/HiveMind-releases/releases/latest).

Or download a binary directly from the
[releases page](https://github.com/BibhabenduMukherjee/HiveMind-releases/releases)
for your platform: macOS (Intel/Apple Silicon), Linux (x86_64/aarch64), or
Windows (x86_64).

> **`hivemind` is a command-line tool, not a desktop app.** Run it from a
> terminal (PowerShell on Windows, Terminal on macOS/Linux) — double-clicking
> `hivemind.exe`/`hivemind` in a file browser opens a console window and closes
> it again the instant the program exits, which looks like a crash but isn't
> one.

## Run

No account of your own? Sign in with Google and pay as you go:

```sh
hivemind auth login      # prints a code + URL, approve it in your browser
hivemind auth status     # check who's signed in and your balance
hivemind auth logout     # remove the stored credential

hivemind activate                              # interactive REPL, starts on Flash
```

Or bring your own HiveMind API key:

```sh
export HIVEMIND_API_KEY=...

hivemind activate                              # interactive REPL, starts on Flash
hivemind activate -p "summarize src/main.rs"   # headless one-shot
hivemind activate --tier pro                   # start on the stronger tier
```

If both are set, an explicit key (flag, config file, or `$HIVEMIND_API_KEY`) always
wins over a signed-in hosted session.

## Configuration

No config file is required. To customize models, thresholds, or a proxy
`base_url`, create `~/.config/hivemind/config.toml`:

```toml
[model]
# api_key = "..."           # prefer $HIVEMIND_API_KEY
# base_url = "..."          # only needed to point at a proxy or mock

[agent]
default_tier = "flash"              # "flash" | "pro"
max_turns = 25
compaction_threshold_percent = 75
auto_escalate = true
escalate_after_repeats = 2
```

## Flags

All of these are flags on `hivemind activate`, e.g. `hivemind activate --tier pro`.

| Flag | Meaning |
|---|---|
| `-p, --prompt` | Run one prompt headlessly (auto-approves shell), then exit. |
| `--workdir` | Workspace root. Default `.`. |
| `--config` | Config file path. Default `~/.config/hivemind/config.toml`. |
| `--tier` | Start on `flash` (default) or `pro`. |
| `--api-key` / `--base-url` | Override resolved endpoint. |
| `--yolo` | Auto-approve all shell commands. Off by default. |
| `--show-reasoning` | Print streamed chain-of-thought (Pro tier only). |

## Tools

Seven built-ins, all workspace-confined (`--workdir`, default `.`):
`read_file`, `write_file`, `edit_file`, `list_dir`, `search`,
`semantic_search`, and `run_shell` (interactive `[y/N]` approval by
default; `--yolo` or headless `-p` mode auto-approves).

## License

MIT — see [LICENSE](LICENSE).
