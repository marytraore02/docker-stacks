# 🚢 Portainer — Docker Management UI

Portainer is a powerful, lightweight management UI which allows you to easily manage your different Docker environments.

## Services

| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **Portainer CE** | `portainer/portainer-ce:latest` | `9443` (HTTPS), `8000` (Edge) | Docker management interface |

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
| Portainer Web UI | [https://localhost:9443](https://localhost:9443) | Initial Setup on first run |

## Features

- **Container Management**: Start, stop, restart, and monitor containers.
- **Image Management**: Pull, push, and remove images.
- **Network & Volume Management**: Inspect and manage Docker resources.
- **Dashboard**: Visual overview of your Docker host.

## Network

This stack uses the `shared_network_local` external network, allowing it to inspect and manage services connected to this network.
