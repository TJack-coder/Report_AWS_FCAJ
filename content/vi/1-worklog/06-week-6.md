---
title: "Tuần 6 - Tự động hóa triển khai hoàn chỉnh"
linkTitle: "1.6. Nhật ký Tuần 6"
weight: 6
---

**Thời gian:** 20/07/2026 - 24/07/2026

| Ngày | Ngày thực hiện | Công việc chính |
|---:|---|---|
| 2 | 20/07 | Mở rộng workflow để build/push image theo commit. |
| 3 | 21/07 | Tự động hóa deployment bundle, S3 upload, application version và update environment. |
| 4 | 22/07 | Thêm vòng lặp kiểm tra running version, `Status: Ready` và `Health: Ok`. |
| 5 | 23/07 | Khắc phục quyền IAM còn thiếu cho CloudFormation, S3 và Auto Scaling. |
| 6 | 24/07 | Tích hợp thay đổi của nhóm và xác nhận push `develop_2.0` kích hoạt deployment. |

**Kết quả:** hoàn thành pipeline từ source-code push đến môi trường AWS.
