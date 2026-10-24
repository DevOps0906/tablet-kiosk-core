# task-008 메뉴 화면

- **Phase**: 2. 손님 주문 MVP (카페 · 갤럭시탭형)
- **선행 작업**: task-007
- **확인 위치**: 윈도우

> 착수 전 `docs/00-overview.md` 린 검증 게이트(G1–G3)를 확인합니다.

## 목표

분류 · 메뉴 카드 · 매장/포장 탭 · 장바구니 요약을 만든다.

## 참고 문서

- `DESIGN.md 6장`
- `../tablet-kiosk-cafe/specs/customer-flow.md (메뉴)`
- `../tablet-kiosk-cafe/screenshots/Main.png`
- `../tablet-kiosk-cafe/screenshots/sw-01-menu.png`

## 할 것

- [ ] OrderTypeTabs(선택된 쪽 강조, 바꾸면 세션 반영)
- [ ] CategoryChips, MenuCard 그리드, 품절 표시
- [ ] 업종 `menuCardDecorator` · `categoryBanner` 확장 지점 연결
- [ ] 하단 장바구니 요약 바 (개수 · 합계 · 주문 확인)
- [ ] 메뉴 탭 → 업종 `itemConfigurator` 호출 (기본: 바로 담기)

## 안 할 것 (범위 밖)

- 음료 옵션 화면(task-009)

## 완료 조건

- [ ] 상단 탭이 시작 화면 선택과 일치
- [ ] 품절 메뉴는 누를 수 없음
- [ ] 세로 · 가로 레이아웃이 스크린샷과 일치 (주요 크기)

## 완료 보고

| 완료 조건 | 결과 | 확인 방법 |
|---|---|---|
| | | |
