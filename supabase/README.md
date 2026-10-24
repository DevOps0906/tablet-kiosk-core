# supabase

서버: Postgres(스키마 `kiosk`) · Auth · Realtime · Edge Functions. **task-005**에서 `supabase init`으로 설정 파일을 만듭니다.

```
supabase/
├── config.toml          (task-005에서 생성)
├── migrations/          0001_init.sql, 0002_... — 기존 번호 파일 수정 금지
├── functions/           Edge Functions (Deno · TypeScript)
│   ├── device-register/   기기 등록 코드 → 기기 계정 발급
│   ├── order-confirm/     주문 확정 + 주문번호 발급
│   ├── coupon-issue/      쿠폰 캠페인 · 시리얼 생성
│   ├── coupon-check/      시리얼 검증 · 할인 계산
│   ├── coupon-reserve/    결제 중 예약
│   ├── coupon-redeem/     사용 확정
│   └── coupon-release/    예약 해제
├── seed.sql             업종별 예시 메뉴 (설계 저장소 docs/02-menu-seed.md 기준)
└── tests/               pgTAP — RLS · 함수 테스트
```

설계: `docs/07-data-model.md`, `docs/06-coupon.md`.

## 규칙

- 마이그레이션은 **추가만**. 잘못 만든 것도 고치지 말고 새 파일로 바로잡습니다.
- 모든 매장 데이터 테이블에 RLS를 켜고, "다른 매장 데이터가 안 보인다" 테스트를 같이 추가합니다.
- service role 키가 필요한 일은 Edge Function 안에서만 합니다.
- 비밀 값은 `supabase secrets set`으로 넣고, 이름만 `.env.example`에 적습니다.
