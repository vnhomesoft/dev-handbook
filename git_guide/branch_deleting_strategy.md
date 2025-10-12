Một chiến lược merge hiệu quả **phải đi kèm với chiến lược xóa nhánh hợp lý và an toàn** để tránh rối repo, giảm nguy cơ lỗi và giữ cho lịch sử Git sạch sẽ. 
Dưới đây là một quy trình chuẩn bạn có thể áp dụng:

---

## 🧹 Chiến lược xóa nhánh sau khi merge

### ✅ 1. **Chỉ xóa nhánh sau khi đã merge thành công**
- Kiểm tra kỹ nhánh đã được merge vào `dev`, `main`, hoặc `release`.
- Dùng lệnh kiểm tra:
  ```bash
  git branch --merged dev
  ```
- Nếu nhánh đã merge, bạn có thể xóa bằng:
  ```bash
  git branch -d feat/login-form
  ```
  > ⚠️ Dùng `-d` để xóa an toàn. Nếu chưa merge, Git sẽ cảnh báo.

---

### 🛡️ 2. **Không xóa nhánh chưa được review hoặc chưa test**
- Nếu nhánh chưa được review hoặc chưa pass CI/CD → giữ lại.
- Gắn nhãn `WIP` (Work In Progress) hoặc `do-not-delete` để tránh xóa nhầm.

---

### 🧭 3. **Xóa nhánh local và remote**
- Sau khi merge và review xong, xóa cả local và remote:
  ```bash
  git branch -d feat/login-form           # local
  git push origin --delete feat/login-form  # remote
  ```

---

### 📦 4. **Tự động xóa nhánh sau khi merge (GitHub/GitLab)**
- Bật tùy chọn **"Automatically delete head branches"** trong repo settings.
- Giúp repo sạch sẽ, không cần thao tác thủ công.

---

### 📋 5. **Lưu lịch sử nếu cần rollback**
- Trước khi xóa nhánh, đảm bảo commit đã được lưu trong `dev` hoặc `main`.
- Nếu cần backup, có thể tag:
  ```bash
  git tag backup/feat-login HEAD
  ```

---

### 🔄 6. **Lập lịch dọn dẹp định kỳ**
- Mỗi tuần/tháng, kiểm tra các nhánh cũ:
  ```bash
  git branch --merged dev
  git branch --no-merged dev
  ```
- Xóa các nhánh đã merge và không còn dùng.

---

## 🧠 Gợi ý quy tắc đặt tên giúp dễ quản lý
| Loại nhánh | Quy tắc tên | Tự động nhận diện |
|------------|-------------|-------------------|
| Feature    | `feat/*`    | Dễ lọc bằng `git branch | grep feat` |
| Bugfix     | `fix/*`     | Dễ phân loại khi cleanup |
| Combine    | `combine/*` | Xóa sau khi merge vào `dev` |
