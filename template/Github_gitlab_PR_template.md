## 📌 Mục đích của Pull Request
<!-- Mô tả ngắn gọn lý do tạo PR này -->
Thêm tính năng đăng nhập người dùng và xử lý lỗi xác thực.

---

## ✅ Các thay đổi chính
<!-- Liệt kê các thay đổi nổi bật -->
- Thêm component `LoginForm`
- Tích hợp API `/auth/login`
- Xử lý lỗi sai mật khẩu và tài khoản không tồn tại
- Viết unit test cho `LoginForm`

---

## 🧪 Kiểm thử
<!-- Mô tả cách bạn đã test PR này -->
- [x] Đã test UI trên Chrome, Firefox
- [ ] Đã chạy toàn bộ unit test (`npm test`)
- [ ] Đã kiểm thử API với dữ liệu giả


## 🔍 Reviewer cần chú ý
<!-- Gợi ý phần code cần review kỹ -->
- Logic xử lý lỗi trong `handleLogin()`
- Kiểm tra lại điều kiện validate form

---

## 📚 Liên quan đến
<!-- Liệt kê các issue/ticket liên quan -->
- Closes #123
- Relates to #456

---

## 🧹 Checklist trước khi merge
- [x] Đã rebase từ `dev` mới nhất
- [ ] Không còn xung đột
- [ ] Đã cập nhật tài liệu nếu cần