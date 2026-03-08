# Coolify CLI Skill

This repository contains a Codex skill for working with the official [`coolify-skill`](https://github.com/coollabsio/coolify-skill).

The skill helps Codex verify the local CLI, configure contexts, discover resource UUIDs, and compose or run safe `coolify` commands for apps, services, servers, databases, backups, deployments, and environment variables.

The skill lives in [`coolify-skill/`](./coolify-skill) and can be invoked as `$coolify-skill`.

## Install

From the root of this repository, install the skill locally for Codex via symlink:

```bash
mkdir -p ~/.agents/skills
ln -s "$(pwd)/coolify-skill" ~/.agents/skills/coolify-skill
```

If the symlink already exists, remove it first or replace it with:

```bash
ln -sfn "$(pwd)/coolify-skill" ~/.agents/skills/coolify-skill
```
