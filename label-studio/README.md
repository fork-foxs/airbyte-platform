# Label Studio – Docker & Docker Compose Setup

This repository provides a simple way to run **Label Studio** using **Docker Compose**, based on the **official Label Studio documentation**.

It includes:

* Label Studio
* PostgreSQL database (recommended for production)
* Persistent volumes for data safety

---

## 📦 Requirements

* Docker
* Docker Compose **v1.25.0+** or `docker compose` plugin

Verify installation:

```bash
docker --version
docker compose version
```

---

## 🚀 Run Label Studio with Docker Compose (PostgreSQL)

### ⚠️ Important: Prepare data directory permissions

Before starting the containers, you **must** prepare the data directory on the host. Label Studio does **not** run as root inside the container, so incorrect permissions will cause startup failures.

Run the following commands in the same directory as `docker-compose.yml`:

```bash
mkdir -p labelstudio-data
chmod -R 777 labelstudio-data
# OR (recommended and more secure)
chown -R 1001:1001 labelstudio-data
```

> ℹ️ Use **either** `chmod` **or** `chown`.
>
> * `chmod 777` → quick and simple (OK for dev/test)
> * `chown 1001:1001` → recommended for production

---

### 1️⃣ Docker Compose file

The following `docker-compose.yml` runs Label Studio with a PostgreSQL backend:

```yaml
version: "3.8"

services:
  label_studio:
    image: heartexlabs/label-studio:latest
    container_name: label_studio
    ports:
      - "8080:8080"
    environment:
      DJANGO_DB: default
      POSTGRE_NAME: postgres
      POSTGRE_USER: postgres
      POSTGRE_PASSWORD: examplepassword
      POSTGRE_HOST: db
      POSTGRE_PORT: 5432
    volumes:
      - ./labelstudio-data:/label-studio/data
    depends_on:
      - db

  db:
    image: postgres:13
    container_name: labelstudio_postgres
    restart: always
    environment:
      POSTGRES_DB: postgres
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: examplepassword
    volumes:
      - ./postgres-data:/var/lib/postgresql/data

volumes:
  postgres-data:
  labelstudio-data:
```

---

### 2️⃣ Start the services

From the project directory:

```bash
docker compose up -d
```

This will:

* Pull the required images
* Start PostgreSQL
* Start Label Studio

---

### 3️⃣ Access Label Studio

Open your browser:

```
http://localhost:8080
```

Create the first admin user when prompted.

---

## 💾 Data Persistence

* `./labelstudio-data` → Label Studio projects, uploads, annotations
* `./postgres-data` → PostgreSQL database files

Your data will **persist even after container restarts**.

---

## 🧪 Alternative: Run Label Studio with SQLite (No PostgreSQL)

If you want a **simpler setup** (testing, small projects), you can use **SQLite** instead of PostgreSQL.

### Docker Compose (SQLite)

```yaml
version: "3.8"

services:
  label_studio:
    image: heartexlabs/label-studio:latest
    ports:
      - "8080:8080"
    volumes:
      - ./labelstudio-data:/label-studio/data
```

Run:

```bash
docker compose up -d
```

⚠️ SQLite is **not recommended for production**.

---

## 🐳 Run Label Studio with Docker (Single Command)

You can also run Label Studio **without Docker Compose** using this command:

```bash
docker run -it \
  -p 8080:8080 \
  -v $(pwd)/mydata:/label-studio/data \
  heartexlabs/label-studio:latest
```

This setup:

* Uses **SQLite** by default
* Stores data in `./mydata`
* Is suitable for quick testing

---

## 🔐 Security Notes

* Change database passwords before production use
* Consider using `.env` files for secrets
* For production, use HTTPS and a reverse proxy (Nginx / Traefik)

---

## 📚 Official References

* Label Studio – Install with Docker:
  [https://labelstud.io/guide/install.html#Install-with-Docker](https://labelstud.io/guide/install.html#Install-with-Docker)

* Label Studio GitHub Repository:
  [https://github.com/HumanSignal/label-studio](https://github.com/HumanSignal/label-studio)

---

✅ You are now ready to use Label Studio with Docker or Docker Compose.
