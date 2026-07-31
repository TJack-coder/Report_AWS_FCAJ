---
title: "Điều kiện tiên quyết"
linkTitle: "5.2. Điều kiện tiên quyết"
weight: 2
---


## Công cụ và tài khoản

- Tài khoản AWS có quyền IAM, ECR, S3, EC2, Elastic Beanstalk và CloudWatch.
- GitHub repository chứa source code CloudLibrary.
- Git, Docker Desktop, Docker Compose.
- Python 3, `pip`, Node.js và `npm`.
- AWS CLI hoặc AWS CloudShell.
- IAM role cho GitHub Actions được cấu hình qua OpenID Connect.

## Tài nguyên dự án

| Tài nguyên | Giá trị |
|---|---|
| AWS Region | `ap-southeast-2` |
| Backend ECR repository | `aws-library-backend` |
| Frontend ECR repository | `aws-library-frontend` |
| Elastic Beanstalk application | `aws-library-system` |
| Elastic Beanstalk environment | `Aws-library-system-env` |
| GitHub deployment role | `aws-library-github-deploy` |
| EC2 instance role | `aws-elasticbeanstalk-ec2-role` |
| Deployment branch | `develop_2.0` |

## Kiểm tra cấu trúc dự án

```text
.github/workflows/
.platform/hooks/
aws/
backend/
cloudwatch/
deploy/
frontend/
docker-compose.yml
.env.example
```

## Quy tắc bảo mật

- Không commit `.env`, access key, session token hoặc mật khẩu.
- Dùng GitHub OIDC thay vì AWS access key dài hạn.
- Secret được cấu hình bằng Elastic Beanstalk environment properties/GitHub variables.
- Trước khi public file kỹ thuật, thay account ID bằng placeholder.
