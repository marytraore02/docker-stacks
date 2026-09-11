# 🌬️ Apache Airflow

Full Apache Airflow deployment using **CeleryExecutor** with Redis as the broker and PostgreSQL as the metadata database.

## Services

| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **Webserver** | `apache/airflow:2.10.4` | `8080` | Airflow web UI |
| **Scheduler** | `apache/airflow:2.10.4` | — | DAG scheduler |
| **Worker** | `apache/airflow:2.10.4` | — | Celery worker |
| **Triggerer** | `apache/airflow:2.10.4` | — | Async trigger handler |
| **Flower** | `apache/airflow:2.10.4` | `5555` | Celery monitoring (optional) |
| **PostgreSQL** | `postgres:13` | — | Metadata database |
| **Redis** | `redis:7.2-bookworm` | — | Celery message broker |

## Quick Start

```bash
# Set the Airflow UID (Linux only)
echo "AIRFLOW_UID=$(id -u)" > .env

# Initialize Airflow
docker compose up airflow-init

# Start all services
docker compose up -d

# Optional: Start Flower monitoring
docker compose --profile flower up -d
```

## Access

| Interface | URL | Credentials |
|-----------|-----|-------------|
| Airflow UI | http://localhost:8080 | `airflow` / `airflow` |
| Flower | http://localhost:5555 | — |

## Directory Structure

```
airflows/
├── dags/          # Place your DAG files here
├── logs/          # Airflow logs (auto-generated)
├── plugins/       # Custom plugins
├── config/        # Airflow configuration
├── .env           # Environment variables
└── docker-compose.yaml
```

## Adding DAGs

Simply place your Python DAG files in the `dags/` directory. They will be automatically detected by Airflow.
