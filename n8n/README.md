# 🔄 n8n — Workflow Automation

Self-hosted workflow automation platform, similar to Zapier/Make, with PostgreSQL backend.

## Services

| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **n8n** | `docker.n8n.io/n8nio/n8n` | `5678` | Workflow automation UI & engine |

## Quick Start

```bash
# Create shared network (if not exists)
docker network create shared_network_local

# Start the stack
docker compose up -d
```

## Access

| Interface | URL |
|-----------|-----|
| n8n Editor | http://localhost:5678 |

## Database

n8n is configured to use an external PostgreSQL database (from the `postgres-stack`):

| Setting | Value |
|---------|-------|
| Host | `postgres` |
| Port | `5432` |
| Database | `postgres` |
| User | `postgres` |

> ⚠️ Ensure the PostgreSQL stack is running before starting n8n.

## Network

This stack uses the `shared_network_local` external network.
