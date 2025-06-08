
# 🐳 Deploying Taiga with Docker on Ubuntu 24.04

This guide explains how to install and run the **Taiga Project Management Tool** using **Docker** and **Docker Compose**.

---

## ✅ Step 1: Install Docker

Run the following commands to install Docker:

```bash
curl -s https://get.docker.com/ | sh

docker --version
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER
```

👉 **Important**: You must **log out and log in again** (or run `newgrp docker`) to apply the group changes.

---

## ✅ Step 2: Clone the Taiga Docker Repository

```bash
git clone https://github.com/taigaio/taiga-docker.git
cd taiga-docker
```

---

## ✅ Step 3: Configure the Environment

An `.env` file already exists in the repository. Open it for editing:

```bash
vim .env
```

Update the following key variables:

```env
# Taiga access settings
TAIGA_SCHEME=http
TAIGA_DOMAIN=192.168.55.49:9000
SUBPATH=""

# WebSocket settings
WEBSOCKETS_SCHEME=ws

# Secret key for Django (you can generate a new one)
SECRET_KEY="e5aadd1db76f7dc35646a8c1aec9adbf7d1d9668a1e6be66fbe0fb03ce52bf71"

# Database configuration
POSTGRES_USER=taiga
POSTGRES_PASSWORD=taiga

# Email settings (console is fine for testing)
EMAIL_BACKEND=console

# RabbitMQ
RABBITMQ_USER=taiga
RABBITMQ_PASS=taiga
RABBITMQ_VHOST=taiga
RABBITMQ_ERLANG_COOKIE=secret-erlang-cookie
```

---

## ✅ Step 4: Start Taiga Using Docker Compose

```bash
docker compose up -d
```

If `docker compose` doesn’t work, try:

```bash
docker-compose up -d
```

This command will pull and start all required containers:

- `taiga-back`
- `taiga-front`
- `postgres`
- `rabbitmq`
- `taiga-events`
- `celery`
- `nginx`

---

## ✅ Step 5: Create the Admin User

Once all containers are running, use the built-in helper script to create an admin user:

```bash
./taiga-manage.sh createsuperuser
```

If needed, ensure the script is executable:

```bash
chmod +x taiga-manage.sh
./taiga-manage.sh createsuperuser
```

Enter your desired username, email, and password.

---

## ✅ Step 6: Access the Taiga Web UI

Open your browser and go to:

```
http://192.168.55.49:9000
```

Login with the admin credentials you just created.

---

## 🌐 Optional: Enable Persian Language

After logging in:

1. Click your profile picture (top-right corner).
2. Go to **My Settings**.
3. Change **Language** to **Persian (فارسی)**.
4. Save and refresh the page.
