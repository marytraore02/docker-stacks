# ☕ Spring Boot + MySQL

Full-stack Java Spring Boot application with MySQL database and phpMyAdmin.

## Services

| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **MySQL** | `mysql:latest` | `$MYSQLDB_LOCAL_PORT` | Database server |
| **phpMyAdmin** | `phpmyadmin/phpmyadmin:latest` | `8899` | Database web interface |
| **Spring Boot App** | Custom (built from `./app`) | `$SPRING_LOCAL_PORT` | Java web application |

## Prerequisites

Ensure you have a `.env` file with the required variables:

```env
MYSQLDB_ROOT_PASSWORD=your_password
MYSQLDB_DATABASE=your_database
MYSQLDB_USER=your_user
MYSQLDB_LOCAL_PORT=3306
MYSQLDB_DOCKER_PORT=3306
SPRING_LOCAL_PORT=8080
SPRING_DOCKER_PORT=8080
```

## Quick Start

```bash
# Build and start the stack
docker compose up -d --build
```

## Access

| Interface | URL |
|-----------|-----|
| Spring Boot App | http://localhost:8080 |
| phpMyAdmin | http://localhost:8899 |

## Project Structure

```
springboot-mysql/
├── app/                      # Spring Boot application
│   ├── src/                  # Java source code
│   ├── pom.xml               # Maven dependencies
│   └── Dockerfile            # Application container
├── .env                      # Environment variables
└── docker-compose.yml
```
