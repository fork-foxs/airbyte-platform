# Dagster Simple Setup
> Official deployment using `deploy_docker` example

## 📦 Quick Start

```bash
# 1. Get the official example
cd ~/data-stack
git clone https://github.com/dagster-io/dagster.git dagster-repo
cd dagster-repo/examples/deploy_docker

# 2. Start Dagster
docker-compose up -d

# 3. Check status
docker-compose ps
```

## 🌐 Access
- **Web UI**: http://your-server-ip:3000
- **Status**: `curl http://localhost:3000/server_info`

## 🛠️ Manage
```bash
# Stop
docker compose down

# Restart
docker compose restart

# View logs
docker compose logs -f
```

## 📁 Project Structure
```
deploy_docker/
├── docker-compose.yml    # Main setup
├── definitions.py        # Your pipelines
├── workspace.yaml       # Code locations
├── dagster.yaml        # Configuration
└── requirements.txt    # Dependencies
```


## 📚 References
- **Source**: `dagster-repo/examples/deploy_docker/`
- **Docs**: https://docs.dagster.io
- **Examples**: https://github.com/dagster-io/dagster/tree/master/examples

## ⚠️ Notes
- Default PostgreSQL: `postgres_user`/`postgres_password`
- No authentication by default
- Ports: 3000 (UI), 5432 (PostgreSQL), 4266 (gRPC)
