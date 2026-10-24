---
name: flutter-expert
description: >-
  `apps/kiosk`(Flutter 키오스크 앱) · `packages/kiosk_devices`(기기 연동) 작업 규약. 손님 화면 · 사장님 세팅 화면,
  Riverpod 상태, go_router, drift(로컬 캐시 · outbox · 출력 대기열), 결제 상태 흐름, 업종 모듈(VerticalModule) 구현,
  가짜/진짜 기기 구현, Kotlin 플랫폼 채널을 만들거나 고칠 때 반드시 먼저 읽을 것.
  "화면", "위젯", "메뉴", "장바구니", "결제", "더치페이", "출력", "프린터", "카드 단말", "잠금", "업종 모듈" 요청도 여기서 시작한다.
  DB · RLS · Edge Function 은 supabase-expert, 사장님 대시보드는 nextjs-expert 다.
---

# flutter-expert — `apps/kiosk` · `packages/kiosk_devices` 작업 규약

> **버전 주의**: Flutter · Riverpod · go_router · drift 는 메이저 변경이 잦다. 새 코드를 쓰기 전 `pubspec.yaml`의 실제 버전과
> 공식 문서를 확인한다. 확인하지 못한 API 는 "미확인"으로 보고한다.

## 0. 30초 요약

1. 기기는 `kiosk_devices` 인터페이스로만 부른다. 개발은 가짜 기기(`DEVICE_MODE=fake`) + 윈도우가 기본이다.
2. 공통 코드는 업종을 모른다. 업종 차이는 `verticals/<업종>/`의 확장 지점으로만 (`docs/08`).
3. 금액은 `int`(원). 할인 · 분할 계산은 `core/money` 한 곳에서.
4. 결제는 상태 머신(`docs/04`) + 멱등 키. 버튼 중복 탭과 `CommError`(승인 여부 모름)를 항상 생각한다.
5. 인터넷 · 프린터는 끊긴다. outbox · 출력 대기열 · 임시 번호(`docs/01` 5장, `docs/05`)가 정상 경로다.

## 1. 요청 판별

| 요청 | 먼저 볼 곳 |
|---|---|
| 새 화면 | 업종 설계 저장소 `specs/` 해당 장 → `screenshots/` · `design/*.dc.html` → `DESIGN.md` 6장 공통 컴포넌트 |
| 업종 기능 | `docs/08` 확장 지점 표 → 업종 저장소 `docs/01-vertical-rules.md` |
| 결제 · 더치페이 | `docs/04` 상태 표 · 분할 규칙 · 멱등 키 |
| 출력 | `docs/05` 양식 · 대기열 |
| 쿠폰 입력 | `docs/06` 상태 · 오류 문구 |
| 기기 · 잠금 | `docs/03`, `packages/kiosk_devices/README.md` |
| 실행 · 화면 크기 | `docs/02` |

## 2. 핵심 규칙

- 폴더 구조는 `docs/01-architecture.md` 2장을 따른다. 새 최상위 폴더를 만들지 않는다.
- 화면마다 `landscape`(갤럭시탭 1280×800) · `portrait`(스탠드 800×1280) 두 레이아웃.
- 색 · 글자 크기 · 여백은 `core/theme` 토큰만. 문구는 `core/ui/strings` 또는 업종 `labels`.
- 기기 · 네트워크 실패는 결과 타입으로 받아 화면에 "다음 행동" 문구로 보여 준다 (예외를 삼키지 않는다).
- 비동기 작업 후 화면이 사라졌을 수 있다 — `ref.mounted` / `context.mounted`를 확인한다.
- 개발 도구 막대 · 가짜 기기는 `APP_ENV=prod`에서 빠져야 한다.

## 3. 제출 전 자가 점검

- [ ] `dart format` · `flutter analyze` · `flutter test` 결과를 보고했는가 (미실행이면 "미검증")
- [ ] 두 레이아웃(1280×800 · 800×1280)에서 확인했는가
- [ ] `references/pitfalls.md` 항목을 다시 훑었는가
- [ ] 근거(task 번호 · 명세 경로)를 인용했는가

## 4. 참조 파일

| 파일 | 언제 |
|---|---|
| `references/pitfalls.md` | 구현 전 · 리뷰 전 체크리스트 |
