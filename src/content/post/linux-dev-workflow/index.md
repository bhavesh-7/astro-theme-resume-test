---
title: "Designing a Linux-First Development Workflow"
description: "How I structured a distraction-free, keyboard-driven environment using Hyprland, Neovim, Lazy.nvim, Ghostty, and tmux for high-speed development"
publishDate: "18 Feb 2026"
tags: ["linux", "workflow", "neovim", "hyprland", "productivity", "dotfiles"]
coverImage:
  src: "./cover.png"
  alt: "Linux development workflow with Hyprland and Neovim"
---

## Why Linux-First?

After years of experimenting with different development environments, I've settled on a Linux-first workflow that prioritizes speed, keyboard-driven navigation, and minimal distractions. This setup has transformed how I code, making context switching nearly instant and keeping me in the flow state longer.

## The Stack

My development environment is built on four core components:

- **Hyprland** - Dynamic tiling Wayland compositor
- **Ghostty** - GPU-accelerated terminal emulator
- **tmux** - Terminal multiplexer for session management
- **Neovim** - Modal text editor with Lazy.nvim plugin manager

## Hyprland: The Foundation

[Hyprland](https://hyprland.org/) is a dynamic tiling Wayland compositor that provides smooth animations, powerful window management, and extensive customization. Unlike traditional desktop environments, Hyprland is keyboard-first by design.

### Why Hyprland?

- **Tiling by default** - Windows automatically organize themselves
- **Wayland native** - Better performance and security than X11
- **Smooth animations** - Makes window management feel natural
- **Highly configurable** - Every keybinding and behavior is customizable

### Key Features I Use

```bash
# Workspace switching (Super + 1-9)
bind = SUPER, 1, workspace, 1
bind = SUPER, 2, workspace, 2

# Move windows between workspaces
bind = SUPER SHIFT, 1, movetoworkspace, 1

# Window focus (Vim-style)
bind = SUPER, h, movefocus, l
bind = SUPER, l, movefocus, r
bind = SUPER, k, movefocus, u
bind = SUPER, j, movefocus, d
```

I organize workspaces by context:
- Workspace 1: Code (Neovim + tmux)
- Workspace 2: Browser (documentation, testing)
- Workspace 3: Communication (Discord, Matrix)
- Workspace 4: System monitoring

## Ghostty: The Terminal

[Ghostty](https://ghostty.org/) is a GPU-accelerated terminal emulator that's blazingly fast and highly configurable. It handles rendering with ease, even with complex tmux layouts and Neovim UI elements.

### Why Ghostty?

- **GPU acceleration** - Smooth scrolling and rendering
- **Native performance** - Written in Zig for speed
- **True color support** - Beautiful syntax highlighting
- **Ligature support** - Programming fonts look great

### Configuration Highlights

```conf
# Font configuration
font-family = "JetBrainsMono Nerd Font"
font-size = 12

# Theme
theme = "catppuccin-mocha"

# Performance
shell-integration = true
```

## tmux: Session Management

[tmux](https://github.com/tmux/tmux) is the glue that holds my terminal workflow together. It provides session persistence, window management, and the ability to detach/reattach sessions.

### My tmux Workflow

```bash
# Create project-specific sessions
tmux new -s project-name

# Split panes for different tasks
Ctrl-b %  # Vertical split
Ctrl-b "  # Horizontal split

# Navigate panes (Vim-style)
Ctrl-b h/j/k/l
```

### Key Configuration

```bash
# Remap prefix to Ctrl-a
set -g prefix C-a
unbind C-b

# Enable mouse support
set -g mouse on

# Start windows at 1, not 0
set -g base-index 1
setw -g pane-base-index 1

# Vi mode for copy
setw -g mode-keys vi
```

I use tmux sessions for different projects, making it easy to switch contexts without losing my place.

## Neovim: The Editor

[Neovim](https://neovim.io/) with [Lazy.nvim](https://github.com/folke/lazy.nvim) is the heart of my development workflow. It's fast, extensible, and once you learn the keybindings, incredibly efficient.

### Why Neovim + Lazy.nvim?

- **Modal editing** - Different modes for different tasks
- **Lazy loading** - Plugins load only when needed
- **LSP integration** - Native language server support
- **Extensible** - Lua configuration is powerful and fast
- **Community** - Massive plugin ecosystem

### Essential Plugins

```lua
-- Plugin manager
require("lazy").setup({
  -- File explorer
  "nvim-tree/nvim-tree.lua",
  
  -- Fuzzy finder
  "nvim-telescope/telescope.nvim",
  
  -- LSP configuration
  "neovim/nvim-lspconfig",
  
  -- Autocompletion
  "hrsh7th/nvim-cmp",
  
  -- Syntax highlighting
  "nvim-treesitter/nvim-treesitter",
  
  -- Git integration
  "lewis6991/gitsigns.nvim",
  
  -- Status line
  "nvim-lualine/lualine.nvim",
})
```

### My Workflow

1. **Open project** - `nvim .` in project root
2. **Find files** - `<leader>ff` (Telescope)
3. **Search text** - `<leader>fg` (Telescope grep)
4. **Navigate code** - LSP go-to-definition, references
5. **Git operations** - Gitsigns for hunks, Fugitive for commits

## Dotfiles Management with GNU Stow

The secret to maintaining this setup across multiple machines and distros is [GNU Stow](https://www.gnu.org/software/stow/). It's a symlink farm manager that makes dotfiles management trivial.

### Why Stow?

- **Simple** - Just symlinks, no complex scripts
- **Selective** - Install only what you need
- **Reversible** - Easy to unstow configurations
- **Distro-agnostic** - Works everywhere

### My Dotfiles Structure

```
~/dotfiles/
├── hyprland/
│   └── .config/
│       └── hypr/
├── ghostty/
│   └── .config/
│       └── ghostty/
├── tmux/
│   └── .tmux.conf
├── nvim/
│   └── .config/
│       └── nvim/
├── zsh/
│   └── .zshrc
└── scripts/
    └── scripts/
```

### Using Stow

Install configurations:

```bash
cd ~/dotfiles

# Install specific config
stow nvim
stow tmux
stow hyprland

# Install everything
stow */
```

Remove configurations:

```bash
# Remove specific config
stow -D nvim

# Remove everything
stow -D */
```

### Distro Hopping Made Easy

When switching distros, my setup process is:

1. **Install base system**
2. **Clone dotfiles** - `git clone https://github.com/bhavesh-7/dotfiles ~/dotfiles`
3. **Install dependencies** - Hyprland, Neovim, tmux, Ghostty, stow
4. **Stow configs** - `cd ~/dotfiles && stow */`
5. **Done** - Fully configured environment in minutes

No manual copying, no broken symlinks, no missing configs. Everything just works.

## The Complete Workflow

Here's how it all comes together:

1. **Boot into Hyprland** - Instant login to tiling compositor
2. **Launch Ghostty** - GPU-accelerated terminal
3. **Start tmux session** - `tmux new -s project`
4. **Open Neovim** - `nvim .` in project directory
5. **Code** - Everything is keyboard-driven, no mouse needed

### Typical Development Session

```bash
# Create new project session
tmux new -s myproject

# Split terminal
Ctrl-a %  # Vertical split for code + terminal

# Left pane: Neovim
nvim .

# Right pane: Development server
npm run dev

# Switch between panes with Ctrl-a h/l
# Switch workspaces with Super + 1-9
# Everything stays running, even if I disconnect
```

## Benefits of This Setup

### Speed

- **No mouse** - Keyboard navigation is faster
- **Instant context switching** - Workspaces and tmux sessions
- **Fast startup** - Everything loads in milliseconds
- **GPU acceleration** - Smooth rendering everywhere

### Focus

- **Minimal distractions** - No notification popups or animations
- **Full screen** - Tiling maximizes screen real estate
- **Single task** - One workspace, one focus
- **Flow state** - Stay in the zone longer

### Portability

- **Dotfiles in git** - Version controlled configuration
- **Stow for deployment** - Install anywhere in seconds
- **Distro agnostic** - Works on Fedora, Arch, Ubuntu, Debian
- **Session persistence** - tmux keeps everything running

## Getting Started

Want to try this workflow? Here's how:

### 1. Install Dependencies

```bash
# Fedora
sudo dnf install hyprland neovim tmux stow

# Arch
sudo pacman -S hyprland neovim tmux stow

# Ubuntu (Hyprland requires PPA or build from source)
sudo apt install neovim tmux stow
```

### 2. Install Ghostty

Follow instructions at [ghostty.org](https://ghostty.org/)

### 3. Clone My Dotfiles

```bash
git clone https://github.com/bhavesh-7/dotfiles ~/dotfiles
cd ~/dotfiles
```

### 4. Stow Configurations

```bash
# Start with basics
stow zsh
stow tmux
stow nvim

# Add Hyprland when ready
stow hyprland
```

### 5. Learn the Keybindings

- **Hyprland** - Super key for everything
- **tmux** - Ctrl-a prefix (or Ctrl-b default)
- **Neovim** - Start with `vimtutor`, then customize

## Tips for Beginners

1. **Start small** - Don't install everything at once
2. **Learn one tool** - Master tmux before adding Neovim
3. **Customize gradually** - Copy configs, then modify
4. **Use cheatsheets** - Keep keybindings handy
5. **Be patient** - Modal editing has a learning curve

## Conclusion

This Linux-first workflow has made me a faster, more focused developer. The keyboard-driven nature keeps me in flow, the tiling window manager maximizes screen space, and the dotfiles management with Stow makes it portable across machines.

If you're tired of slow, mouse-heavy development environments, give this setup a try. It takes time to learn, but the productivity gains are worth it.

## Resources

- [My Dotfiles](https://github.com/bhavesh-7/dotfiles)
- [Hyprland Wiki](https://wiki.hyprland.org/)
- [Neovim Documentation](https://neovim.io/doc/)
- [tmux Cheat Sheet](https://tmuxcheatsheet.com/)
- [GNU Stow Manual](https://www.gnu.org/software/stow/manual/)

---

*This entire blog post was written in Neovim, inside tmux, running in Ghostty, on Hyprland. The workflow works.*
