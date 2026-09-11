# 🐘 PostgreSQL Stack

PostgreSQL database with **pgvector** extension for vector similarity search, plus pgAdmin4 web interface.

## Services

| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **PostgreSQL** | `pgvector/pgvector:0.8.1-pg18-trixie` | `5432` | PostgreSQL with vector extension |
| **pgAdmin4** | `dpage/pgadmin4` | `8887` | Web-based database management |

## Quick Start

```bash
# Create shared network (if not exists)
docker network create shared_network_local

# Start the stack
docker compose up -d
```

## Access

| Interface | URL | Credentials |
|-----------|-----|-------------|
| pgAdmin4 | http://localhost:8887 | `admin@gmail.com` / `admin123` |
| PostgreSQL CLI | `psql -h localhost -p 5432 -U postgres` | `postgres` |

## pgvector

This stack uses the `pgvector` extension, enabling:
- Vector similarity search
- AI/ML embeddings storage
- Nearest neighbor queries

## Network

This stack uses the `shared_network_local` external network.
