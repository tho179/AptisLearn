## Task 1: save/restore đáp án + tab/view
**Description:** Tự lưu value từng select + tab + view vào localStorage, reload khôi phục.
**Acceptance:**
- [ ] Chọn đáp án → reload → còn nguyên
- [ ] Đổi tab/view → reload → đúng tab/view cũ
**Verification:**
- [ ] Manual reload Chrome + mobile viewport 360px
- [ ] DevTools thấy `aptis_progress_v1`
**Dependencies:** None
**Files:** `index.html`
**Estimated scope:** Small: 1 file

## Task 2: save/restore kết quả + nút Làm lại
**Description:** Lưu kết quả chấm từng đoạn, thêm nút Làm lại topic hiện tại.
**Acceptance:**
- [ ] Nộp bài → reload → ✔/✘ còn nguyên
- [ ] Làm lại → confirm → xóa đáp án + result topic đó
**Verification:**
- [ ] Manual: chấm → reload → reset → reload trống
**Dependencies:** Task 1
**Files:** `index.html`
**Estimated scope:** Small: 1 file

## Checkpoint: After Tasks 1-2
- [ ] Reload giữ bài, reset sạch, không vỡ mobile
- [ ] Review với user trước deploy

## Task 3: deploy GitHub Pages
**Description:** Commit + push `main`, bật Pages, verify URL phone.
**Acceptance:**
- [ ] `https://tho179.github.io/AptisLearn/` 200, đủ 4 topics
- [ ] Mở trên phone (4G) thao tác y PC, reload giữ data
**Verification:**
- [ ] `curl -I` + mở ẩn danh + mở phone thật
**Dependencies:** Task 1, Task 2
**Files:** none (config GitHub)
**Estimated scope:** XS
