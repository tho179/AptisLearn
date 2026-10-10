# Spec: deploy

## Objective
Có URL https public mở được trên điện thoại để luyện, không cần cắm cáp hay cùng WiFi. Dùng GitHub Pages vì miễn phí, giữ nguyên repo.

## Tech Stack
- GitHub Pages, branch `main`, root `/`, file phục vụ: `index.html`.
- Không build step.

## Commands
- Enable (lần đầu, chủ repo làm trên web hoặc CLI):
  `gh api repos/tho179/AptisLearn -f has_pages=true` rồi Pages → Deploy from branch → `main` / `(root)`
  hoặc web: Settings → Pages → Build and deployment → Deploy from a branch.
- Verify: `curl -I https://tho179.github.io/AptisLearn/` trả 200; mở trên Chrome Android/iOS.
- Rollback: revert commit trên `main`, Pages tự redeploy ~1-2 phút.

## Project Structure
- Không đổi code để deploy. Nếu cần custom domain sau này thêm file `CNAME` (ngoài scope).

## Code Style
- Không đổi code. Nếu phải thêm (ví dụ `<meta theme-color>`) thì 1 dòng, giữ tương thích Pages.

## Testing Strategy
- Sau bật Pages 1-2 phút: mở URL ẩn danh + mở trên điện thoại (4G, không cùng WiFi) → làm 1 câu → reload → nếu đã xong persistence thì đáp án còn.
- Check responsive 360px: tabs cuộn được, action-bar dạng bottom bar hiện tại không che nút.

## Boundaries
- Always: deploy từ `main` sau khi persistence đã merge; kiểm tra https 200 trước khi báo xong.
- Ask first: chuyển sang Netlify/Vercel, thêm custom domain, thêm backend đồng bộ.
- Never: public đáp án riêng tư nào khác, commit file môi trường, force-push `main`.

## Success Criteria
1. `https://tho179.github.io/AptisLearn/` mở được trên điện thoại, đủ 4 topics + vocab + docs.
2. Reload trên điện thoại giữ bài làm (phụ thuộc SPEC-persistence đã live).
3. Chủ repo không cần chạy lệnh lạ mỗi lần sửa: chỉ `git push origin main`.

## Open Questions
- Đã chốt GitHub Pages. Cần quyền admin repo `tho179/AptisLearn` để bật Pages lần đầu.
