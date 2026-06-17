<p align="center">
  <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" alt="Docker Logo" width="120"/>
</p>

<h1 align="center">🐳 Docker Stacks Collection</h1>

<p align="center">
  <strong>A curated collection of production-ready Docker Compose stacks for data engineering, streaming, monitoring, AI, and application development.</strong>
</p>

<p align="center">
  <a href="#-quick-start"><img src="https://img.shields.io/badge/Quick_Start-blue?style=for-the-badge" alt="Quick Start"/></a>
  <a href="#-stacks-catalog"><img src="https://img.shields.io/badge/Stacks_Catalog-green?style=for-the-badge" alt="Stacks"/></a>
  <a href="#-contributing"><img src="https://img.shields.io/badge/Contributing-orange?style=for-the-badge" alt="Contributing"/></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge" alt="License"/></a>
</p>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Prerequisites](#-prerequisites)
- [Repository Structure](#-repository-structure)
- [Stacks Catalog](#-stacks-catalog)
  - [📊 Data Processing & Big Data](#-data-processing--big-data)
  - [📡 Streaming & Messaging](#-streaming--messaging)
  - [🗄️ Databases & Storage](#️-databases--storage)
  - [📈 Monitoring & Observability](#-monitoring--observability)
  - [🤖 AI & Machine Learning](#-ai--machine-learning)
  - [⚙️ Automation & Orchestration](#️-automation--orchestration)
  - [🌐 Full-Stack Applications](#-full-stack-applications)
- [Quick Start](#-quick-start)
- [Networking](#-networking)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🌟 Overview

This repository contains a well-organized collection of **Docker Compose** stacks, each designed for a specific technology or use case. Every stack is self-contained in its own directory with its own documentation, configuration files, and `docker-compose.yml`.

### ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🏗️ **Modular** | Each stack is independent and can be started/stopped individually |
| 🔗 **Interconnectable** | Stacks can communicate via shared Docker networks |
| 📖 **Documented** | Every stack includes its own README with usage instructions |
| 🚀 **Ready-to-Use** | Just `docker compose up -d` and you're good to go |

---

## 🔧 Prerequisites

| Requirement | Minimum Version |
|-------------|-----------------|
| [Docker](https://docs.docker.com/get-docker/) | `20.10+` |
| [Docker Compose](https://docs.docker.com/compose/install/) | `2.0+` |
| Available RAM | `4 GB` (8 GB+ recommended) |
| Disk Space | `20 GB+` free |

---

## 📁 Repository Structure

```
docker-stacks/
│
├── 📂 BDD/                          # Databases & Storage
│   ├── 📂 clickhouse-connect/       # ClickHouse database + Python connector
│   ├── 📂 minio/                    # MinIO S3-compatible object storage
│   ├── 📂 mysql-stack/              # MySQL + phpMyAdmin
│   └── 📂 postgres-stack/           # PostgreSQL (pgvector) + pgAdmin
│
├── 📂 airflows/                     # Apache Airflow (CeleryExecutor)
├── 📂 apache_flink/                 # Apache Flink (JobManager + TaskManager)
├── 📂 apache_spark/                 # Apache Spark (Master + 2 Workers)
│
├── 📂 cluster_kafka_min/            # Kafka + Zookeeper + Redis + UIs
├── 📂 kafka-stack-docker-compose/   # Advanced Kafka configurations (multi-broker)
│
├── 📂 elk2/                         # ELK Stack v7.14 (basic)
├── 📂 elk3/                         # ELK Stack v7.14 (+ Filebeat)
│
├── 📂 grafana/                      # Grafana + Prometheus monitoring
├── 📂 hadoop-ecosystem/             # Hadoop ecosystem (HDFS, YARN, MapReduce)
│
├── 📂 n8n/                          # n8n workflow automation
├── 📂 portainer/                    # Portainer Docker management UI
├── 📂 ollama-stack/                 # Ollama LLM + Open WebUI
│
├── 📂 services/                     # All-in-one stack (Kafka + ELK + PostgreSQL)
├── 📂 springboot-mysql/             # Spring Boot + MySQL application
│
├── 📄 .gitignore                    # Git ignore rules
├── 📄 CONTRIBUTING.md               # Contribution guidelines
├── 📄 LICENSE                       # MIT License
└── 📄 README.md                     # This file
```

---

## 📦 Stacks Catalog

### 📊 Data Processing & Big Data

| Stack | Description | Directory | Ports |
|-------|-------------|-----------|-------|
| **Apache Spark** | Distributed computing cluster with 1 master and 2 workers | [`apache_spark/`](apache_spark/) | `8080`, `7077`, `4040` |
| **Apache Flink** | Stream & batch processing engine | [`apache_flink/`](apache_flink/) | `8082` |
| **Apache Airflow** | Workflow orchestration platform (CeleryExecutor) | [`airflows/`](airflows/) | `8080`, `5555` |
| **Hadoop Ecosystem** | HDFS, YARN, MapReduce cluster | [`hadoop-ecosystem/`](hadoop-ecosystem/) | Various |

### 📡 Streaming & Messaging

| Stack | Description | Directory | Ports |
|-------|-------------|-----------|-------|
| **Kafka Minimal** | Kafka + Zookeeper + Redis + Kafka UI + RedisInsight | [`cluster_kafka_min/`](cluster_kafka_min/) | `9092`, `8040`, `6379`, `5540` |
| **Kafka Advanced** | Multiple configurations (single/multi broker, schema registry) | [`kafka-stack-docker-compose/`](kafka-stack-docker-compose/) | Various |

### 🗄️ Databases & Storage

| Stack | Description | Directory | Ports |
|-------|-------------|-----------|-------|
| **PostgreSQL** | PostgreSQL with pgvector extension + pgAdmin4 | [`BDD/postgres-stack/`](BDD/postgres-stack/) | `5432`, `8887` |
| **MySQL** | MySQL 8 + phpMyAdmin | [`BDD/mysql-stack/`](BDD/mysql-stack/) | `3306`, `8899` |
| **ClickHouse** | ClickHouse analytics DB + Python connector | [`BDD/clickhouse-connect/`](BDD/clickhouse-connect/) | `8123`, `9000` |
| **MinIO** | S3-compatible object storage | [`BDD/minio/`](BDD/minio/) | `9000`, `9001` |

### 📈 Monitoring & Observability

| Stack | Description | Directory | Ports |
|-------|-------------|-----------|-------|
| **Grafana + Prometheus** | Metrics monitoring & visualization | [`grafana/`](grafana/) | `3000`, `9094` |
| **ELK Stack (basic)** | Elasticsearch + Logstash + Kibana | [`elk2/`](elk2/) | `9200`, `5044`, `5601` |
| **ELK Stack (+ Filebeat)** | Full ELK with Filebeat log collector | [`elk3/`](elk3/) | `9200`, `5044`, `5601` |

### 🤖 AI & Machine Learning

| Stack | Description | Directory | Ports |
|-------|-------------|-----------|-------|
| **Ollama + Open WebUI** | Self-hosted LLM with chat interface | [`ollama-stack/`](ollama-stack/) | `11434`, `3001` |

### ⚙️ Automation & Orchestration

| Stack | Description | Directory | Ports |
|-------|-------------|-----------|-------|
| **n8n** | Workflow automation platform | [`n8n/`](n8n/) | `5678` |
| **Portainer** | Docker management UI | [`portainer/`](portainer/) | `9443` |

### 🌐 Full-Stack Applications

| Stack | Description | Directory | Ports |
|-------|-------------|-----------|-------|
| **Services (All-in-One)** | Kafka + ELK + PostgreSQL combined | [`services/`](services/) | Various |
| **Spring Boot + MySQL** | Java web app with MySQL backend | [`springboot-mysql/`](springboot-mysql/) | `8080`, `3306` |

---

## 🚀 Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/marytraore02/docker-stacks.git
cd docker-stacks
```

### 2. Create the shared network (if needed)

Some stacks use a shared Docker network to communicate with each other:

```bash
docker network create shared_network_local
```

### 3. Start a stack

Navigate to the desired stack directory and start it:

```bash
# Example: Start the PostgreSQL stack
cd BDD/postgres-stack
docker compose up -d

# Example: Start the Kafka minimal cluster
cd cluster_kafka_min
docker compose up -d

# Example: Start the Ollama AI stack
cd ollama-stack
docker compose up -d
```

### 4. Stop a stack

```bash
docker compose down
```

### 5. Stop and remove volumes

```bash
docker compose down -v
```

---

## 🔗 Networking

Many stacks in this repository use a shared external Docker network called `shared_network_local`. This allows services from different stacks to communicate with each other.

### Creating the shared network

```bash
docker network create shared_network_local
```

### How it works

```
┌──────────────────────────────────────────────────────────────┐
│                    shared_network_local                       │
│                                                              │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────────┐ │
│  │ Kafka    │  │ Postgres │  │ Grafana  │  │ Ollama       │ │
│  │ Stack    │──│ Stack    │──│ Stack    │──│ Stack        │ │
│  └──────────┘  └──────────┘  └──────────┘  └──────────────┘ │
│                                                              │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────────┐ │
│  │ ELK      │  │ MinIO    │  │ n8n      │  │ Redis        │ │
│  │ Stack    │──│ Stack    │──│ Stack    │──│ Insight      │ │
│  └──────────┘  └──────────┘  └──────────┘  └──────────────┘ │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

> **Note:** Stacks that don't use the shared network (like `elk2/`, `services/`) run in their own isolated network.

---

## 🤝 Contributing

Contributions are welcome! Please read the [Contributing Guide](CONTRIBUTING.md) for details on how to add new stacks or improve existing ones.

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

<p align="center">
  Made with ❤️ by <a href="https://github.com/marytraore02">@marytraore02</a>
</p>