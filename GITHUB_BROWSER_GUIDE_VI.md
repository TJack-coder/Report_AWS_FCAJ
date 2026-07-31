# Hướng dẫn cập nhật giao diện FCAJ bằng trình duyệt

1. Giải nén file ZIP.
2. Trên macOS, nhấn `Command + Shift + .` để hiện `.github` và `.devcontainer`.
3. Xóa các file cũ trong repository `Report_AWS` hoặc upload đè toàn bộ **nội dung bên trong** thư mục giải nén vào thư mục gốc.
4. Đảm bảo có các file ở đúng vị trí:
   - `hugo.yaml`
   - `go.mod`
   - `.github/workflows/hugo.yaml`
   - `content/en/...`
   - `content/vi/...`
5. Commit trực tiếp vào `main`.
6. Vào **Actions → Build and deploy Hugo report** và chờ cả `build` lẫn `deploy` chuyển xanh.
7. Mở `https://tjack-coder.github.io/Report_AWS/` và tải lại mạnh bằng `Command + Shift + R`.

Workflow sẽ tự tải Hugo Relearn v7.2.1, vì vậy không cần tải theme về máy.
