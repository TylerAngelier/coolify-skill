# Coolify CLI Command Workflows

## Contents

- Installation
- Context setup
- Read-only discovery
- Application workflows
- Service workflows
- Database workflows
- Server workflows
- Notes

## Installation

Prefer the official install scripts or `go install`:

```bash
curl -fsSL https://raw.githubusercontent.com/coollabsio/coolify-cli/main/scripts/install.sh | bash
go install github.com/coollabsio/coolify-cli/coolify@latest
```

After installation, verify with:

```bash
coolify --version
coolify --help
```

## Context Setup

For Coolify Cloud:

```bash
coolify context set-token cloud <token>
coolify context verify
```

For self-hosted Coolify:

```bash
coolify context add -d <context_name> <url> <token>
coolify context verify
```

Useful context commands:

- `coolify context list`
- `coolify context get <context_name>`
- `coolify context set-default <context_name>`
- `coolify context use <context_name>`
- `coolify context version`

## Read-Only Discovery

Use discovery commands before any mutation so you can resolve exact UUIDs:

```bash
coolify projects list
coolify resources list
coolify app list
coolify service list
coolify database list
coolify server list
```

Inspect a single resource before changing it:

```bash
coolify app get <uuid>
coolify service get <uuid>
coolify database get <uuid>
coolify server get <uuid>
```

## Application Workflows

Common operations:

```bash
coolify app list
coolify app get <uuid>
coolify app update <uuid> --name <name>
coolify app start <uuid>
coolify app stop <uuid>
coolify app restart <uuid>
coolify app logs <uuid>
```

Environment variable workflows:

```bash
coolify app env list <app_uuid>
coolify app env get <app_uuid> <env_uuid_or_key>
coolify app env create <app_uuid> --key <key> --value <value>
coolify app env update <app_uuid> <env_uuid>
coolify app env delete <app_uuid> <env_uuid>
coolify app env sync <app_uuid> --file .env
```

Deployment troubleshooting:

```bash
coolify app deployments list <app_uuid>
coolify app deployments logs <app_uuid>
coolify app deployments logs <app_uuid> <deployment_uuid> -n 200
coolify app deployments logs <app_uuid> <deployment_uuid> -f
```

## Service Workflows

Common operations:

```bash
coolify service list
coolify service get <uuid>
coolify service start <uuid>
coolify service stop <uuid>
coolify service restart <uuid>
coolify service delete <uuid>
```

Environment variable workflows mirror the app commands:

```bash
coolify service env list <service_uuid>
coolify service env get <service_uuid> <env_uuid_or_key>
coolify service env create <service_uuid> --key <key> --value <value>
coolify service env update <service_uuid> <env_uuid>
coolify service env delete <service_uuid> <env_uuid>
coolify service env sync <service_uuid> --file .env
```

## Database Workflows

Common operations:

```bash
coolify database list
coolify database get <uuid>
coolify database start <uuid>
coolify database stop <uuid>
coolify database restart <uuid>
coolify database delete <uuid>
```

Creation requires a database type plus target placement:

```bash
coolify database create postgresql \
  --server-uuid <server_uuid> \
  --project-uuid <project_uuid> \
  --environment-name production
```

Backup workflows:

```bash
coolify database backup list <database_uuid>
coolify database backup create <database_uuid> --frequency '0 2 * * *'
coolify database backup executions <database_uuid> <backup_uuid>
coolify database backup trigger <database_uuid> <backup_uuid>
```

## Server Workflows

Common operations:

```bash
coolify server list
coolify server get <uuid>
coolify server validate <uuid>
coolify server domains <uuid>
coolify server add <name> <ip> <private_key_uuid> --validate
coolify server remove <uuid>
```

## Notes

- Always inspect `coolify <group> --help` and `coolify <group> <action> --help` before using less common flags.
- `coolify app env sync` and `coolify service env sync` update existing variables and create missing ones, but do not delete variables absent from the `.env` file.
- Treat delete and remove commands as destructive and require explicit user confirmation before execution.
