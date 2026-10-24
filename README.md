# ansible-role-spamassassin

[![Build Status](https://github.com/systemli/ansible-role-spamassassin/workflows/Integration/badge.svg?branch=main)](https://github.com/systemli/ansible-role-spamassassin/actions?query=workflow%3AIntegration)
[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-spamassassin-blue.svg)](https://galaxy.ansible.com/systemli/spamassassin/)

Role to install & maintain SpamAssassin (including DKIM, pyzor and razor checks)

## Role Variables


For an overview of these, see `defaults/main.yml`.

## Download


Download latest release with `ansible-galaxy`

	ansible-galaxy install systemli.spamassassin

## Example Playbook


    - hosts: servers
      roles:
         - { role: systemli.spamassassin }

## Testing & Development

Molecule with the Docker driver and GitHub Actions are used for continuous testing.
CI runs the role on Debian 13 (trixie); `meta/main.yml` lists Debian trixie and bookworm.
You can test the role locally with

    molecule test

Use `molecule converge` to apply the role and `molecule login` to open a shell in the container.
This requires Docker or Podman, `molecule`, `molecule-plugins[docker]` and `ansible-lint` to be installed.

## License

GPLv3

## Author Information

https://www.systemli.org
