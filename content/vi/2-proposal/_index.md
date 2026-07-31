---
title: "Đề xuất dự án"
linkTitle: "2. Proposal"
weight: 2
---


## Tổng quan dự án

CloudLibrary là ứng dụng web quản lý thư viện trên nền tảng đám mây, hỗ trợ quản lý sách, người dùng, mượn/trả, gia hạn, đặt trước, thông báo và nghiệp vụ quản trị. Hệ thống sử dụng **React + Vite + Nginx** ở frontend, **Flask + Gunicorn** ở backend và **PostgreSQL** cho dữ liệu quan hệ.

Mục tiêu không chỉ là xây dựng ứng dụng hoạt động tốt mà còn áp dụng DevOps và cloud-native practices: container hóa, CI/CD, image registry, managed deployment và centralized monitoring.

## Mục tiêu

- Xây dựng hệ thống mượn và quản lý sách trên web.
- Xác thực JWT và phân quyền Admin/User.
- CRUD, khôi phục, import/export dữ liệu sách.
- Mượn, trả, gia hạn, đặt trước và thông báo.
- Docker hóa frontend và backend.
- Tự động hóa CI/CD bằng GitHub Actions.
- Lưu image trong Amazon ECR và triển khai bằng Elastic Beanstalk.
- Quan sát logs, CPU, memory, latency, lỗi HTTP và health bằng CloudWatch.

## Kế hoạch theo giai đoạn

1. **Phát triển ứng dụng cốt lõi:** danh sách sách, chi tiết, CRUD, database models và API.
2. **Xác thực và phân quyền:** đăng nhập, đăng ký, JWT, password reset và role-based access.
3. **Nghiệp vụ thư viện:** mượn, trả, gia hạn, đặt trước, tiền phạt và thông báo.
4. **Containerization và CI/CD:** Docker, Docker Compose và GitHub Actions.
5. **AWS deployment và monitoring:** ECR, S3, Elastic Beanstalk, CloudWatch và CloudShell.

## Ngăn xếp công nghệ

| Tầng | Công nghệ/Dịch vụ |
|---|---|
| Frontend | React, Vite, Nginx |
| Backend | Flask, Flask-SQLAlchemy, Gunicorn |
| Authentication | JWT |
| Database | PostgreSQL |
| Containerization | Docker, Docker Compose |
| CI/CD | GitHub Actions |
| Container Registry | Amazon ECR |
| Deployment | AWS Elastic Beanstalk |
| Monitoring | Amazon CloudWatch |
| Cloud Operations | AWS CloudShell |

## Kiến trúc và luồng triển khai

{{< report-figure src="images/architecture-current.svg" alt="Kiến trúc triển khai hiện tại của CloudLibrary" caption="Kiến trúc hiện tại: PostgreSQL chạy dưới dạng container trong môi trường Elastic Beanstalk/EC2; Amazon RDS là hướng cải tiến trong tương lai." >}}

1. Developer đẩy mã nguồn lên GitHub.
2. GitHub Actions kiểm thử, build frontend/backend và Docker image.
3. Image được lưu trong Amazon ECR.
4. Deployment bundle được upload lên S3 và tạo Elastic Beanstalk application version.
5. Elastic Beanstalk chạy `frontend`, `backend`, `db` bằng Docker Compose.
6. CloudWatch thu thập logs, metrics, health và alarms.

## Bảo mật

- GitHub Actions xác thực với AWS qua OpenID Connect.
- IAM role giới hạn theo repository và branch.
- Secret không lưu trong mã nguồn.
- JWT và role-based access bảo vệ backend APIs.
- File `.env` và access key bị loại khỏi Git repository.

## Khả năng mở rộng

Phiên bản hiện tại ưu tiên tính đơn giản và khả năng tái tạo. Các cải tiến tiếp theo có thể gồm Amazon RDS, S3/CloudFront cho media, SES cho email, HTTPS/custom domain và ECS/EKS khi cần orchestration nâng cao.

## Kết quả kỳ vọng

Một ứng dụng thư viện full-stack có thể được kiểm thử, đóng gói, triển khai và giám sát thông qua một quy trình thống nhất, cung cấp cả giá trị nghiệp vụ và trải nghiệm thực tế về software delivery trên AWS.
