---
title: "Kiến trúc triển khai"
linkTitle: "5.3. Kiến trúc triển khai"
weight: 3
---


## Sơ đồ kiến trúc hiện tại

{{< report-figure src="images/architecture-current.svg" alt="Sơ đồ kiến trúc CloudLibrary hiện tại" caption="GitHub Actions build/push image, tạo S3 bundle và triển khai frontend, backend, PostgreSQL container trên Elastic Beanstalk." >}}

## Vai trò của các thành phần

- **GitHub:** lưu source code và phát sinh sự kiện push/pull request.
- **GitHub Actions:** test, build frontend, build/push Docker image và triển khai.
- **Amazon ECR:** lưu private image frontend/backend.
- **Amazon S3:** lưu deployment bundle của Elastic Beanstalk.
- **Elastic Beanstalk:** quản lý EC2, application version, deployment và health.
- **Frontend container:** Nginx phục vụ React và reverse proxy `/api`.
- **Backend container:** Flask/Gunicorn xử lý JWT, business logic và database access.
- **PostgreSQL container:** lưu dữ liệu ứng dụng trong phiên bản hiện tại.
- **CloudWatch:** thu thập logs, metrics, dashboard và alarms.
- **CloudShell:** chạy AWS CLI và hỗ trợ vận hành.

## Giao tiếp runtime

```text
User → Nginx frontend → /api → Flask backend → PostgreSQL
                           ↓
                     JWT authorization
```

## Tính truy vết

Docker image sử dụng tag dựa trên Git commit; Elastic Beanstalk version sử dụng định dạng:

```text
gh-<commit-sha>-<workflow-run-id>-<attempt>
```

Nhờ đó, phiên bản đang chạy có thể đối chiếu với commit và workflow đã tạo ra nó.
