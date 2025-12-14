

````markdown
# Airbyte Platform v0.50.40 (Docker Compose Deployment)

This repository contains the Docker Compose setup for **Airbyte v0.50.40**.

> ⚠️ Note: This deployment method is **only available in this version**.  
> Later versions removed `docker-compose.yaml` from the main branch and migrated to **Helm / Kubernetes** deployment methods.

## Repository

GitHub: [airbyte-platform v0.50.40](https://github.com/airbytehq/airbyte-platform/tree/v0.50.40)

---

## Getting Started

Download the required files using:

```bash
wget https://raw.githubusercontent.com/airbytehq/airbyte-platform/v0.50.40/docker-compose.yaml
wget https://raw.githubusercontent.com/airbytehq/airbyte-platform/v0.50.40/.env
````

This will provide:

* `docker-compose.yaml` → the Docker Compose configuration
* `.env` → environment variables for Docker deployment

---

## Prerequisites

* Docker >= 20.x
* Docker Compose >= 2.x
* At least 8 GB RAM recommended

---

## Configuration

Check the `.env` file for important variables:

```env
BASIC_AUTH_USERNAME=airbyte
BASIC_AUTH_PASSWORD=password
WEBAPP_URL=http://localhost:8000/
DATABASE_USER=docker
DATABASE_PASSWORD=docker
DATABASE_HOST=db
DATABASE_PORT=5432
DATABASE_DB=airbyte
```

### Change WEBAPP URL for External Access

If you want to access Airbyte from outside the server, edit the `.env`:

```env
WEBAPP_URL=http://YOUR_SERVER_IP:8000/
```

Replace `YOUR_SERVER_IP` with your server’s public IP or domain.

> **Security Note:** Always change the default username/password before exposing Airbyte publicly.

---

## Running Airbyte

Start all services:

```bash
docker compose up -d
```

Check container status:

```bash
docker compose ps
```

Stop all services:

```bash
docker compose down
```

---

## Port Usage

| Port | Service            | Usage / Notes                                           |
| ---- | ------------------ | ------------------------------------------------------- |
| 8000 | Web UI + API proxy | Access via browser or API requests; requires Basic Auth |
| 8001 | Internal server    | Not exposed to external users                           |
| 8003 | Internal proxy     | Internal communication between services                 |
| 8006 | Internal API       | Access via 8000 proxy recommended                       |

> For external access, **only port 8000** should be used.

---

## Basic Authentication

By default, Airbyte is protected via HTTP Basic Auth:

```env
BASIC_AUTH_USERNAME=airbyte
BASIC_AUTH_PASSWORD=password
```

Use these credentials when accessing the Web UI or API.
To disable (not recommended) or change credentials, edit `.env` and restart:

```bash
docker compose restart
```

---

## Testing Airbyte API

### Health Check

```bash
curl -u airbyte:password http://YOUR_SERVER_IP:8000/api/v1/health
```

Expected response:

```json
{"available":true}
```

### List Workspaces

```bash
curl -u airbyte:password \
  -H "Content-Type: application/json" \
  http://YOUR_SERVER_IP:8000/api/v1/workspaces/list \
  -d '{}'
```

---

## Firewall / Network Notes

* Ensure **TCP port 8000** is open for external access.
* If using UFW:

```bash
sudo ufw allow 8000/tcp
sudo ufw reload
```

* For cloud providers, check Security Groups or firewall rules.
* If Airbyte is on a NAT or private network, make sure the public IP is forwarded correctly.

---

## Important Notes

* This Docker Compose deployment is **legacy**.
* For newer versions, refer to Airbyte docs for **Helm / Kubernetes deployment**.
* Use HTTPS or Nginx proxy for production exposure.
* Avoid using default credentials on public servers.

---

## References

* Official Airbyte Docs: [https://docs.airbyte.com](https://docs.airbyte.com)
* v0.50.40 GitHub Tag: [https://github.com/airbytehq/airbyte-platform/tree/v0.50.40](https://github.com/airbytehq/airbyte-platform/tree/v0.50.40)

```

```
