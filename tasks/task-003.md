# task-003 업종 모듈 구조 (VerticalModule)

- **Phase**: 1. 기반
- **선행 작업**: task-002
- **확인 위치**: 윈도우

## 목표

업종을 끼우는 인터페이스와 레지스트리를 만들고 3개 업종의 빈 모듈을 등록한다.

## 참고 문서

- `docs/08-vertical-module.md`

## 할 것

- [ ] `verticals/vertical_module.dart`: 08 문서 2장 확장 지점 전부를 기본 구현(아무것도 안 함)과 함께 정의
- [ ] `vertical_registry.dart`, 업종별 `*_module.dart` 빈 구현 + theme · labels 연결
- [ ] 개발 도구 막대: 업종 · 형태(세로/가로) · 기기 모드 표시 및 전환 (dev 전용)

## 안 할 것 (범위 밖)

- 업종 전용 기능 구현

## 완료 조건

- [ ] VERTICAL=cafe/restaurant/burger 실행 시 테마 · 문구가 바뀜
- [ ] core · features 폴더에서 업종 이름 분기 0건 (검색으로 확인)

## 완료 보고

| 완료 조건 | 결과 | 확인 방법 |
|---|---|---|
| | | |
