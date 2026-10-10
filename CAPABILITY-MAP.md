# Capability Map: AptisLearn persistence + deploy

| Module id | Responsibility | Depends on |
|---|---|---|
| persistence | Lưu đáp án + tiến độ + làm lại, khôi phục khi mở lại (localStorage từng máy) | — |
| deploy | Public URL https qua GitHub Pages để luyện trên điện thoại | persistence |

Build order: persistence → deploy
