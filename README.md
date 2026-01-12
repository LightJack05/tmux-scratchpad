# tmux-scratchpad

A tool to quickly create scratchpad directories from tmux and start sessions in them.

## Features

- 🎯 Interactive scratchpad name input using `gum` in a tmux popup
- 📁 Automatically creates directories under a configurable base path
- 🔄 Reuses existing directories and sessions
- ⚡ Fast session switching with tmux
- ⚙️ Configurable base path and optional shell command execution

## Dependencies

- `tmux` - Terminal multiplexer
- `gum` - A tool for glamorous shell scripts ([charmbracelet/gum](https://github.com/charmbracelet/gum))

## Installation

1. Clone this repository or download the `tmux-scratchpad` script
2. Make it executable: `chmod +x tmux-scratchpad`
3. Place it in your PATH (e.g., `~/.local/bin/` or `/usr/local/bin/`)
4. Ensure dependencies are installed

Install `gum`:
```bash
# On macOS
brew install gum

# On Linux (using go)
go install github.com/charmbracelet/gum@latest

# For other installation methods, see: https://github.com/charmbracelet/gum#installation
```

## Usage

```bash
# Interactive mode - prompts for scratchpad name
tmux-scratchpad

# Direct mode - specify scratchpad name as argument
tmux-scratchpad my-project

# Show help
tmux-scratchpad --help
```

## Configuration

Create a configuration file at `~/.config/tmux-scratchpad/config`:

```bash
# Base directory for scratchpad folders (default: $HOME/scratchpad)
SCRATCHPAD_BASE_PATH="$HOME/scratch"

# Optional command to execute in the shell (e.g., "zsh" or "bash")
SHELL_COMMAND="zsh"
```

Or copy the example configuration file:

```bash
mkdir -p ~/.config/tmux-scratchpad
cp config.example ~/.config/tmux-scratchpad/config
# Then edit the config file with your preferred settings
```

## How It Works

1. **Get Name**: Prompts for a scratchpad directory name using `gum input` in a tmux popup (or uses the provided argument)
2. **Create Directory**: Creates the directory under `SCRATCHPAD_BASE_PATH` if it doesn't exist
3. **Reuse Existing**: If the directory already exists, uses it in-place
4. **Session Management**: 
   - If a tmux session for this scratchpad exists, switches to it
   - Otherwise, creates a new session and switches to it
5. **Optional Command**: If `SHELL_COMMAND` is configured, executes it in the new session

## Examples

### Basic Usage

```bash
# Run interactively - will show popup asking for name
tmux-scratchpad
```

### Direct Usage

```bash
# Create/open scratchpad named "meeting-notes"
tmux-scratchpad meeting-notes

# Create/open scratchpad named "quick-test"
tmux-scratchpad quick-test
```

### Bind to Tmux Key

Add to your `~/.tmux.conf`:

```tmux
# Bind Ctrl-g to launch tmux-scratchpad
bind-key -n C-g run-shell "tmux-scratchpad"
```

## Similar Tools

This tool is part of a family of tmux session management tools:

- [tmux-git-finder](https://github.com/LightJack05/tmux-git-finder) - Find and open git repositories in tmux sessions
- [tmux-nix-finder](https://github.com/LightJack05/tmux-nix-finder) - Find and open Nix projects in tmux sessions

## License

MIT
