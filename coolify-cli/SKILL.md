---
name: coolify-cli
description: Work with the official Coolify CLI to inspect, configure, and operate Coolify Cloud or self-hosted instances. Use when Codex needs to install or verify `coolify`, configure contexts and API tokens, discover projects/resources/UUIDs, manage applications, services, servers, databases, backups, deployments, or environment variables, or troubleshoot CLI workflows with exact `coolify` commands.
---

# Coolify CLI

Use this skill to plan or run `coolify` CLI workflows safely and accurately.

## Workflow

1. Confirm the local CLI before assuming syntax.
   Run `command -v coolify`, `coolify --version`, and the relevant `--help` command for the exact subcommand you need.
2. Verify authentication and active target before changing anything.
   Start with `coolify context list`, `coolify context get <name>`, `coolify context verify`, or `coolify context version`.
3. Discover UUIDs with read-only commands before running mutations.
   Use `list` and `get` commands to resolve the exact app, service, server, project, or database identifier.
4. Prefer the narrowest command that proves the next step.
   For example, inspect `coolify app get <uuid>` before `coolify app update <uuid>`, or inspect `coolify database get <uuid>` before restart or delete actions.
5. Re-check command help immediately before execution if the command is high impact.
   The CLI evolves; use `coolify <group> --help` and `coolify <group> <action> --help` instead of relying on memory.

## Safety Rules

- Never print, log, or restate API tokens unless the user explicitly asks for that exact value.
- Treat `delete`, `remove`, `stop`, `restart`, backup deletion, and context replacement as potentially disruptive. Require explicit user intent before executing them.
- Resolve names to UUIDs with read-only discovery commands first; do not guess identifiers.
- Prefer showing or composing commands before executing them when the request is ambiguous or high impact.
- Call out that `env sync` updates existing variables and creates missing ones, but does not delete variables absent from the `.env` file.

## Common Patterns

### Install or verify the CLI

- Use the official install instructions in [references/command-workflows.md](./references/command-workflows.md) if `coolify` is missing.
- Prefer verifying with `coolify --version` after install.

### Configure access

- For Coolify Cloud, use `coolify context set-token cloud <token>`.
- For self-hosted Coolify, use `coolify context add -d <context_name> <url> <token>`.
- Verify access with `coolify context verify` before resource operations.

### Discover resources before mutation

- Use `list` first, then `get`, then mutate.
- Typical discovery sequence:
  `coolify projects list`
  `coolify resources list`
  `coolify app list`
  `coolify service list`
  `coolify database list`

### Troubleshoot deployments and runtime issues

- Use `coolify app logs <uuid>` for application logs.
- Use `coolify app deployments list <app_uuid>` to inspect recent deployments.
- Use `coolify app deployments logs <app_uuid> [deployment_uuid]` for deployment logs, optionally with `-n <lines>` or `-f`.
- Use `coolify context version` when behavior may depend on the target Coolify API version.

## Reference

Read [references/command-workflows.md](./references/command-workflows.md) for installation, context setup, common command groups, and example workflows.
