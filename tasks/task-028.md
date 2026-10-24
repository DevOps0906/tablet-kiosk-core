# task-028 운영 방식 · 테이블 · 열린 계산서 스키마

- **Phase**: 6b. 테이블오더
- **선행 작업**: task-005, task-006
- **확인 위치**: 로컬 Supabase

> 운영 방식 작업입니다. 업종 모듈이 아니라 core 공통 기능으로 만듭니다 (`docs/12`, `docs/08` 4-1장).
> 착수 전 plan-challenger 로 계획을 점검합니다 (`docs/11` 3.2).

## 목표

테이블오더의 데이터와 서버 함수 기반(계산서 · 차수 · 취소 · 이동 · 합석 · 닫기 · 호출)을 만든다.

## 참고 문서

- `docs/12-operation-modes.md` 1 · 3 · 5장
- `docs/07-data-model.md` 운영 방식 절 · 4장
- `../goki-kiosk-restaurant/docs/03-operation-modes.md` 2 · 4 · 5 · 6장
- `../goki-kiosk-restaurant/docs/02-menu-seed.md` 테이블 · 계산서 예시

## 할 것

- [ ] `stores.operation_mode`, `devices.role` · `table_id` 새 마이그레이션
- [ ] `store_tables` · `table_sessions` · `order_item_cancellations` · `staff_calls` 테이블, `orders` · `payments` · `split_plans` · `order_discounts` 컬럼 추가
- [ ] RLS: 테이블 기기는 자기 테이블만, 카운터는 매장 전체 (07 문서 4장)
- [ ] Edge Function: `table-order-submit` · `session-bill` · `session-item-cancel` · `session-move` · `session-merge` · `session-start-billing` · `session-close` · `staff-call` · `staff-call-done`
- [ ] 시드: 홀 1~12 · 룸 2, 12번 열린 계산서 예시 (1~3차 104,000원)
- [ ] pgTAP: 열린 계산서 1개 제약, 다른 테이블 · 다른 매장 접근 차단, 중복 주문(같은 멱등 키) 1건

## 안 할 것 (범위 밖)

- 테이블 · 카운터 화면 (task-029, 030)
- ③ 간편결제 (task-034)

## 완료 조건

- [ ] `supabase db reset` 후 시드 계산서 `session-bill` = 104,000원
- [ ] 같은 멱등 키 `table-order-submit` 두 번 → 주문 1건
- [ ] 테이블 기기 JWT 로 다른 테이블 계산서 조회 거부
- [ ] `session-merge` 후 차수 시간순 재정렬 · 원래 계산서 closed

## 완료 보고

| 완료 조건 | 결과 | 확인 방법 |
|---|---|---|
| | | |
