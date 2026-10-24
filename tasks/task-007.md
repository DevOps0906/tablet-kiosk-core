# task-007 시작 화면 · 주문 세션

- **Phase**: 2. 손님 주문 MVP (카페 · 갤럭시탭형)
- **선행 작업**: task-003, task-006
- **확인 위치**: 윈도우

> 착수 전 `docs/00-overview.md` 린 검증 게이트(G1–G3)를 확인합니다.

## 목표

매장 / 포장을 고르고 주문 세션을 시작한다.

## 참고 문서

- `docs/01-architecture.md 4장`
- `../tablet-kiosk-cafe/specs/customer-flow.md (시작 화면)`
- `../tablet-kiosk-cafe/screenshots/sw-00-start.png`
- `../tablet-kiosk-cafe/screenshots/00-start.png`

## 할 것

- [ ] 시작 화면 가로 · 세로 레이아웃
- [ ] 주문 세션 Provider (order_type, 장바구니, 쿠폰, 시작 시각)
- [ ] 무입력 초기화 타이머(설정값, 결제 중 비활성) + "시간을 더 드릴까요?"
- [ ] 직원 호출 버튼(공통 하단) — 호출 이벤트만 발생(알림 연결은 task-014)

## 안 할 것 (범위 밖)

- 메뉴 화면

## 완료 조건

- [ ] 매장 / 포장 선택이 세션에 저장되고 다음 화면으로 이동
- [ ] 무입력 시 안내 후 시작 화면 복귀

## 완료 보고

| 완료 조건 | 결과 | 확인 방법 |
|---|---|---|
| | | |
