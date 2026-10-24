# task-005 Supabase 1차 스키마 · RLS · 시드

- **Phase**: 1. 기반
- **선행 작업**: 없음
- **확인 위치**: 로컬 Supabase

## 목표

매장 · 기기 · 메뉴 · 주문 · 결제 테이블과 권한, 카페 예시 메뉴를 만든다.

## 참고 문서

- `docs/07-data-model.md`
- `supabase/README.md`
- `../tablet-kiosk-cafe/docs/02-menu-seed.md`

## 할 것

- [ ] `supabase init`, 스키마 `kiosk`
- [ ] 마이그레이션 0001: stores, devices, device_registration_codes, categories, menu_items, option_groups, options, menu_item_option_groups
- [ ] 마이그레이션 0002: orders, order_items, order_discounts, split_plans, payments, daily_order_counters
- [ ] RLS 정책(사장님 · 기기) + pgTAP 테스트
- [ ] `seed.sql`: 테스트 사장님 1명, 카페 매장 1곳, 카페 예시 메뉴 · 옵션

## 안 할 것 (범위 밖)

- 쿠폰 · 스탬프 테이블 (task-020, 019)
- Edge Functions (필요한 작업에서)

## 완료 조건

- [ ] `supabase db reset` 성공
- [ ] `supabase test db`: 다른 매장 데이터 차단 테스트 통과
- [ ] `payments.idempotency_key` 고유 제약 확인

## 완료 보고

| 완료 조건 | 결과 | 확인 방법 |
|---|---|---|
| | | |
