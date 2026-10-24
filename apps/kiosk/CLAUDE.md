# CLAUDE.md — apps/kiosk (Flutter 키오스크 앱)

> 루트 `CLAUDE.md`의 규칙을 먼저 따르고, 이 파일은 Flutter 앱에만 해당하는 규칙입니다.
> 이 폴더는 아직 비어 있습니다. **task-001**에서 Flutter 프로젝트를 생성합니다.

## 생성 규칙 (task-001)

```bash
cd apps/kiosk
flutter create . --org kr.nomadaifactory --project-name tablet_kiosk --platforms android,windows
```

- 패키지 이름 `kr.nomadaifactory.tablet_kiosk` (출시 전 확정 — 바꾸려면 task-001 전에 결정)
- 플랫폼: `android`(실제 매장), `windows`(개발 확인). iOS · 웹은 만들지 않습니다.
- 최소 안드로이드 버전: 시범 매장 태블릿 기준으로 정하고 `docs/00`에 기록

## 폴더 구조

`docs/01-architecture.md` 2장을 그대로 따릅니다. 새 최상위 폴더를 임의로 만들지 않습니다.

## 코드 규칙

| 항목 | 규칙 |
|---|---|
| 상태 | Riverpod 3. 코드 생성(`riverpod_generator`) 사용 여부는 task-001에서 정하고 이 표에 기록 |
| 화면 이동 | `go_router`. 경로 이름은 `/start`, `/menu`, `/item/:id`, `/cart`, `/pay`, `/pay/split`, `/coupon`, `/done`, `/setup/:step`, `/admin` |
| 모델 | 불변 객체(`freezed` 또는 직접 작성 중 task-001에서 선택). 금액 필드는 `int` |
| 레이아웃 | 화면마다 `portrait`(스탠드 800×1280) / `landscape`(갤럭시탭 1280×800) 두 레이아웃. 공통 위젯은 `core/ui` |
| 테마 | 색 · 글자 크기는 `core/theme`의 토큰만 사용. 위젯에 색 코드 직접 쓰기 금지 |
| 문구 | 화면 문구는 한 곳(`core/ui/strings` 또는 업종 `labels`)에 모음. 다국어는 범위 밖 |
| 기기 | `kiosk_devices` 인터페이스만 사용. `dart:io Socket` 등을 화면 · 도메인에서 직접 쓰지 않음 |
| 오류 | 기기 · 네트워크 실패는 결과 타입으로 받아 화면에 "다음 행동" 문구로 표시 |
| 로그 | 카드 정보 · 전화번호 원문을 로그에 남기지 않음 |

## 디자인 대조

- 화면을 만들 때 업종 설계 저장소의 `screenshots/<화면>.png`를 열어 놓고 맞춥니다.
- 크기 · 여백 · 글자 크기는 `design/<화면>.dc.html`의 인라인 스타일 값이 기준입니다 (px = dp).
- 다른 점이 생기면 이유를 커밋 메시지에 남깁니다.

## 실행

`docs/02-dev-environment.md` 5장 참고. 기본은 윈도우 + 가짜 기기.
