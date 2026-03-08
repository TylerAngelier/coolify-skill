# Coolify CLI Skill

This repository contains a Codex skill for working with the official [`coolify-cli`](https://github.com/coollabsio/coolify-cli).

The skill helps Codex verify the local CLI, configure contexts, discover resource UUIDs, and compose or run safe `coolify` commands for apps, services, servers, databases, backups, deployments, and environment variables.

The skill lives in [`coolify-cli/`](./coolify-cli) and can be invoked as `$coolify-cli`.

## Install

From the root of this repository, install the skill locally for Codex via symlink:

```bash
mkdir -p ~/.agents/skills
ln -s "$(pwd)/coolify-cli" ~/.agents/skills/coolify-cli
```

If the symlink already exists, remove it first or replace it with:

```bash
ln -sfn "$(pwd)/coolify-cli" ~/.agents/skills/coolify-cli
```
