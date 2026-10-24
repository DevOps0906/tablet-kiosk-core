# task-006 데이터 계층 · 로컬 캐시 · outbox

- **Phase**: 1. 기반
- **선행 작업**: task-003, task-005
- **확인 위치**: 윈도우 + 로컬 Supabase

## 목표

앱이 Supabase와 로컬 DB를 통해 메뉴를 읽고, 주문 · 결제를 안전하게 기록하는 계층을 만든다.

## 참고 문서

- `docs/01-architecture.md 4·5장`
- `docs/07-data-model.md 5장`
- `docs/04-payment.md 7장`

## 할 것

- [ ] drift 로컬 DB: cached_menu, outbox_payments, outbox_orders, print_jobs, device_settings
- [ ] 메뉴 동기화(앱 시작 · 주기 · 수동)
- [ ] 저장소 인터페이스(MenuRepository, OrderRepository, PaymentRepository) + Supabase 구현 + 메모리 구현(테스트용)
- [ ] outbox 재전송 작업자(앱 시작 시 최우선, 점점 간격 늘림)
- [ ] 개발용 기기 계정: 시드 데이터 기기로 로그인하는 dev 경로

## 안 할 것 (범위 밖)

- 기기 등록 화면(task-014)

## 완료 조건

- [ ] 인터넷 끊고 앱 재시작 → 캐시 메뉴 표시
- [ ] outbox에 넣은 결제 건이 연결 복구 후 서버에 1번만 기록됨 (멱등 키)

## 완료 보고

| 완료 조건 | 결과 | 확인 방법 |
|---|---|---|
| | | |
