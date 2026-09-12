# Unified Apache Big Data Stack
## A single, evolvable stack for running multiple Apache technologies together

This repository provides a unified approach to running Apache Hadoop, Spark, Kafka, Flink, and Airflow together using a shared Docker network and a centralized `.env` file. Adding a new technology is as simple as adding its service block to the Makefile targets.

## Architecture
- **One Docker network** (`bigdata_net`) connects all services
- **Centralized `.env`** file with common environment variables
- **Service names** match internal hostnames from original compose files, so environment variables work unchanged
- **Idempotent targets**: `make <service>` starts/stops a single service independently
- **Common dependencies** (network, volumes) are managed automatically

## Prerequisites
- Docker and Docker Compose installed
- At least 8GB RAM, 20GB disk recommended for full stack

## Quick Start

### Start the complete stack:
```bash
make up
```

### Start specific services:
```bash
make up SERVICES="spark-master kafka"
```

### Stop all services:
```bash
make down
```

### List running containers:
```bash
make ps
```

### View logs:
```bash
make logs SERVICE=spark-master
```

### Build custom Flink image:
```bash
make build-flink
```

## Service Details

| Technology | Services Started | Key Ports (host:container) |
|------------|-----------------|----------------------------|
| **Hadoop** | namenode, datanode, resourcemanager, nodemanager, historyserver | 9870, 9000, 8088, 8042, 8188 |
| **Spark** | spark-master, spark-worker1, spark-worker2 | 9090, 7077, 4040 |
| **Kafka** | zookeeper, kafka, kafka-ui | 2181, 9092, 8040 |
| **Flink** | jobmanager, taskmanager | 8082 |
| **Airflow** | postgres, redis, webserver, scheduler, worker, triggerer, flower, cli | 8080, 5555 |

*Note: The Flink custom image (`my-flink`) must be built first using `make build-flink`. The base image is built from `flink/flink.Dockerfile`.*

## Extending the Stack
To add a new technology:

1. Add environment variables to `.env` if needed (or use service-specific `-e` in the Makefile target)
2. Add a new Makefile target following the existing patterns
3. Commit your changes — the new service integrates seamlessly

## How It Works
Each Makefile target runs `docker run` with:
- `--network $(NETWORK)` — attaches to the shared network
- `--env-file $(ENV_FILE)` — provides the centralized environment
- `--name <service>` — uses the original service name (e.g., `namenode`, `kafka`)
- `-p <host:container>` — exposes necessary ports
- Volumes for data persistence where applicable

Services wait for their dependencies internally (via the original entrypoint scripts), so you can start services in any order.

## Original READMEs Preserved
The original service-specific READMEs are still in their respective directories for reference:
- `apache/hadoop/README.md`
- `apache/spark/README.md`
- `apache/cluster_kafka_min/README.md`
- `apache/flink/README.md`
- `apache/airflows/README.md`

## Contributing
1. Fork and clone
2. Run `make help` to see available commands
3. Add new services following the patterns below
4. Test additions with `make down && make up SERVICES="<new-service>"`