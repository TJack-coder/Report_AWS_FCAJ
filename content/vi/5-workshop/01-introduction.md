---
title: "Tổng quan và Mục tiêu"
linkTitle: "5.1. Giới thiệu"
weight: 1
---


## Tổng quan

CloudLibrary là ứng dụng web full-stack được container hóa, gồm:

- **Frontend:** React, Vite và Nginx.
- **Backend:** Python Flask, Flask-SQLAlchemy và Gunicorn.
- **Database:** PostgreSQL.
- **Container:** Docker và Docker Compose.
- **Source control:** GitHub.
- **CI/CD:** GitHub Actions.
- **Registry:** Amazon ECR.
- **Deployment:** AWS Elastic Beanstalk.
- **Monitoring:** Amazon CloudWatch.

{{< report-figure src="images/cloudlibrary-interface.png" alt="Dashboard quản trị CloudLibrary" caption="Giao diện dashboard của hệ thống CloudLibrary." >}}

## Mục tiêu workshop

Sau khi hoàn thành, người đọc có thể:

1. Kiểm tra cấu trúc dự án và chạy hệ thống bằng Docker Compose.
2. Chạy test Flask backend và build React frontend.
3. Cấu hình GitHub OIDC và IAM role cho CI/CD.
4. Build và push Docker image lên Amazon ECR.
5. Tạo deployment bundle và application version.
6. Triển khai, xác minh, giám sát và rollback trên Elastic Beanstalk.
7. Phân tích lỗi bằng GitHub Actions, Elastic Beanstalk và CloudWatch.

## Luồng tự động hóa

Một commit mới trên `develop_2.0` kích hoạt pipeline. Pipeline kiểm thử backend, build frontend, build/push hai Docker image, tạo gói triển khai, cập nhật Elastic Beanstalk và xác minh version/health.
