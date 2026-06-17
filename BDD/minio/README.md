# 🗃️ MinIO — S3-Compatible Object Storage

Self-hosted S3-compatible object storage solution.

## Services

| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **MinIO** | `minio/minio:latest` | `9000` (API), `9001` (Console) | S3-compatible storage |

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
| MinIO Console | http://localhost:9001 | `admin` / `admin123` |
| S3 API | http://localhost:9000 | — |

## Network

This stack uses the `shared_network_local` external network.
