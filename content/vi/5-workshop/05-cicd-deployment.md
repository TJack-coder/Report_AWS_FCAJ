---
title: "CI/CD và Triển khai AWS"
linkTitle: "5.5. CI/CD và Triển khai AWS"
weight: 5
---


## Tạo Amazon ECR repositories

```bash
aws ecr create-repository \
  --repository-name aws-library-backend \
  --region ap-southeast-2

aws ecr create-repository \
  --repository-name aws-library-frontend \
  --region ap-southeast-2
```

{{< report-figure src="images/ecr-repositories.png" alt="Hai Amazon ECR repositories" caption="Hai private repositories lưu Docker image của frontend và backend." >}}

## GitHub OIDC và IAM

Workflow yêu cầu `id-token: write`, sau đó sử dụng GitHub repository variable `AWS_ROLE_ARN` để assume IAM role. Trust policy giới hạn theo owner, repository và branch `develop_2.0`.

```yaml
permissions:
  contents: read
  id-token: write

- name: Configure AWS credentials
  uses: aws-actions/configure-aws-credentials@v6.2.0
  with:
    role-to-assume: ${{ vars.AWS_ROLE_ARN }}
    aws-region: ap-southeast-2
```

## Các bước chính của workflow

1. Checkout source.
2. Cài Python dependencies và chạy test.
3. Cài Node dependencies và build React.
4. Assume AWS role bằng OIDC.
5. Login ECR.
6. Build/push backend và frontend image.
7. Render Docker Compose deployment template.
8. ZIP bundle và upload S3.
9. Tạo Elastic Beanstalk application version.
10. Update environment và chờ deployment.
11. Kiểm tra version, status, health và endpoint.

{{< report-figure src="images/github-actions-workflow.png" alt="Danh sách workflow GitHub Actions" caption="Các lần chạy pipeline cho nhánh develop_2.0, bao gồm cả lần lỗi và lần thành công." >}}

## Kích hoạt deployment

```bash
git switch develop_2.0
git add -A
git commit -m "feat: deploy CloudLibrary to AWS"
git push origin develop_2.0
```

## Application version

Deployment bundle chứa Docker Compose đã render và các cấu hình `.ebextensions`/`.platform`. Bundle được upload lên S3 rồi đăng ký thành application version.

{{< report-figure src="images/beanstalk-application-version.png" alt="Elastic Beanstalk environment overview" caption="Elastic Beanstalk environment đạt Health: Ok và chạy một application version có thể truy vết." >}}

## Điều kiện xác minh thành công

```text
Status: Ready
Health: Ok
Running version: gh-<new-version>
Public health endpoint: HTTP 200
```
