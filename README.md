# ansible-role-spamassassin

[![Build Status](https://github.com/systemli/ansible-role-spamassassin/workflows/Integration/badge.svg?branch=main)](https://github.com/systemli/ansible-role-spamassassin/actions?query=workflow%3AIntegration)
[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-spamassassin-blue.svg)](https://galaxy.ansible.com/systemli/spamassassin/)

Role to install & maintain spamassassin (including DKIM, pyzor and razor checks)

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

Molecule, Goss, Docker, and Github Actions are used for continous testing.
You can easily test the role locally with

    molecule test

This requires Molecule, Vagrant and `python-vagrant` to be installed.

## License

GPLv3

## Author Information

https://www.systemli.org
