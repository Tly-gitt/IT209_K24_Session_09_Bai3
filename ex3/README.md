# BÁO CÁO BÀI TẬP

---

## 1. Cấu trúc mã nguồn

- `index.html`: Chứa nội dung hiển thị của website.
- `Dockerfile`: Chứa các chỉ thị đóng gói ứng dụng vào image Nginx.

### Nội dung Dockerfile:
```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

---

## 2. Các bước thực hiện trên PowerShell

1. **Xây dựng Docker Image:**
   ```powershell
   docker build -t my-html-app:v1 .
   ```

2. **Khởi chạy container chạy ngầm (detached) và ánh xạ cổng 8081:**
   ```powershell
   docker run -d -p 8081:80 --name html-app my-html-app:v1
   ```

---

## 3. Kết quả nghiệm thu (Verification)

### a. Kiểm tra phản hồi HTTP qua lệnh curl
- **Lệnh thực thi trên PowerShell:**
  ```powershell
  curl.exe http://localhost:8081
  ```
- **Kết quả trả về:**
  ```html
  <h1>Hello Docker Session 09!</h1>
  ```

### b. Kiểm tra trạng thái container đang hoạt động
- **Lệnh thực thi:**
  ```powershell
  docker ps -f name=html-app
  ```
- **Kết quả Terminal:**
  ```text
  CONTAINER ID   IMAGE            COMMAND                  CREATED         STATUS         PORTS                  NAMES
  3f8b1a9c4d2e   my-html-app:v1   "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   0.0.0.0:8081->80/tcp   html-app
  ```

---

## 4. Kết luận
- Trang HTML tĩnh đã được đóng gói thành công vào container Nginx siêu nhẹ (`alpine`).
- Container khởi chạy ổn định và lắng nghe phản hồi chính xác tại cổng `8081` trên máy Windows.