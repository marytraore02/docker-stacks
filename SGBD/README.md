# 🗄️ Databases & Storage

This directory contains Docker stacks for various database and storage solutions.

## Available Stacks

| Stack | Description | Directory |
|-------|-------------|-----------|
| **ClickHouse Connect** | ClickHouse analytics database with Python connector library | [`clickhouse-connect/`](clickhouse-connect/) |
| **MinIO** | S3-compatible object storage with web console | [`minio/`](minio/) |
| **MongoDB Stack** | MongoDB 8.0 database with Mongo Express UI | [`mongodb/`](mongodb/) |
| **MySQL Stack** | MySQL 8 database with phpMyAdmin interface | [`mysql/`](mysql/) |
| **PostgreSQL Stack** | PostgreSQL with pgvector extension + pgAdmin4 | [`postgres/`](postgres/) |
| **Redis Stack** | Redis database with RedisInsight UI | [`redis/`](redis/) |

## Quick Start

```bash
# Start any stack
cd <stack-directory>
docker compose up -d
```
