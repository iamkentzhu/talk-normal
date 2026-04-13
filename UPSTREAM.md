# Upstream Policy

## Upstream Source

- Original author: [hexiecs](https://github.com/hexiecs)
- Upstream repository: [hexiecs/talk-normal](https://github.com/hexiecs/talk-normal)
- Current upstream version tracked by this repo: `0.6.2`

## This Repository's Role

This repository is **not** the official upstream project.

It is a maintained **OpenClaw skill wrapper** around the original `talk-normal` prompt, with:
- `SKILL.md` packaging for OpenClaw
- installation and usage documentation
- maintenance notes for downstream users

## Sync Strategy

We do **not** auto-pull upstream changes directly into production use.

Instead, the maintenance flow is:

1. fetch upstream changes
2. review the diff manually
3. decide whether the changes should be absorbed
4. validate the updated skill behavior
5. release a new version of this wrapper repo
6. sync downstream copies if needed

## Maintenance Principles

- Keep the original rule content as intact as possible
- Put wrapper-specific changes in documentation and packaging, not in the prompt logic unless necessary
- Record upstream sync points explicitly
- Prefer stable, reviewed updates over automatic tracking

## Local Changes in This Wrapper

Compared with upstream, this repository currently adds:
- OpenClaw `SKILL.md` packaging
- README installation/configuration instructions
- attribution and acknowledgment for the original author
- downstream maintenance policy
