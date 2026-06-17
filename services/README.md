# 🌐 Services — All-in-One Stack

Combined Docker stack with Kafka, ELK, and PostgreSQL clusters running together.

## Services

### Kafka Cluster
| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **Zookeeper** | `confluentinc/cp-zookeeper:7.3.2` | `2181` | Kafka coordination |
| **Kafka Broker** | `confluentinc/cp-kafka:7.4.0` | `9092` | Message broker |
| **Kafka UI** | `provectuslabs/kafka-ui:latest` | `8080` | Kafka web management |
| **Kafka Manager** | `hlebalbau/kafka-manager:stable` | `9000` | Cluster management |

### ELK Cluster
| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **Elasticsearch** | `elasticsearch:7.14.0` | `9200` | Search engine |
| **Logstash** | `logstash:7.14.0` | `6000`, `9600` | Log processing |
| **Kibana** | `kibana:7.14.0` | `5601` | Visualization |

### PostgreSQL Cluster
| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **PostgreSQL** | `postgres:latest` | `5432` | Database server |
| **pgAdmin** | `dpage/pgadmin4` | `8888` | Web management |

## Quick Start

```bash
docker compose up -d
```

## Access

| Interface | URL | Credentials |
|-----------|-----|-------------|
| Kafka UI | http://localhost:8080 | — |
| Kafka Manager | http://localhost:9000 | — |
| Kibana | http://localhost:5601 | — |
| Elasticsearch | http://localhost:9200 | — |
| pgAdmin | http://localhost:8888 | `admin@gmail.com` / `admin123` |

> 💡 This is a monolithic stack — for individual stacks, see the root directories.
