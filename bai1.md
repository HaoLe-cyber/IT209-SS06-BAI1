# Báo cáo Bài 1: Khảo sát FHS và Phân quyền File/Folder nâng cao

## 1. Nhật ký các lệnh đã thực hiện

### Bước 1: Khởi tạo cấu trúc thư mục
Tạo thư mục `/var/www/my-app/public` và `/var/www/my-app/logs`:
```bash
sudo mkdir -p /var/www/my-app/public
sudo mkdir -p /var/www/my-app/logs
```

### Bước 2: Phân quyền truy cập cho các thư mục
- Thư mục `public`: Phân quyền `750` (`drwxr-x---` - Owner: rwx, Group: r-x, Others: ---)
```bash
sudo chmod 750 /var/www/my-app/public
```

- Thư mục `logs`: Phân quyền `770` (`drwxrwx---` - Owner: rwx, Group: rwx, Others: ---)
```bash
sudo chmod 770 /var/www/my-app/logs
```

### Bước 3: Thay đổi chủ sở hữu và nhóm sở hữu
Gán người dùng hiện tại (`$USER`) làm Chủ sở hữu và nhóm `www-data` làm Nhóm sở hữu cho toàn bộ thư mục `/var/www/my-app`:
```bash
sudo chown -R $USER:www-data /var/www/my-app
```

---

## 2. Kiểm tra kết quả

Chạy lệnh kiểm tra cấu trúc thư mục và phân quyền:
```bash
ls -la /var/www/my-app
```

### Đầu ra (Output):
```text
total 16
drwxr-xr-x 4 ubuntu www-data 4096 Oct 24 10:00 .
drwxr-xr-x 3 root   root     4096 Oct 24 10:00 ..
drwxrwx--- 2 ubuntu www-data 4096 Oct 24 10:00 logs
drwxr-x--- 2 ubuntu www-data 4096 Oct 24 10:00 public
```

### Đánh giá kết quả:
- Thư mục `/var/www/my-app/public` có quyền `drwxr-x---` (750), đúng yêu cầu.
- Thư mục `/var/www/my-app/logs` có quyền `drwxrwx---` (770), đúng yêu cầu.
- Chủ sở hữu là user non-root (`ubuntu`) và nhóm sở hữu là `www-data`.