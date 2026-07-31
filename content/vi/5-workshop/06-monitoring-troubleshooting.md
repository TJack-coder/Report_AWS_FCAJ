---
title: "Giám sát và Xử lý sự cố"
linkTitle: "5.6. Giám sát và Xử lý sự cố"
weight: 6
---


## Chỉ số giám sát

Amazon CloudWatch theo dõi:

- EC2 CPU và memory.
- HTTP request count.
- p95 backend latency.
- HTTP 4xx/5xx.
- Elastic Beanstalk environment health.
- Flask/Gunicorn, Nginx, Docker và deployment logs.

{{< report-figure src="images/cloudwatch-monitoring.png" alt="CloudWatch dashboard CloudLibrary" caption="Dashboard gồm CPU/memory, environment health, traffic, p95 latency và HTTP 5xx." >}}

## Nguồn dữ liệu xử lý lỗi

- GitHub Actions job logs.
- Elastic Beanstalk Events và Enhanced Health.
- Deployment log bundle.
- `/var/log/eb-engine.log`.
- Docker container logs.
- CloudWatch Logs.

Yêu cầu log bundle:

```bash
aws elasticbeanstalk request-environment-info \
  --environment-name Aws-library-system-env \
  --info-type bundle \
  --region ap-southeast-2
```

## Sự cố thực tế: PostgreSQL credentials không đồng nhất

Backend từng dùng mật khẩu hard-code trong `DATABASE_URL`, trong khi PostgreSQL container dùng password từ Elastic Beanstalk environment properties.

```text
Credential mismatch
→ backend connection failure
→ backend health-check failure
→ frontend not started
→ Elastic Beanstalk deployment failure
```

Giải pháp: tạo `DATABASE_URL` từ cùng bộ biến:

```text
POSTGRES_USER
POSTGRES_PASSWORD
POSTGRES_DB
```

{{< report-figure src="images/deployment-error.png" alt="GitHub Actions deployment error" caption="Workflow dừng ở bước kiểm tra version và health khi môi trường ở trạng thái Red/Degraded." >}}

## Rollback

```text
Elastic Beanstalk
→ Application versions
→ Select a stable version
→ Deploy
```

Rollback giúp phục hồi dịch vụ trong khi phiên bản lỗi tiếp tục được điều tra.

## Dọn dẹp tài nguyên

- Xóa image ECR cũ.
- Xóa application version và S3 bundle không dùng.
- Điều chỉnh log retention.
- Xóa IAM policy/role không còn cần thiết.
- Không xóa tài nguyên đang phục vụ môi trường hiện tại.
