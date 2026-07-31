---
title: "Workshop: Triển khai CloudLibrary lên AWS"
linkTitle: "5. Workshop"
weight: 5
---


Workshop này mô tả toàn bộ quá trình đưa CloudLibrary từ môi trường phát triển lên AWS. Nội dung được chia thành các phần độc lập để người đọc có thể thực hiện theo trình tự, đồng thời đáp ứng các yêu cầu bắt buộc về **song ngữ, hình ảnh, sơ đồ kiến trúc, code snippet và file đính kèm**.

{{< report-figure src="images/cloudlibrary-production.png" alt="Giao diện kho sách CloudLibrary trên môi trường production" caption="CloudLibrary hoạt động trên môi trường triển khai công khai." >}}

{{< notice type="warning" title="Lưu ý về kiến trúc database" >}}
Source code hiện tại chạy PostgreSQL dưới dạng container `db` trong Docker Compose trên Elastic Beanstalk/EC2. Amazon RDS chỉ được xem là phương án nâng cấp trong tương lai.
{{< /notice >}}


### Nội dung
- [5.1. Giới thiệu](01-introduction/)
- [5.2. Điều kiện tiên quyết](02-prerequisites/)
- [5.3. Kiến trúc triển khai](03-architecture/)
- [5.4. Kiểm thử và xác thực local](04-local-validation/)
- [5.5. CI/CD và Triển khai AWS](05-cicd-deployment/)
- [5.6. Giám sát và Xử lý sự cố](06-monitoring-troubleshooting/)
- [5.7. Kết quả và File đính kèm](07-results-files/)
