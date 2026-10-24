# task-001 Flutter 앱 생성 · 폴더 구조

- **Phase**: 1. 기반
- **선행 작업**: 없음
- **확인 위치**: 윈도우, 에뮬레이터

## 목표

키오스크 앱 뼈대를 만들고 윈도우 · 안드로이드에서 빈 화면이 뜨게 한다.

## 참고 문서

- `CLAUDE.md`
- `apps/kiosk/CLAUDE.md`
- `docs/01-architecture.md 2장`
- `docs/02-dev-environment.md`

## 할 것

- [ ] `apps/kiosk`에 `flutter create` (android, windows) — 기존 `CLAUDE.md`가 덮어쓰이면 git으로 되돌림
- [ ] `docs/01` 2장의 `lib/` 폴더 구조 생성 (빈 파일 · README 수준)
- [ ] Riverpod · go_router · drift 의존성 추가 (최신 stable 확인 후 버전 고정)
- [ ] `--dart-define` 값(APP_ENV, DEVICE_MODE, VERTICAL, WINDOW) 읽는 설정 클래스
- [ ] 윈도우 창 크기 지정(WINDOW=1280x800 / 800x1280)
- [ ] lint 규칙(`analysis_options.yaml`) 설정
- [ ] `apps/kiosk/CLAUDE.md` 코드 규칙 표의 "task-001에서 정함" 항목 결정 · 기록

## 안 할 것 (범위 밖)

- 화면 디자인 구현
- 기기 연동

## 완료 조건

- [ ] `flutter run -d windows`로 1280×800 · 800×1280 창에 빈 시작 화면 표시
- [ ] 안드로이드 에뮬레이터에서 실행
- [ ] `flutter analyze` 경고 0

## 완료 보고

| 완료 조건 | 결과 | 확인 방법 |
|---|---|---|
| | | |
