# 📊 ELK Stack (Basic)

Elasticsearch, Logstash, and Kibana stack v7.14 for log aggregation and visualization.

## Services

| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **Elasticsearch** | `elasticsearch:7.14.0` | `9200`, `9300` | Search & analytics engine |
| **Logstash** | `logstash:7.14.0` | `5044`, `9600` | Log processing pipeline |
| **Kibana** | `kibana:7.14.0` | `5601` | Data visualization |

## Quick Start

```bash
docker compose up -d
```

## Access

| Interface | URL |
|-----------|-----|
| Kibana | http://localhost:5601 |
| Elasticsearch API | http://localhost:9200 |
| Logstash Monitoring | http://localhost:9600 |

## Configuration

Custom configurations are located in `elk-config/`:

```
elk-config/
├── elasticsearch/
│   └── elasticsearch.yml
├── logstash/
│   ├── Logstash.conf
│   └── Logstash.yml
└── kibana/
    └── kibana.yml
```

> 💡 See also [`elk3/`](../elk3/) for the version with Filebeat log collector.
