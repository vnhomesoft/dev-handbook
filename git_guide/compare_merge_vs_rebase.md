# Merge vs Rebase

## So sánh
**Nên dùng `merge` khi muốn giữ lịch sử commit đầy đủ và rõ ràng; dùng `rebase` khi muốn lịch sử gọn gàng, tuyến tính. Mỗi cách có ưu và nhược điểm riêng tùy vào mục tiêu làm việc nhóm hoặc cá nhân.**

Dưới đây là phân tích chi tiết về hai lệnh phổ biến trong Git: `merge` và `rebase`.

---

### 🔀 Git Merge

**Cách hoạt động:**  
`git merge` kết hợp nội dung của một nhánh vào nhánh hiện tại bằng cách tạo một commit hợp nhất (merge commit).

**Ưu điểm:**
- *Giữ nguyên lịch sử commit*: Lịch sử phát triển được bảo toàn, giúp dễ truy vết.
- *An toàn khi làm việc nhóm*: Không thay đổi commit gốc, tránh xung đột khi nhiều người cùng làm việc.

**Nhược điểm:**
- *Lịch sử phức tạp*: Có thể tạo ra nhiều nhánh rẽ, khó đọc nếu có nhiều merge.
- *Tạo thêm commit không cần thiết*: Merge commit đôi khi không mang nhiều ý nghĩa.

**Khi nên dùng:**
- Khi làm việc nhóm và muốn giữ lịch sử đầy đủ.
- Khi tích hợp nhánh đã được chia sẻ với người khác.
- Khi thực hiện pull request trên GitHub/GitLab.

---

### 🔁 Git Rebase

**Cách hoạt động:**  
`git rebase` di chuyển toàn bộ commit của một nhánh lên đầu nhánh khác, tạo lại commit mới theo thứ tự tuyến tính.

**Ưu điểm:**
- *Lịch sử gọn gàng*: Không có merge commit, dễ đọc và theo dõi.
- *Dễ kiểm tra từng thay đổi*: Mỗi commit được giữ riêng biệt.

**Nhược điểm:**
- *Thay đổi lịch sử commit*: Có thể gây xung đột nếu nhánh đã được chia sẻ.
- *Yêu cầu hiểu rõ Git*: Dễ gây lỗi nếu không cẩn thận.

**Khi nên dùng:**
- Khi làm việc cá nhân hoặc trước khi push lên remote.
- Khi muốn làm sạch lịch sử trước khi tạo pull request.
- Khi cần tích hợp thay đổi từ `main` vào nhánh feature mà chưa chia sẻ với ai.

---

### ✅ Quy tắc chọn lựa

| Tình huống | Nên dùng |
|-----------|----------|
| Làm việc nhóm, nhánh đã chia sẻ | `merge` |
| Làm việc cá nhân, chưa push | `rebase` |
| Muốn giữ lịch sử rõ ràng | `merge` |
| Muốn lịch sử gọn gàng, tuyến tính | `rebase` |

Nguồn: [200Lab Blog](https://200lab.io/blog/git-rebase-vs-git-merge), [Viblo](https://viblo.asia/p/so-sanh-merge-va-rebase-trong-git-63vKjwa6Z2R), [TopDev](https://topdev.vn/blog/merge-vs-rebase-trong-git/)

---

## Hướng dẫn sử dụng rebase an toàn

**Để sử dụng `git rebase` an toàn, bạn nên thực hiện trên nhánh chưa chia sẻ, luôn sao lưu trước khi rebase, và kiểm tra kỹ xung đột. Tránh rebase các nhánh đã được push lên remote hoặc đang được người khác sử dụng.**


### ✅ Các bước sử dụng `git rebase` an toàn

1. **Đảm bảo nhánh chưa được chia sẻ**
   - *Chỉ rebase nhánh local* chưa được push lên remote hoặc chưa có người khác làm việc chung.
   - Nếu đã chia sẻ, hãy cân nhắc dùng `merge` thay vì `rebase`.

2. **Sao lưu trước khi rebase**
   - Tạo một nhánh phụ để lưu trạng thái hiện tại:
     ```bash
     git branch backup-before-rebase
     ```

3. **Kiểm tra trạng thái làm việc**
   - Đảm bảo không có thay đổi chưa commit:
     ```bash
     git status
     ```

4. **Thực hiện rebase**
   - Ví dụ: rebase nhánh `feature` lên `main`
     ```bash
     git checkout feature
     git rebase main
     ```

5. **Xử lý xung đột nếu có**
   - Git sẽ dừng lại và yêu cầu bạn sửa xung đột.
   - Sau khi sửa, dùng:
     ```bash
     git add .
     git rebase --continue
     ```

6. **Kiểm tra lại lịch sử**
   - Dùng `git log` để xem lịch sử commit sau khi rebase.

7. **Sử dụng tùy chọn nâng cao**
   - `--interactive` để chỉnh sửa, gộp, bỏ qua commit:
     ```bash
     git rebase -i main
     ```
   - `--autosquash` để tự động gộp commit được đánh dấu `fixup!` hoặc `squash!`.

---

### ⚠️ Những điều cần tránh

- Không rebase nhánh đã được push lên remote trừ khi bạn là người duy nhất làm việc trên đó.
- Không rebase nhánh có nhiều người đang làm việc chung mà chưa thống nhất.
- Không rebase khi có nhiều xung đột phức tạp nếu bạn chưa quen xử lý.

---

### 🧠 Mẹo nâng cao

- Dùng `git rerere` để ghi nhớ cách bạn xử lý xung đột và tự động áp dụng lần sau.
- Luôn kiểm tra lại bằng `git log --oneline --graph` để đảm bảo lịch sử commit đúng như mong muốn.

Nguồn: [CodeGym](https://codegym.vn/blog/huong-dan-su-dung-git-rebase-tu-co-ban-den-nang-cao/), [Cafedev](https://cafedev.vn/tu-hoc-git-lenh-git-rebase/), [CareerLink](https://www.careerlink.vn/cam-nang-viec-lam/tu-van-nghe-nghiep/git-rebase-la-gi)
