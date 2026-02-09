# Ansible Setup for Terminal Applications

This Ansible setup installs a collection of useful terminal applications on a WSL Ubuntu environment.

## Prerequisites

- Ansible installed on your local machine.
- WSL Ubuntu instance.

### Fonts  

Nerd fonts need to be installed in windows to get glyphs to work. Can be downloaded from https://www.nerdfonts.com/font-downloads, e.g. https://github.com/ryanoasis/nerd-fonts/releases/download/v3.4.0/Hack.zip

Install font (probably monospace version), and change font in windows terminal app.

## How to Run

1. Navigate to the `ansible` directory.
2. Run the playbook locally:

   ```bash
   ansible-playbook -i localhost, -c local playbook.yml
   ```

   This provisions the machine you run the command on (your WSL Ubuntu instance).

## What it does

The playbook performs the following actions:

1. Installs prerequisite packages like `build-essential`, `python3-pip`, `golang`, `curl`, and `git`.
2. Installs Node.js (NodeSource repo) and configures the APT repo for 1Password CLI.
3. Installs Rust via `rustup`.
4. Installs additional tools:
   - Downloads and installs `lazygit` and `lazydocker` to `/usr/local/bin`.
   - Installs applications from `apt`, `cargo`, `pip`, `npm`, `go install`, and shell-script/manual installers.
5. Creates symlinks for tools like `fd` (from `fdfind`) and `bat` (from `batcat`) into `~/.local/bin`.
6. Installs `fzf` (from git) and wires up shell integration and aliases in `~/.bashrc`.

## Installed Applications

The exact lists are defined in `roles/terminal_applications/defaults/main.yml`.

### Installed via APT

- lsd
- fd-find (symlinked as `fd`)
- ripgrep
- bat (symlinked as `bat` from `batcat`)
- btop
- dtrx
- tig
- 1password-cli
- nodejs

### Installed via Cargo

- repgrep
- tailspin
- dua-cli
- du-dust (binary `dust`)
- tokei
- zellij
- tealdeer (binary `tldr`)
- clac
- clock-tui
- xh
- atac
- presenterm
- ducker

### Installed via npm (global)

- @google/gemini-cli
- @continuedev/cli

### Installed via Go

- freeze
- vhs

### Installed via shell scripts

- starship
- zoxide
- atuin

### Installed manually

- rip

### Installed from GitHub releases

- lazygit
- lazydocker

### Installed from git source

- fzf

### Shell profile changes

This role *does* modify `~/.bashrc` to enable integrations:

- fzf completion + keybindings
- `eval "$(zoxide init bash)"`
- `eval "$(starship init bash)"`
- `eval "$(atuin init bash)"`
- `~/.local/bin` is added to `PATH`
- aliases: `l`, `la`, `lla`, `lt`, and `ls` -> `lsd`
