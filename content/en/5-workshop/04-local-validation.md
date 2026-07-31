---
title: "Local Testing and Validation"
linkTitle: "5.4. Local Testing and Validation"
weight: 4
---


## Create local configuration

```bash
cp .env.example .env
```

Replace the placeholders in `.env`; do not commit this file.

## Start Docker Compose

```bash
docker compose up --build -d
docker compose ps
```

Expected services:

```text
db       healthy
backend  healthy
frontend running
```

PostgreSQL must become healthy before the backend, and the backend must become healthy before the frontend.

## Health check

```bash
curl http://localhost/health
```

```json
{
  "service": "library-flask-api",
  "status": "ok"
}
```

## Validate the backend

```bash
cd backend
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements-dev.txt
PYTHONPATH=. python -m pytest -q
```

A failed required test must stop the deployment workflow.

## Build the frontend

```bash
cd frontend
npm ci
VITE_API_BASE_URL=/api npm run build
```

The optimized build is generated in `frontend/dist`. Nginx reverse-proxies `/api` to the backend.

## Stop the local environment

```bash
docker compose down
# Also remove the database volume when a clean database is required:
docker compose down -v
```
