---
title: "Kiểm thử và xác thực local"
linkTitle: "5.4. Kiểm thử và xác thực local"
weight: 4
---


## Tạo cấu hình local

```bash
cp .env.example .env
```

Thay các giá trị placeholder trong `.env`; không commit file này.

## Khởi chạy Docker Compose

```bash
docker compose up --build -d
docker compose ps
```

Ba service dự kiến:

```text
db       healthy
backend  healthy
frontend running
```

PostgreSQL phải healthy trước backend; backend phải healthy trước frontend.

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

## Kiểm thử backend

```bash
cd backend
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements-dev.txt
PYTHONPATH=. python -m pytest -q
```

Nếu test bắt buộc thất bại, deployment workflow phải dừng.

## Build frontend

```bash
cd frontend
npm ci
VITE_API_BASE_URL=/api npm run build
```

Kết quả build nằm trong `frontend/dist`. Nginx sử dụng `/api` làm reverse proxy đến backend.

## Dừng môi trường local

```bash
docker compose down
# Xóa cả volume database khi cần dữ liệu sạch:
docker compose down -v
```
