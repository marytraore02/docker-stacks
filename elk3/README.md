# 📊 ELK Stack (+ Filebeat)

Full ELK Stack v7.14 with Filebeat for automated log collection from Docker containers and system logs.

## Services

| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **Elasticsearch** | `elasticsearch:7.14.0` | `9200`, `9300` | Search & analytics engine |
| **Logstash** | `logstash:7.14.0` | `5044`, `9600` | Log processing pipeline |
| **Kibana** | `kibana:7.14.0` | `5601` | Data visualization |
| **Filebeat** | `elastic/filebeat:7.14.0` | — | Log collector agent |

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
| Kibana | http://localhost:5601 |
| Elasticsearch API | http://localhost:9200 |
| Logstash Monitoring | http://localhost:9600 |

## Filebeat Auto-Collection

Filebeat automatically collects logs from:
- 🐳 Docker containers (`/var/lib/docker/containers`)
- 📋 System logs (`/var/log/syslog`, `/var/log/auth.log`)

## Configuration

```
elk-config/
├── elasticsearch/
│   └── elasticsearch.yml
├── logstash/
│   ├── logstash.conf
│   └── logstash.yml
├── kibana/
│   └── kibana.yml
└── filebeat/
    └── filebeat.yml
```

## Network

This stack uses the `shared_network_local` external network.
