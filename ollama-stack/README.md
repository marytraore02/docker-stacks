# 🤖 Ollama + Open WebUI

Self-hosted Large Language Model (LLM) stack with Ollama backend and Open WebUI chat interface.

## Services

| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **Ollama** | `ollama/ollama:latest` | `11434` | LLM inference server |
| **Open WebUI** | `ghcr.io/open-webui/open-webui:main` | `3001` | ChatGPT-like web interface |

## Quick Start

```bash
# Create shared network (if not exists)
docker network create shared_network_local

# Start the stack
docker compose up -d

# Pull a model (e.g., Mistral)
docker exec -it ollama ollama pull mistral
```

## Access

| Interface | URL |
|-----------|-----|
| Open WebUI (Chat) | http://localhost:3001 |
| Ollama API | http://localhost:11434 |

## Pulling Models

```bash
# List available models
docker exec -it ollama ollama list

# Pull models
docker exec -it ollama ollama pull llama3
docker exec -it ollama ollama pull mistral
docker exec -it ollama ollama pull codellama
```

## Configuration

| Parameter | Value |
|-----------|-------|
| Parallel Requests | `2` |
| Model Keep Alive | `5 minutes` |

## Network

This stack uses the `shared_network_local` external network.
