# 🗄️ Databases & Storage

This directory contains Docker stacks for various database and storage solutions.

## Available Stacks

| Stack | Description | Directory |
|-------|-------------|-----------|
| **ClickHouse Connect** | ClickHouse analytics database with Python connector library | [`clickhouse-connect/`](clickhouse-connect/) |
| **MinIO** | S3-compatible object storage with web console | [`minio/`](minio/) |
| **MySQL Stack** | MySQL 8 database with phpMyAdmin interface | [`mysql-stack/`](mysql-stack/) |
| **PostgreSQL Stack** | PostgreSQL with pgvector extension + pgAdmin4 | [`postgres-stack/`](postgres-stack/) |
| **Redis Stack** | Redis database with RedisInsight UI | [`redis-stack/`](redis-stack/) |

## Quick Start

```bash
# Start any stack
cd <stack-directory>
docker compose up -d
```
