# 🐘 Hadoop Ecosystem

Hadoop ecosystem stacks for distributed storage (HDFS) and processing (MapReduce, YARN).

## Available Configurations

| Configuration | Directory | Description |
|---------------|-----------|-------------|
| **Docker Hadoop** | [`docker-hadoop/`](docker-hadoop/) | Full Hadoop cluster (NameNode, DataNode, YARN) |
| **Hadoop Eco** | [`hadoop-eco/`](hadoop-eco/) | Extended Hadoop ecosystem |
| **First** | [`first/`](first/) | Basic Hadoop configuration |

## Quick Start

```bash
# Navigate to the desired configuration
cd docker-hadoop

# Start the cluster
docker compose up -d
```

## Notes

- These stacks are resource-intensive and require at least **4 GB RAM**
- The `el_quijote.txt` file is sample data for HDFS testing
- MapReduce example JAR is included for running sample jobs
