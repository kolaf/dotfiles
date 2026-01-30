# Ansible Setup for Terminal Applications

This Ansible setup installs a collection of useful terminal applications on a WSL Ubuntu environment.

## Prerequisites

- Ansible installed on your local machine.
- WSL Ubuntu instance.

## How to Run

1.  Navigate to the `ansible` directory.
2.  Run the playbook:

    ```bash
    ansible-playbook -i inventory playbook.yml
    ```

    The playbook will run on your localhost and connect to it directly, so it will provision the machine you are running the command from. Make sure you run this inside your WSL Ubuntu instance.

## What it does

The playbook performs the following actions:

1.  Installs prerequisite packages like `build-essential`, `python3-pip`, `golang`, `curl`, and `git`.
2.  Installs Rust via `rustup`.
3.  Installs applications from various sources:
    -   `apt` package manager (including adding a PPA for `lazygit`).
    -   `cargo` (Rust's package manager).
    -   `pip` (Python's package manager).
    -   `go install`.
    -   Custom installation scripts.
    -   Manual download.
4.  Creates necessary symlinks for tools like `fd` (as `fdfind`) and `bat` (as `batcat`).

## Installed Applications

The list of applications to be installed is defined in `roles/terminal_applications/defaults/main.yml`. You can customize this list to add or remove applications.

### Shell profile

Note that some installers (like for `zoxide` and `atuin`) might want to modify your shell's startup files (e.g., `.bashrc`, `.zshrc`) to be fully integrated. The playbook runs them in a non-interactive mode (`CI=true`), which should prevent this. You may need to add initialization logic to your shell's config file manually for these tools. For example, for zoxide, you would add `eval "$(zoxide init bash)"` to your `.bashrc`.
# dotfiles
