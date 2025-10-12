Dưới đây là một **quy trình chuẩn để thực hiện combine merge** — tức là gộp nhiều nhánh `feat/` hoặc `fix/` vào một nhánh trung gian trước khi merge vào `dev`. Quy trình này giúp kiểm soát chất lượng, giảm xung đột và đảm bảo mọi thay đổi đều được kiểm thử kỹ lưỡng.

---

## ✅ QUY TRÌNH COMBINE MERGE CHUẨN

### 📌 Mục tiêu
- Gộp nhiều nhánh nhỏ (`feat/`, `fix/`) vào một nhánh trung gian (`combine/feature-group`) để kiểm thử và review trước khi merge vào `dev`.

---

### 🧩 Bước 1: Xác định các nhánh cần combine
- Chọn các nhánh có liên quan về mặt chức năng hoặc thời điểm release.
- Ví dụ: `feat/login`, `feat/register`, `fix/login-error` → cùng thuộc nhóm `auth`.

---

### 🌿 Bước 2: Tạo nhánh combine trung gian
```bash
git checkout dev
git pull origin dev
git checkout -b combine/auth-features
```

---

### 🔀 Bước 3: Merge từng nhánh con vào nhánh combine
```bash
git merge origin/feat/login
git merge origin/feat/register
git merge origin/fix/login-error
```

> ⚠️ Nếu có xung đột, xử lý ngay và commit lại.

---

### 🧪 Bước 4: Kiểm thử và review
- Chạy toàn bộ test (unit test, integration test, UI test…).
- Đảm bảo không có lỗi build, test fail hoặc bug mới.
- Tạo Pull Request từ `combine/auth-features` → `dev` để review.

---

### ✅ Bước 5: Merge vào `dev`
- Sau khi review OK và test pass:
  - **Squash and merge** nếu muốn gọn lịch sử.
  - **Merge commit** nếu muốn giữ lịch sử từng nhánh.

---

### 🧹 Bước 6: Dọn dẹp
- Xóa nhánh `combine/auth-features` nếu không còn dùng.
- Cân nhắc xóa các nhánh `feat/`, `fix/` đã merge nếu không cần giữ.

---

## 📘 Gợi ý đặt tên nhánh combine
| Mục đích | Tên nhánh gợi ý |
|---------|-----------------|
| Nhóm tính năng auth | `combine/auth-features` |
| Nhóm bugfix cho release 1.2 | `combine/fix-release-1.2` |
| Nhóm UI cải tiến | `combine/ui-enhancements` |
