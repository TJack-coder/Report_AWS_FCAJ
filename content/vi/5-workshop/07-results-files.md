---
title: "Kết quả và File đính kèm"
linkTitle: "5.7. Kết quả và File đính kèm"
weight: 7
---


## Kết quả đạt được

- Frontend và backend được đóng gói thành Docker image riêng.
- Image được lưu trong private Amazon ECR repositories.
- GitHub Actions tự động test, build và triển khai.
- GitHub Actions xác thực AWS thông qua OIDC.
- Push lên `develop_2.0` kích hoạt deployment.
- Elastic Beanstalk quản lý Docker environment và application versions.
- CloudWatch thu thập logs, metrics, health và alarms.
- Deployment lỗi có thể điều tra và rollback.

{{< report-figure src="images/cloudlibrary-production.png" alt="CloudLibrary production book catalog" caption="Kết quả cuối: giao diện kho sách hoạt động trên môi trường triển khai." >}}

## File kỹ thuật đính kèm

Các file dưới đây được trích từ source code và **đã thay AWS account ID bằng placeholder** trước khi công khai.

{{< download path="files/attachments/docker-compose.yml" label="docker-compose.yml" meta="Local integration: db, backend, frontend" >}}
{{< download path="files/attachments/backend.Dockerfile" label="Backend Dockerfile" meta="Flask + Gunicorn image" >}}
{{< download path="files/attachments/frontend.Dockerfile" label="Frontend Dockerfile" meta="React build + Nginx runtime" >}}
{{< download path="files/attachments/beanstalk-compose.template.yml" label="Beanstalk Compose template" meta="Production deployment bundle template" >}}
{{< download path="files/attachments/ci.yml" label="GitHub Actions CI" meta="Backend tests and frontend build" >}}
{{< download path="files/attachments/deploy.yml" label="GitHub Actions deployment" meta="ECR, S3 and Elastic Beanstalk pipeline" >}}
{{< download path="files/attachments/setup-github-oidc.example.sh" label="GitHub OIDC setup script" meta="Sanitized AWS IAM configuration" >}}
{{< download path="files/attachments/setup-cloudwatch.sh" label="CloudWatch setup script" meta="Dashboard, metrics and alarms" >}}
{{< download path="files/attachments/env.example" label="Environment example" meta="Placeholder values only" >}}

## Kết luận workshop

Luồng triển khai đã chuyển CloudLibrary từ một ứng dụng full-stack chạy local thành một hệ thống AWS có khả năng kiểm thử, đóng gói, phát hành, giám sát và phục hồi theo quy trình thống nhất. Kết quả quan trọng nhất là deployment trở nên **repeatable, traceable và mostly automated**.
