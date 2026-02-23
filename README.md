# ansible-project

## Overview

This repository contains an Ansible playbook designed to automate the configuration of Fedora-based internet-facing systems.

## What it does

- **Nginx**: Installs and starts the Nginx web server, configures firewall rules for HTTP/HTTPS (ports 80/443), and manages SELinux settings as required.
- **Docker**: Adds the official Docker CE repository, installs Docker and Docker Compose, starts the Docker daemon, and adds the current user to the `docker` group.
- **Dotfiles**: Installs Zsh and Oh My Zsh, clones my repository ([link](https://github.com/aaronpo97/dotfiles)), and applies configuration using GNU Stow.
- **Fail2ban**: Installs Fail2ban, deploys a custom `jail.local` configuration, and enables the service.
- **Security**: Changes the SSH port to 1997, closes port 22, applies optional SSH hardening, configures firewalld, enables SELinux port, installs and configures `dnf-automatic` for security updates, installs Cockpit and restricts access to localhost.
- **Lazydocker**: Installs Lazydocker for simplified Docker management.
- **Fastfetch**: Installs Fastfetch for system information display.

## Requirements

- Ansible must be installed on the control machine.
- SSH access to the target host is required.
- Target system must be running Fedora (tested with Fedora 43).

## Usage

To execute the playbook, run:

```bash
ansible-playbook -i inventory.ini playbook.yml --ask-pass --ask-become-pass
```

The `--ask-pass` flag prompts for the SSH password, while `--ask-become-pass` prompts for the sudo password. If SSH keys are configured, omit `--ask-pass`.

After the playbook completes, update your inventory file to use the new SSH port (1997).

## Inventory Example

Refer to `inventory.ini.example` for a sample inventory configuration.

## Collections

The following Ansible collections are required:

- `ansible.posix`
- `community.general`

Install them with:

```bash
ansible-galaxy collection install -r requirements.yml
```
