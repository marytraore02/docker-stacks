# 📬 MailDev — Mock SMTP Server & Web UI

MailDev is a simple web interface for previewing emails during development. It acts as an SMTP server and captures sent emails so they can be viewed in a web browser without sending actual emails to real recipients.

## Services

| Service | Image | Port | Description |
|---------|-------|------|-------------|
| **MailDev** | `maildev/maildev:2.1.0` | `1080` (Web UI), `1025` (SMTP) | Mock SMTP server & email preview interface |

## Quick Start

```bash
# Create shared network (if not exists)
docker network create shared_network_local

# Navigate to stack folder and start
cd maildev
docker compose up -d
```

## Access

| Interface | Host / URL | Port | Description |
|-----------|------------|------|-------------|
| **MailDev Web UI** | [http://localhost:1080](http://localhost:1080) | `1080` | Email inbox interface |
| **SMTP Server** | `localhost` (host) / `maildev` (Docker network) | `1025` | SMTP port for outgoing mail |

## Features

- 📧 **Web-based Inbox**: Instant live preview of HTML and plain text emails.
- 🔌 **REST API**: Programmatic access to captured emails for automated integration tests.
- 📱 **Responsive Design**: View emails formatted for desktop and mobile views.
- 🚀 **Zero Configuration**: Ready out-of-the-box for development environments.

## Network & Integration

This stack uses the `shared_network_local` external network. Other containers running in the same network (such as Spring Boot, Apache Airflow, n8n, etc.) can send emails using:

- **SMTP Host**: `maildev`
- **SMTP Port**: `1025`
- **TLS/SSL**: Disabled
- **Auth**: None

### Quick Python SMTP Test Example

```python
import smtplib
from email.mime.text import MIMEText

msg = MIMEText("This is a test email sent to MailDev.")
msg["Subject"] = "Hello from Docker Network"
msg["From"] = "app@example.com"
msg["To"] = "user@example.com"

with smtplib.SMTP("maildev", 1025) as server:
    server.sendmail("app@example.com", ["user@example.com"], msg.as_string())
```
