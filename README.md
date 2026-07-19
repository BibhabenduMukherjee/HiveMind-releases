# HiveMind

A fast, cost-optimized coding agent for DeepSeek. This repo distributes
pre-built binaries only — there's no source here, and none is required to
install or run it.

Free while pricing is undecided.

## Install

```sh
curl -fsSL https://raw.githubusercontent.com/BibhabenduMukherjee/HiveMind-releases/main/install.sh | bash
```

This detects your OS/architecture, downloads the matching binary from the
[latest release](https://github.com/BibhabenduMukherjee/HiveMind-releases/releases/latest),
and installs it to `~/.local/bin` (override with `HARNESS_INSTALL_DIR`).

Or download a binary directly from the
[releases page](https://github.com/BibhabenduMukherjee/HiveMind-releases/releases)
for your platform: macOS (Intel/Apple Silicon), Linux (x86_64/aarch64), or
Windows (x86_64).

## Run

```sh
export DEEPSEEK_API_KEY=sk-...

harness                              # interactive REPL, starts on Flash
harness -p "summarize src/main.rs"   # headless one-shot
harness --tier pro                   # start on the stronger tier
```

## Configuration

No config file is required. To customize models, thresholds, or a proxy
`base_url`, create `~/.config/harness/config.toml`:

```toml
[deepseek]
# api_key = "sk-..."        # prefer $DEEPSEEK_API_KEY
# base_url = "https://api.deepseek.com"
# flash_model = "deepseek-v4-flash"
# pro_model = "deepseek-v4-pro"

[agent]
default_tier = "flash"              # "flash" | "pro"
max_turns = 25
compaction_threshold_percent = 75
auto_escalate = true
escalate_after_repeats = 2
```

## Flags

| Flag | Meaning |
|---|---|
| `-p, --prompt` | Run one prompt headlessly (auto-approves shell), then exit. |
| `--workdir` | Workspace root. Default `.`. |
| `--config` | Config file path. Default `~/.config/harness/config.toml`. |
| `--tier` | Start on `flash` (default) or `pro`. |
| `--api-key` / `--base-url` | Override resolved endpoint. |
| `--yolo` | Auto-approve all shell commands. Off by default. |
| `--show-reasoning` | Print streamed chain-of-thought (deepseek-v4-pro). |

## Tools

Four built-ins, all workspace-confined (`--workdir`, default `.`):
`read_file`, `write_file`, `list_dir`, and `run_shell` (interactive `[y/N]`
approval by default; `--yolo` or headless `-p` mode auto-approves).

## License

MIT — see [LICENSE](LICENSE).
