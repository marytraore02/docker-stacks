# 🤝 Contributing to Docker Stacks

Thank you for considering contributing to this project! Here's how you can help.

---

## 📋 How to Contribute

### 1. Adding a New Stack

To add a new Docker stack, follow this structure:

```
your-stack-name/
├── docker-compose.yml    # Required: Docker Compose configuration
├── README.md             # Required: Stack documentation
├── .env.example          # Optional: Environment variables template
└── config/               # Optional: Configuration files
```

### 2. Stack README Template

Every stack must include a `README.md` with at minimum:

```markdown
# Stack Name

Brief description of what this stack provides.

## Services

| Service | Image | Port |
|---------|-------|------|
| service-name | image:tag | host:container |

## Quick Start

\`\`\`bash
docker compose up -d
\`\`\`

## Configuration

Description of key configuration options.

## Access

How to access the services (URLs, credentials, etc.)
```

### 3. Naming Conventions

- **Directory names**: Use `kebab-case` (e.g., `my-new-stack/`)
- **Docker Compose files**: Always name them `docker-compose.yml`
- **Environment files**: Use `.env.example` for templates (never commit real `.env` with secrets)

---

## 🔧 Guidelines

### Do's ✅

- Keep each stack self-contained in its own directory
- Document all exposed ports
- Include health checks when possible
- Use specific image versions (not `latest` in production)
- Add meaningful container names
- Use the shared network `shared_network_local` when inter-stack communication is needed

### Don'ts ❌

- Don't commit runtime data (volumes, logs, etc.)
- Don't hardcode sensitive credentials — use environment variables
- Don't modify existing stack configurations without discussing it first
- Don't add unnecessary dependencies between stacks

---

## 🚀 Submitting Changes

1. **Fork** the repository
2. **Create a branch** for your feature: `git checkout -b feat/my-new-stack`
3. **Commit** your changes with clear messages: `git commit -m "feat: add Redis cluster stack"`
4. **Push** to your fork: `git push origin feat/my-new-stack`
5. **Open a Pull Request** with a clear description

### Commit Convention

Use [Conventional Commits](https://www.conventionalcommits.org/) format:

| Prefix | Usage |
|--------|-------|
| `feat:` | Adding a new stack or feature |
| `fix:` | Fixing a bug in a stack configuration |
| `docs:` | Documentation updates |
| `refactor:` | Restructuring without changing functionality |
| `chore:` | Maintenance tasks |

---

## 📞 Questions?

Feel free to open an [issue](https://github.com/marytraore02/docker-stacks/issues) if you have questions or suggestions!
