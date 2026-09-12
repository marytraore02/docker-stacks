# ⚡ Apache Flink

Apache Flink stream and batch processing cluster with JobManager and TaskManager.

## Services

| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **JobManager** | `my-flink` (custom) | `8082` | Flink cluster manager & web UI |
| **TaskManager** | `my-flink` (custom) | — | Flink task execution |

## Prerequisites

Build the custom Flink image first:

```bash
docker build -t my-flink -f flink.Dockerfile .
```

## Quick Start

```bash
docker compose up -d
```

## Access

| Interface | URL |
|-----------|-----|
| Flink Dashboard | http://localhost:8082 |

## Configuration

- **Task Slots**: 6 per TaskManager
- **RPC Address**: `jobmanager`
