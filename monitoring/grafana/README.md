# 📈 Grafana + Prometheus

Monitoring and visualization stack with Grafana dashboards and Prometheus metrics collection.

## Services

| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **Grafana** | `grafana/grafana-enterprise` | `3000` | Metrics visualization & dashboards |
| **Prometheus** | `prom/prometheus:v2.51.0` | `9094` | Metrics collection & storage |

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
| Grafana | http://localhost:3000 | `admin` / `admin123` |
| Prometheus | http://localhost:9094 | — |

## Pre-installed Plugins

- `grafana-clock-panel`
- `grafana-simple-json-datasource`
- `grafana-clickhouse-datasource`

## Configuration

```
grafana/
├── docker-compose.yml
├── prometheus.yml           # Prometheus scrape targets
├── provisioning/            # Grafana auto-provisioning
└── grafana/
    └── provisioning/        # Additional provisioning configs
```

## Prometheus Data Retention

Metrics are retained for **30 days** (`--storage.tsdb.retention.time=30d`).

## Network

This stack uses the `shared_network_local` external network.
