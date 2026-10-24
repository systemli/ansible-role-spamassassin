# AGENTS.md

Ansible role that installs and configures SpamAssassin (including DKIM, pyzor and razor checks) on Debian.

## Layout

- `defaults/main.yml`: role variables with defaults
- `tasks/`, `handlers/`, `templates/`, `meta/`: role code
- `molecule/default/`: integration test (`molecule.yml`, `prepare.yml`, `converge.yml`)

## Checks

- `ansible-lint .` (config in `.ansible-lint`) and `yamllint .` (config in `.yamllint`)
- `molecule test` runs the role in a container; CI runs it through the shared `systemli/github-ansible-workflow`
- `ansible-lint` creates `.ansible/`; it is git ignored, never commit it

## Conventions

- Give every task a `name`; use fully qualified module names and `true`/`false` booleans
- Document new or changed role variables in `defaults/main.yml` and the README
- Pin GitHub Actions to commit SHAs with a `# vX.Y.Z` comment; Dependabot keeps them current

## Commits and PRs

- Write in English, use conventional commit titles (`feat:`, `fix:`, `chore:`, `ci:`; `!` for breaking changes)
- The PR title sets the release-drafter label (`enhancement`, `bug`, `chore`, `breaking`); a breaking change bumps the major version
- Open PRs as draft and fill in `.github/pull_request_template.md`: what changed and why, plus a breaking changes section if needed
- Do not list changed files or claim test results in the description; CI covers that
