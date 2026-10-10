# Implementation Plan: persistence + deploy

## Overview
Thêm lưu tiến độ localStorage (đáp án + kết quả chấm + tab/view) và nút Làm lại vào `index.html` duy nhất, rồi public qua GitHub Pages để phone thao tác y hệt PC.

## Architecture Decisions
- Reuse `loadJSON`/`saveJSON` có sẵn, key mới `aptis_progress_v1` — không thêm lib, không backend (`ponytail:` per-device, muốn sync đa máy phải nâng cấp backend sau).
- Restore sau `applyBank()` vì hàm này rebuild `<select>` ngẫu nhiên.
- Reset per-topic, confirm trước khi xóa để chống mất data.

## Task List
- [ ] Task 1: save/restore đáp án + activeTab/activeView
- [ ] Task 2: save/restore kết quả chấm + nút Làm lại
- [ ] Checkpoint: reload giữ bài, reset sạch topic
- [ ] Task 3: deploy GitHub Pages + verify phone

## Risks and Mitigations
| Risk | Impact | Mitigation |
|------|--------|------------|
| rebuild options xóa value | Med | restore sau applyBank, giữ `cur` trong buildOptions |
| push Pages cần quyền admin | Low | hướng dẫn bật 1 click, rollback = revert commit |

## Open Questions
- Không còn — đã chốt per-device + Pages.
