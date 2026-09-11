# 🐬 MySQL Stack

MySQL 8 database with phpMyAdmin web interface.

## Services

| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **MySQL** | `mysql:latest` | `3306` | MySQL 8 database server |
| **phpMyAdmin** | `phpmyadmin/phpmyadmin:latest` | `8899` | Web-based database management |

## Quick Start

```bash
docker compose up -d
```

## Access

| Interface | URL | Credentials |
|-----------|-----|-------------|
| phpMyAdmin | http://localhost:8899 | `user` / `password` |
| MySQL CLI | `mysql -h localhost -P 3306 -u user -p` | `password` |

## Default Database

- **Database**: `churn_finance`
- **Root Password**: `password`
