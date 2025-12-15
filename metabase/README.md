
---

# Metabase Docker Setup

This guide explains how to run Metabase using Docker Compose.

## How to Run

1.  **Create the project folder and configuration file:**
    ```bash
    git clone https://github.com/malnozili/data-stack.git
    cd data-stack && cd metabase 
  
    ```

2.  **Start Metabase:**
    ```bash
    docker compose up -d
    ```
    This command will download the images and start the containers in the background.

3.  **Access the application:**
    Open your web browser and go to:
    ```
    http://YOUR_SERVER_IP:3000
    ```
    Follow the setup wizard to create an admin account and connect your first database.


**Important:** Replace `your_secure_password_here` with a strong password in both places.

## Reference

All configuration details, environment variables, and advanced guides are in the official documentation:
*   **Main Docker Guide:** [Running Metabase on Docker](https://www.metabase.com/docs/latest/installation-and-operation/running-metabase-on-docker)
*   **Production Setup:** [How to run Metabase in production](https://www.metabase.com/docs/latest/installation-and-operation/running-metabase-in-production)

---
