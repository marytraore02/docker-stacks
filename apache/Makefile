# Unified Big Data Stack - Docker Commands
# Usage: make up [SERVICES=...] | make down | make logs SERVICE=... | make ps

NETWORK = bigdata_net
ENV_FILE = .env

# All services to manage
ALL_SERVICES = hadoop-namenode hadoop-datanode hadoop-resourcemanager hadoop-nodemanager hadoop-historyserver \
               spark-master spark-worker1 spark-worker2 \
               kafka-zookeeper kafka-kafka kafka-kafka-ui \
               flink-jobmanager flink-taskmanager \
               airflow-postgres airflow-redis airflow-init airflow-webserver airflow-scheduler airflow-worker airflow-triggerer airflow-flower airflow-cli

# Services that need airflow-init first
AIRFLOW_SERVICES = airflow-webserver airflow-scheduler airflow-worker airflow-triggerer airflow-flower airflow-cli

.PHONY: up down ps logs status network clean init all-services

# Default: start all services
up: network init-airflow $(ALL_SERVICES)

# Start specific services: make up SERVICES="spark-master kafka-kafka"
ifneq ($(SERVICES),)
up: network init-airflow $(SERVICES)
endif

# Create shared network
network:
	@docker network inspect $(NETWORK) >/dev/null 2>&1 || docker network create $(NETWORK)

# Airflow init must run before other airflow services
init-airflow: network airflow-postgres airflow-redis
	@echo "Running Airflow initialization..."
	docker run --rm --network $(NETWORK) --env-file $(ENV_FILE) \
	  -v $(CURDIR)/airflows/dags:/opt/airflow/dags \
	  -v $(CURDIR)/airflows/logs:/opt/airflow/logs \
	  -v $(CURDIR)/airflows/config:/opt/airflow/config \
	  -v $(CURDIR)/airflows/plugins:/opt/airflow/plugins \
	  --name airflow-init \
	  apache/airflow:2.10.4 \
	  bash -c "mkdir -p /sources/logs /sources/dags /sources/plugins && chown -R 502:0 /sources/{logs,dags,plugins} && airflow db migrate && airflow users create --username airflow --password airflow --firstname Airflow --lastname Admin --role Admin --email admin@example.com || true"

# Start individual services (idempotent - removes existing container first)
hadoop-namenode: network
	@docker rm -f hadoop-namenode 2>/dev/null || true
	docker run -d --name hadoop-namenode \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -p 9870:9870 -p 9000:9000 \
	  -v hadoop_namenode:/hadoop/dfs/name \
	  bde2020/hadoop-namenode:2.0.0-hadoop3.2.1-java8

hadoop-datanode: network
	@docker rm -f hadoop-datanode 2>/dev/null || true
	docker run -d --name hadoop-datanode \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -v hadoop_datanode:/hadoop/dfs/data \
	  bde2020/hadoop-datanode:2.0.0-hadoop3.2.1-java8

hadoop-resourcemanager: network
	@docker rm -f hadoop-resourcemanager 2>/dev/null || true
	docker run -d --name hadoop-resourcemanager \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -p 8088:8088 \
	  bde2020/hadoop-resourcemanager:2.0.0-hadoop3.2.1-java8

hadoop-nodemanager: network
	@docker rm -f hadoop-nodemanager 2>/dev/null || true
	docker run -d --name hadoop-nodemanager \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -p 8042:8042 \
	  bde2020/hadoop-nodemanager:2.0.0-hadoop3.2.1-java8

hadoop-historyserver: network
	@docker rm -f hadoop-historyserver 2>/dev/null || true
	docker run -d --name hadoop-historyserver \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -p 8188:8188 \
	  -v hadoop_historyserver:/hadoop/yarn/timeline \
	  bde2020/hadoop-historyserver:2.0.0-hadoop3.2.1-java8

spark-master: network
	@docker rm -f spark-master 2>/dev/null || true
	docker run -d --name spark-master \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -p 9090:8080 -p 7077:7077 -p 4040:4040 \
	  -v $(CURDIR)/spark/apps:/apps \
	  -e SPARK_MODE=master \
	  docker.io/bitnamilegacy/spark:3.3.2

spark-worker1: network spark-master
	@docker rm -f spark-worker1 2>/dev/null || true
	docker run -d --name spark-worker1 \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -v $(CURDIR)/spark/apps:/apps \
	  -e SPARK_MODE=worker \
	  -e SPARK_MASTER_URL=spark://spark-master:7077 \
	  -e SPARK_WORKER_MEMORY=1G \
	  -e SPARK_WORKER_CORES=1 \
	  docker.io/bitnamilegacy/spark:3.3.2

spark-worker2: network spark-master
	@docker rm -f spark-worker2 2>/dev/null || true
	docker run -d --name spark-worker2 \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -v $(CURDIR)/spark/apps:/apps \
	  -e SPARK_MODE=worker \
	  -e SPARK_MASTER_URL=spark://spark-master:7077 \
	  -e SPARK_WORKER_MEMORY=1G \
	  -e SPARK_WORKER_CORES=1 \
	  docker.io/bitnamilegacy/spark:3.3.2

