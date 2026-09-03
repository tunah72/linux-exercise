# Tổng hợp báo cáo bài tập Linux — Nhập môn DevOps

## Danh sách các báo cáo

| # | Nhóm bài tập | File report | Số bài tập | Số screenshot |
|---|--------------|-------------|------------|---------------|
| 1 | User & Group | [01-user-group-report.md](./01-user-group-report.md) | 2 | 6 |
| 2 | Phân quyền file và thư mục | [02-permission-report.md](./02-permission-report.md) | 2 | 5 |
| 3 | Quản lý xuất nhập file | [03-file-io-report.md](./03-file-io-report.md) | 13 | 13 |
| 4 | Quản lý gói phần mềm | [04-package-management-report.md](./04-package-management-report.md) | 9 | 9 |
| 5 | Quản lý dịch vụ | [05-service-management-report.md](./05-service-management-report.md) | 5 | 10 |
| 6 | Quản lý File System | [06-filesystem-report.md](./06-filesystem-report.md) | 9 | 14 |
| 7 | Bash Script & Crontab | [07-bash-script-report.md](./07-bash-script-report.md) | 11 | 13 |
| 8 | Khắc phục lỗi Network & Services | [08-network-troubleshooting-report.md](./08-network-troubleshooting-report.md) | 10 | 12 |
| | **Tổng cộng** | | **61 bài tập** | **82 screenshot** |

## Thứ tự thực hiện khuyến nghị

Thực hiện các nhóm bài tập theo đúng thứ tự trên vì có sự phụ thuộc:

1. **User & Group** → tạo user `peter`, `bigman` cần cho bài phân quyền
2. **Phân quyền** → sử dụng user `peter` từ bước 1
3. **Xuất nhập file** → thao tác file cơ bản
4. **Quản lý gói phần mềm** → cài `nginx`, `vsftpd` cho bước sau
5. **Quản lý dịch vụ** → sử dụng `nginx` đã cài
6. **Quản lý File System** → cần đĩa `/dev/sdb` trong VM
7. **Bash Script & Crontab** → viết script tự động hóa
8. **Network & Services** → kiểm tra mạng, firewall

## Lưu ý khi chụp Screenshot

- Chụp **toàn bộ cửa sổ terminal** để thấy rõ lệnh đã gõ và kết quả.
- Đặt tên file screenshot theo format: `<số nhóm>-<số bài>-<mô tả>.png`
  - Ví dụ: `01-01-create-users.png`, `07-03-sum-script.png`
- Với các bước có nhiều lệnh liên tiếp, có thể gộp vào **1 screenshot** nếu terminal đủ dài.
- Đảm bảo **font size đủ lớn** để đọc được trong báo cáo LaTeX.
