# task-002 디자인 토큰 · 업종 테마 · 공통 컴포넌트 1차

- **Phase**: 1. 기반
- **선행 작업**: task-001
- **확인 위치**: 윈도우

## 목표

DESIGN.md의 토큰과 글꼴을 코드로 옮기고 기본 컴포넌트를 만든다.

## 참고 문서

- `DESIGN.md`
- `../tablet-kiosk-cafe/DESIGN.md`
- `../tablet-kiosk-cafe/screenshots/`

## 할 것

- [ ] `core/theme`: 공통 토큰 + 업종 테마 3종 (토큰 이름 동일)
- [ ] Noto Sans KR · JetBrains Mono · Bebas Neue를 앱 자산으로 포함
- [ ] `core/money`: 금액 int → `29,000원` 표시
- [ ] `core/ui`: TopBar, BottomActionBar, NoticeBox, 주요 버튼, MenuCard(기본형), OrderSummaryCard
- [ ] 개발용 컴포넌트 미리보기 화면(`/dev/gallery`) — prod 빌드 제외

## 안 할 것 (범위 밖)

- 실제 화면 흐름
- 업종 전용 컴포넌트

## 완료 조건

- [ ] 업종을 바꾸면 갤러리 화면 색이 3가지 테마로 바뀜
- [ ] 금액 포맷 단위 테스트 (0원, 1,000원, 1,234,567원)
- [ ] 위젯에 색 코드 직접 사용 0건

## 완료 보고

| 완료 조건 | 결과 | 확인 방법 |
|---|---|---|
| | | |