kafka-zookeeper: network
	@docker rm -f kafka-zookeeper 2>/dev/null || true
	docker run -d --name kafka-zookeeper \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -p 2181:2181 \
	  -e ZOOKEEPER_CLIENT_PORT=2181 \
	  -e ZOOKEEPER_TICK_TIME=2000 \
	  confluentinc/cp-zookeeper:7.3.2

kafka-kafka: network kafka-zookeeper
	@docker rm -f kafka-kafka 2>/dev/null || true
	docker run -d --name kafka-kafka \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -p 9092:9092 -p 29092:29092 -p 9101:9101 \
	  -e KAFKA_KAFKA_ID=1 \
	  -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:2181 \
	  -e KAFKA_LISTENERS=INTERNAL://0.0.0.0:9092,EXTERNAL://0.0.0.0:29092 \
	  -e KAFKA_ADVERTISED_LISTENERS=INTERNAL://kafka:9092,EXTERNAL://localhost:29092 \
	  -e KAFKA_LISTENER_SECURITY_PROTOCOL_MAP=INTERNAL:PLAINTEXT,EXTERNAL:PLAINTEXT \
	  -e KAFKA_INTER_BROKER_LISTENER_NAME=INTERNAL \
	  -e KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 \
	  -e KAFKA_GROUP_INITIAL_REBALANCE_DELAY_MS=0 \
	  -e KAFKA_CONFLUENT_LICENSE_TOPIC_REPLICATION_FACTOR=1 \
	  -e KAFKA_CONFLUENT_BALANCER_TOPIC_REPLICATION_FACTOR=1 \
	  -e KAFKA_TRANSACTION_STATE_LOG_MIN_ISR=1 \
	  -e KAFKA_TRANSACTION_STATE_LOG_REPLICATION_FACTOR=1 \
	  -e KAFKA_JMX_PORT=9101 \
	  -e KAFKA_JMX_HOSTNAME=localhost \
	  confluentinc/cp-kafka:7.4.0

kafka-kafka-ui: network kafka-kafka kafka-zookeeper
	@docker rm -f kafka-kafka-ui 2>/dev/null || true
	docker run -d --name kafka-kafka-ui \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -p 8040:8080 \
	  -e KAFKA_CLUSTERS_0_NAME=local \
	  -e KAFKA_CLUSTERS_0_BOOTSTRAPSERVERS=kafka:9092 \
	  -e KAFKA_CLUSTERS_0_ZOOKEEPER=zookeeper:2181 \
	  provectuslabs/kafka-ui:latest

flink-jobmanager: network
	@docker rm -f flink-jobmanager 2>/dev/null || true
	docker run -d --name flink-jobmanager \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -p 8082:8082 \
	  -e "FLINK_PROPERTIES=jobmanager.rpc.address: jobmanager\nrest.address: jobmanager\nrest.port: 8082" \
	  my-flink jobmanager

flink-taskmanager: network flink-jobmanager
	@docker rm -f flink-taskmanager 2>/dev/null || true
	docker run -d --name flink-taskmanager \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -e "FLINK_PROPERTIES=jobmanager.rpc.address: jobmanager\ntaskmanager.numberOfTaskSlots: 6" \
	  my-flink taskmanager

airflow-postgres: network
	@docker rm -f airflow-postgres 2>/dev/null || true
	docker run -d --name airflow-postgres \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -v postgres-db-volume:/var/lib/postgresql/data \
	  -e POSTGRES_USER=airflow \
	  -e POSTGRES_PASSWORD=airflow \
	  -e POSTGRES_DB=airflow \
	  postgres:13

airflow-redis: network
	@docker rm -f airflow-redis 2>/dev/null || true
	docker run -d --name airflow-redis \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -p 6379:6379 \
	  redis:7.2-bookworm

airflow-webserver: network airflow-postgres airflow-redis
	@docker rm -f airflow-webserver 2>/dev/null || true
	docker run -d --name airflow-webserver \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -p 8080:8080 \
	  -v $(CURDIR)/airflows/dags:/opt/airflow/dags \
	  -v $(CURDIR)/airflows/logs:/opt/airflow/logs \
	  -v $(CURDIR)/airflows/config:/opt/airflow/config \
	  -v $(CURDIR)/airflows/plugins:/opt/airflow/plugins \
	  --user "502:0" \
	  apache/airflow:2.10.4 webserver

airflow-scheduler: network airflow-postgres airflow-redis
	@docker rm -f airflow-scheduler 2>/dev/null || true
	docker run -d --name airflow-scheduler \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -v $(CURDIR)/airflows/dags:/opt/airflow/dags \
	  -v $(CURDIR)/airflows/logs:/opt/airflow/logs \
	  -v $(CURDIR)/airflows/config:/opt/airflow/config \
	  -v $(CURDIR)/airflows/plugins:/opt/airflow/plugins \
	  --user "502:0" \
	  apache/airflow:2.10.4 scheduler

