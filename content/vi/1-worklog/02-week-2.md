---
title: "Tuần 2 - Tích hợp local và container hóa"
linkTitle: "1.2. Nhật ký Tuần 2"
weight: 2
---

**Thời gian:** 22/06/2026 - 26/06/2026

| Ngày | Ngày thực hiện | Công việc chính |
|---:|---|---|
| 2 | 22/06 | Chuẩn bị `.env.example` và các biến PostgreSQL, Flask, JWT, logging và API routing. |
| 3 | 23/06 | Chuẩn bị backend container, Gunicorn, dependencies và endpoint `/health`. |
| 4 | 24/06 | Chuẩn bị React production build, Nginx và reverse proxy `/api`. |
| 5 | 25/06 | Xây dựng `docker-compose.yml` cho `db`, `backend`, `frontend`; thêm health check và volume. |
| 6 | 26/06 | Chạy hệ thống local, kiểm tra authentication/API và sửa lỗi CORS, API path. |

**Kết quả:** hoàn thành môi trường Docker Compose hoạt động ổn định trước khi triển khai AWS.
