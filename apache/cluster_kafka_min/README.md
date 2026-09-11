# 📡 Kafka Minimal Cluster

Minimal Kafka streaming cluster with Zookeeper, Redis, and management UIs.

## Services

| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **Zookeeper** | `confluentinc/cp-zookeeper:7.3.2` | `2181` | Kafka coordination service |
| **Kafka** | `confluentinc/cp-kafka:7.4.0` | `9092`, `29092` | Message broker |
| **Kafka UI** | `provectuslabs/kafka-ui:latest` | `8040` | Kafka web management |
| **Redis** | `redis:7.2-alpine` | `6379` | In-memory data store |
| **RedisInsight** | `redis/redisinsight:2.70` | `5540` | Redis web management |

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
| Kafka UI | http://localhost:8040 | — |
| RedisInsight | http://localhost:5540 | — |

## Kafka Listeners

| Listener | Address | Usage |
|----------|---------|-------|
| `INTERNAL` | `kafka:9092` | Inter-container communication |
| `EXTERNAL` | `localhost:29092` | Host machine access |

## Network

This stack uses the `shared_network_local` external network.
