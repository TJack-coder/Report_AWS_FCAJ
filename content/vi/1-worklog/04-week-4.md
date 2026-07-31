---
title: "Tuần 4 - ECR, IAM và GitHub OIDC"
linkTitle: "1.4. Nhật ký Tuần 4"
weight: 4
---

**Thời gian:** 06/07/2026 - 10/07/2026

| Ngày | Ngày thực hiện | Công việc chính |
|---:|---|---|
| 2 | 06/07 | Cấu hình AWS CLI và vùng `ap-southeast-2`. |
| 3 | 07/07 | Tạo `aws-library-backend` và `aws-library-frontend` trên Amazon ECR. |
| 4 | 08/07 | Cấu hình GitHub OIDC và IAM role `aws-library-github-deploy`. |
| 5 | 09/07 | Chuẩn bị quyền ECR, S3, Elastic Beanstalk, CloudFormation và Auto Scaling. |
| 6 | 10/07 | Build, gắn tag, push Docker image và kiểm tra digest trên ECR. |

**Kết quả:** GitHub Actions kết nối AWS bằng thông tin xác thực tạm thời thay cho access key dài hạn.
