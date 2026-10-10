# Spec: persistence

## Objective
Khi mở lại `index.html` (PC/điện thoại, cùng trình duyệt) phải thấy nguyên những gì đã làm: đáp án đã chọn từng đoạn, kết quả chấm đúng/sai, tab đang học, view đang mở. Sau mỗi lần làm có nút Làm lại để xóa đáp án của topic hiện tại và làm mới.

User: người tự luyện Aptis Reading Part 4. Thành công = reload không mất bài làm.

## Tech Stack
- Static duy nhất `index.html`, vanilla JS + CSS, không dependency, không backend.
- Lưu trữ: `localStorage` per-device (đã chốt, không đồng bộ PC↔phone).

## Commands
- Dev: `npx serve C:\AptisLearn` rồi mở `http://localhost:3000/index.html`
- Test: mở file trực tiếp + reload kiểm tra; `node -e` check JSON keys nếu cần
- Lint: không có (single file)
- Deploy: xem `SPEC-deploy.md`

## Project Structure
```
C:\AptisLearn\
  index.html            → toàn bộ app (HTML/CSS/JS)
  SPEC-persistence.md   → spec này
  SPEC-deploy.md        → spec deploy
  CAPABILITY-MAP.md     → map module
```

## Code Style
- Tái dùng `loadJSON` / `saveJSON` có sẵn, key mới `aptis_progress_v1`.
- Ví dụ:
```js
const PROG_KEY = 'aptis_progress_v1';
let PROG = loadJSON(PROG_KEY, { answers: {}, checked: {}, activeTab: 'topic1', activeView: 'practice' });
const saveProg = () => saveJSON(PROG_KEY, PROG);
```
- Không đổi logic chấm `checkAnswers`, chỉ thêm save/restore + nút reset. `ponytail:` giữ localStorage, không thêm backend.

## Testing Strategy
- Manual (chính): chọn đáp án → reload → đáp án còn; Nộp bài → reload → result còn; đổi tab → reload → đúng tab; Làm lại → đáp án + result của topic đó trống.
- Self-check: mở DevTools Application → Local Storage thấy `aptis_progress_v1`.
- Không thêm framework test (YAGNI cho 1 file static).

## Boundaries
- Always: giữ `aptis_hl_v1`, `aptis_vocab_v1`, `aptis_para_v1` nguyên; restore sau `applyBank()` để không bị ghi đè options; test reload trên Chrome mobile viewport.
- Ask first: thêm lịch sử điểm theo ngày, đồng bộ cloud.
- Never: commit secret, đổi đáp án đúng `data-answer`, thêm dependency/build step.

## Success Criteria
1. Chọn đáp án bất kỳ → reload → select giữ nguyên value.
2. Nộp bài → reload → dòng ✔/✘ còn nguyên, không phải chấm lại.
3. Reload giữ `activeTab` (topic1-4) và `activeView` (practice/vocab/docs).
4. Nút “Làm lại” ở action-bar + từng topic: xóa answers + results của topic hiện tại, confirm trước khi xóa.
5. Không vỡ layout mobile hiện tại (action-bar bottom bar).

## Open Questions
- Đã chốt: per-device, GitHub Pages. Không còn câu hỏi mở.
