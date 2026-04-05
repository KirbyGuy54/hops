# hops 🍺

A Homebrew package manager wrapper for macOS, inspired by `paru` for the AUR on Arch Linux. `hops` adds an interactive, paginated search and install experience on top of Homebrew, with install count sorting powered by Homebrew analytics and version tracking.

## Features

- 🔍 **Interactive search** — search for packages and pick one to install from a numbered list
- 📊 **Sorted by popularity** — results sorted by 30-day install count from Homebrew analytics
- 📄 **Paginated results** — navigate through large result sets with `n`/`p`
- 📦 **Version tracking** — displays latest available version for all packages, with up-to-date status (`✓`) or upgrade arrow (`→`) for installed packages
- 🗑️ **Interactive remove** — search installed packages alphabetically and remove interactively
- 📋 **List installed** — view all installed formulae and casks
- ⚡ **Smart caching** — analytics, descriptions, and version data cached for 1 hour to keep things fast
- 🔄 **Throttled updates** — `brew update` is throttled to once every 5 minutes
- 🔧 **Auto-dependency install** — automatically installs `jq` if missing

## Requirements

- macOS
- [Homebrew](https://brew.sh)
- `zsh` (default shell on macOS)
- `jq` (automatically installed on first run if missing)

## Installation

```bash
sudo curl -o /opt/homebrew/bin/hops https://raw.githubusercontent.com/KirbyGuy54/hops/main/hops
sudo chmod +x /opt/homebrew/bin/hops
```

Or manually:

```bash
git clone https://github.com/KirbyGuy54/hops.git
cd hops
sudo cp hops /opt/homebrew/bin/hops
sudo chmod +x /opt/homebrew/bin/hops
```

## Usage

| Command | Description |
|---|---|
| `hops` | Update, upgrade, and cleanup all packages |
| `hops <package>` | Search for and install a package interactively |
| `hops -l`, `--list` | List all installed packages (formulae and casks) |
| `hops -r`, `--remove` | Search installed packages and remove interactively |
| `hops -r <package>` | Remove a specific installed package directly |
| `hops -h`, `--help` | Show help message |

## Examples

**Search and install with version info:**

```
$ hops lazygit

Page 1/1

3. gitui [1.24.2] — Blazing fast terminal-ui for git written in rust (1776 installs)
2. lazygit [0.44.1 ✓] — Simple terminal UI for git commands (26593 installs)
1. git [2.53.0 ✓] — Distributed revision control system (140853 installs)

Pick a number or Ctrl+C to cancel: 2
Installing lazygit...
```

**Version display legend:**
- `[v1.2.3]` — latest available version (not installed)
- `[v1.2.3 ✓]` — installed and up-to-date
- `[v1.2.2 → v1.2.3]` — installed but outdated, upgrade available

**Remove a package:**

```
$ hops -r lazy

1. lazygit

Pick a number to remove (or Ctrl+C to cancel): 1
Removing lazygit...
```

**Full system update:**

```
$ hops
Updating Homebrew...
Upgrading packages...
Cleaning up...
Done!
```

## Cache

`hops` stores cache files in `~/.hops_cache/`:

| File | Contents |
|---|---|
| `analytics_formula.json` | Raw formula analytics from Homebrew API |
| `analytics_cask.json` | Raw cask analytics from Homebrew API |
| `formula_descs.json` | Processed formula descriptions |
| `cask_descs.json` | Processed cask descriptions |
| `formula_counts.json` | Processed formula install counts |
| `cask_counts.json` | Processed cask install counts |
| `formula_versions.json` | Processed formula versions |
| `cask_versions.json` | Processed cask versions |

Cache expires after **1 hour**. To force a refresh, delete the cache:

```bash
rm -rf ~/.hops_cache
```

## Inspiration

Inspired by [`paru`](https://github.com/Morganamilo/paru), the AUR helper for Arch Linux. `hops` brings a similar interactive package management experience to macOS and Homebrew.

## License

GPL-3.0. See [LICENSE](LICENSE) for details.