airflow-worker: network airflow-postgres airflow-redis
	@docker rm -f airflow-worker 2>/dev/null || true
	docker run -d --name airflow-worker \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -v $(CURDIR)/airflows/dags:/opt/airflow/dags \
	  -v $(CURDIR)/airflows/logs:/opt/airflow/logs \
	  -v $(CURDIR)/airflows/config:/opt/airflow/config \
	  -v $(CURDIR)/airflows/plugins:/opt/airflow/plugins \
	  --user "502:0" \
	  apache/airflow:2.10.4 celery worker

airflow-triggerer: network airflow-postgres airflow-redis
	@docker rm -f airflow-triggerer 2>/dev/null || true
	docker run -d --name airflow-triggerer \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -v $(CURDIR)/airflows/dags:/opt/airflow/dags \
	  -v $(CURDIR)/airflows/logs:/opt/airflow/logs \
	  -v $(CURDIR)/airflows/config:/opt/airflow/config \
	  -v $(CURDIR)/airflows/plugins:/opt/airflow/plugins \
	  --user "502:0" \
	  apache/airflow:2.10.4 triggerer

airflow-flower: network airflow-postgres airflow-redis
	@docker rm -f airflow-flower 2>/dev/null || true
	docker run -d --name airflow-flower \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -p 5555:5555 \
	  -v $(CURDIR)/airflows/dags:/opt/airflow/dags \
	  -v $(CURDIR)/airflows/logs:/opt/airflow/logs \
	  -v $(CURDIR)/airflows/config:/opt/airflow/config \
	  -v $(CURDIR)/airflows/plugins:/opt/airflow/plugins \
	  --user "502:0" \
	  apache/airflow:2.10.4 celery flower

airflow-cli: network airflow-postgres airflow-redis
	@docker rm -f airflow-cli 2>/dev/null || true
	docker run --rm --name airflow-cli \
	  --network $(NETWORK) --env-file $(ENV_FILE) \
	  -v $(CURDIR)/airflows/dags:/opt/airflow/dags \
	  -v $(CURDIR)/airflows/logs:/opt/airflow/logs \
	  -v $(CURDIR)/airflows/config:/opt/airflow/config \
	  -v $(CURDIR)/airflows/plugins:/opt/airflow/plugins \
	  --user "502:0" \
	  apache/airflow:2.10.4 bash -c "airflow"

# Stop all services
down:
	@for svc in $(ALL_SERVICES); do docker rm -f $$svc 2>/dev/null || true; done
	@docker network rm $(NETWORK) 2>/dev/null || true

# Show status
ps:
	@docker ps --filter "network=$(NETWORK)" --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"

# Show logs for a service: make logs SERVICE=spark-master
logs:
	@docker logs -f $(SERVICE)

# Show status of all containers in network
status: ps

# Clean volumes and network
clean: down
	@docker volume rm hadoop_namenode hadoop_datanode hadoop_historyserver postgres-db-volume 2>/dev/null || true

# Build Flink custom image (must run before starting flink services)
build-flink:
	docker build -t my-flink -f flink/flink.Dockerfile ./flink

# Run WordCount example on Hadoop
wordcount: hadoop-namenode hadoop-datanode hadoop-resourcemanager hadoop-nodemanager hadoop-historyserver
	@docker run --rm --network $(NETWORK) --env-file $(ENV_FILE) \
	  bde2020/hadoop-base:2.0.0-hadoop3.2.1-java8 hdfs dfs -mkdir -p /input/
	@docker run --rm --network $(NETWORK) --env-file $(ENV_FILE) \
	  bde2020/hadoop-base:2.0.0-hadoop3.2.1-java8 hdfs dfs -copyFromLocal -f /opt/hadoop-3.2.1/README.txt /input/
	@docker run --rm --network $(NETWORK) --env-file $(ENV_FILE) \
	  bde2020/hadoop-submit:2.0.0-hadoop3.2.1-java8
	@docker run --rm --network $(NETWORK) --env-file $(ENV_FILE) \
	  bde2020/hadoop-base:2.0.0-hadoop3.2.1-java8 hdfs dfs -cat /output/*
	@docker run --rm --network $(NETWORK) --env-file $(ENV_FILE) \
	  bde2020/hadoop-base:2.0.0-hadoop3.2.1-java8 hdfs dfs -rm -r /output /input

# Help
help:
	@echo "Unified Big Data Stack - Docker Commands"
	@echo ""
	@echo "Usage:"
	@echo "  make up                    # Start all services"
	@echo "  make up SERVICES=\"spark-master kafka-kafka\"  # Start specific services"
	@echo "  make down                  # Stop all services and remove network"
	@echo "  make ps                    # List running containers"
	@echo "  make logs SERVICE=<name>   # Follow logs of a service"
	@echo "  make clean                 # Remove volumes and network"
	@echo "  make build-flink           # Build custom Flink image"
	@echo "  make wordcount             # Run Hadoop WordCount example"
	@echo ""
	@echo "Services: $(ALL_SERVICES)"