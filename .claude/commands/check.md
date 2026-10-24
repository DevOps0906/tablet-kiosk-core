---
description: 정적 분석 · 테스트 · 포맷 확인 후 결과 요약
---
존재하는 프로젝트만 실행하고, 결과를 표(항목 / 결과 / 실패 내용)로 요약한다. 실패는 원인과 고칠 방법을 제안하되 사용자가 요청하기 전에는 고치지 않는다.

- apps/kiosk: `dart format --output=none --set-exit-if-changed .`, `flutter analyze`, `flutter test`
- packages/kiosk_devices: `flutter analyze`, `flutter test`
- apps/admin: `pnpm lint`, `pnpm typecheck`(있으면), `pnpm test`
- supabase: `supabase test db` (로컬 Supabase가 켜져 있을 때)
