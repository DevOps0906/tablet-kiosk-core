# CLAUDE.md — tablet-kiosk-core

이 파일은 Claude Code CLI가 이 저장소에서 작업할 때 항상 먼저 읽는 규칙입니다.

## 1. 이 저장소는 무엇인가

식당 · 카페 · 버거 매장용 **태블릿 키오스크의 실제 코드가 모두 들어가는 단일 저장소**입니다.

- 앱은 **하나**만 만듭니다. 사장님이 세팅 2단계(매장 정보)에서 업종(식당 / 카페 / 버거)을 고르면 같은 앱이 그 업종으로 동작합니다.
- 업종별 기획 · 디자인 · 화면 명세는 별도 설계 저장소에 있습니다. 코드는 그곳에 쓰지 않습니다.

| 저장소 | 역할 |
|---|---|
| `tablet-kiosk-core` (여기) | 실제 코드: 키오스크 앱, 사장님 대시보드, 서버(Supabase), 기기 연동 |
| `tablet-kiosk-restaurant` | 식당 설계서: PRD · DESIGN · 화면 명세 · 디자인 원본 |
| `tablet-kiosk-cafe` | 카페 설계서 |
| `tablet-kiosk-burger` | 버거 설계서 |

권장 로컬 폴더 배치 (네 저장소를 같은 상위 폴더에 클론):

```
kiosk/
├── tablet-kiosk-core/
├── tablet-kiosk-restaurant/
├── tablet-kiosk-cafe/
└── tablet-kiosk-burger/
```

업종 기능을 작업할 때는 설계 저장소를 함께 엽니다.

```bash
cd kiosk/tablet-kiosk-core
claude --add-dir ../tablet-kiosk-cafe
```

## 2. 작업 방식

1. `tasks/README.md`에서 상태가 `대기`인 가장 앞 번호 작업을 고릅니다. (`/next-task` 명령으로도 가능)
2. 해당 `tasks/task-XXX.md`의 **참고 문서**를 모두 읽고 시작합니다.
3. 작업 범위의 **안 할 것**은 절대 건드리지 않습니다. 범위 밖 문제를 발견하면 `tasks/README.md`의 "발견한 문제" 표에 적고 넘어갑니다.
4. **완료 조건**을 모두 확인한 뒤 `tasks/README.md`의 상태를 `완료`로 바꾸고 커밋합니다.
5. 설계와 다르게 구현해야 하면, 코드보다 먼저 관련 문서를 고치고 이유를 커밋 메시지에 남깁니다.

## 3. 문서 지도

| 문서 | 내용 |
|---|---|
| `PRD.md` | 무엇을 만드나 — 대상 고객, 기능 범위, MVP 구분, 성공 지표 |
| `DESIGN.md` | 어떻게 보이나 — 공통 디자인 토큰, 업종 테마, 화면 규격, 컴포넌트 |
| `docs/00-overview.md` | 린 검증 게이트, 용어집, 결정 대기 목록 |
| `docs/01-architecture.md` | 전체 구조, 앱 · 서버 · 대시보드 경계, 인터넷 끊김 정책 |
| `docs/02-dev-environment.md` | 윈도우 PC 개발 · 실행 방법, 가짜 기기 모드 |
| `docs/03-device-integration.md` | 카드 단말(VAN), 프린터, 스캐너, 키오스크 잠금 |
| `docs/04-payment.md` | 전체결제 · 더치페이 상태 흐름, 실패 · 취소 · 환불 |
| `docs/05-printing.md` | 주문서 · 영수증 양식, ESC/POS, 재시도 큐 |
| `docs/06-coupon.md` | 쿠폰 발행 · 검증 · 사용 규칙 |
| `docs/07-data-model.md` | 테이블 설계, 접근 권한(RLS) |
| `docs/08-vertical-module.md` | 업종 모듈 구조 (식당 · 카페 · 버거를 끼우는 방법) |
| `docs/09-accessibility.md` | 배리어프리 키오스크 대응 |
| `docs/10-qa-release.md` | 테스트 시나리오, 출시 체크리스트 |
| `apps/kiosk/CLAUDE.md` | Flutter 앱 전용 규칙 |
| `apps/admin/CLAUDE.md` | Next.js 대시보드 전용 규칙 |

## 4. 기술 스택 (작업 시작 시 최신 stable 확인)

| 영역 | 선택 | 비고 |
|---|---|---|
| 키오스크 앱 | Flutter (stable 3.47 이상) · Dart 3 | 타깃: Android(실제 매장), Windows(개발 확인용) |
| 상태 관리 | Riverpod 3 (`flutter_riverpod`) | |
| 화면 이동 | `go_router` | |
| 로컬 저장 | `drift` (SQLite) | 메뉴 캐시, 주문 · 출력 대기열 |
| 서버 | Supabase (Postgres · Auth · Realtime · Edge Functions) | 스키마 `kiosk` 사용 |
| 사장님 대시보드 | Next.js 16.4 (App Router) · React 19 · TypeScript 5 · Tailwind v4 · shadcn/ui | 반응형 3구간 |
| 카드 결제 | VAN사 SDK 또는 앱투앱 연동 (Kotlin 플랫폼 채널) | VAN사 미정 → `docs/00` 결정 대기 |
| 프린터 | ESC/POS 직접 인코딩 + TCP 9100 (LAN) | 블루투스 프린터는 2차 |
| 바코드 | USB · 블루투스 스캐너(키보드 입력) + 카메라 `mobile_scanner` | |
| 키오스크 잠금 | Android Lock Task (`kiosk_mode` 패키지 또는 직접 구현) | Device Owner 필요 |

패키지 버전은 작업 시점에 pub.dev / npm에서 최신 stable과 유지보수 상태를 확인한 뒤 고정합니다.

## 5. 반드시 지킬 규칙

- **기기 직접 호출 금지**: 화면 · 도메인 코드는 카드 단말 · 프린터 · 스캐너를 직접 부르지 않습니다. 반드시 `packages/kiosk_devices`의 인터페이스를 통해 부르고, 진짜 / 가짜 구현을 설정으로 바꿉니다. (`docs/02`, `docs/03`)
- **업종 분기 금지**: 공통 코드에 `if (vertical == cafe)` 같은 분기를 쓰지 않습니다. 업종 차이는 `verticals/<업종>/` 모듈의 확장 지점으로만 넣습니다. (`docs/08`)
- **금액은 정수(원)**: 금액은 `int`(원 단위)로만 다룹니다. 실수(double) 금지. 표시는 세 자리 쉼표 + `원`, 글꼴은 JetBrains Mono.
- **카드 정보 저장 금지**: 카드 번호 등 카드 정보를 앱 · 서버 · 로그 어디에도 저장하지 않습니다. 승인번호 · 마스킹 번호 · 금액만 저장합니다.
- **결제 중복 방지**: 모든 승인 요청에 멱등 키(idempotency key)를 붙입니다. (`docs/04`)
- **DB 변경 규칙**: `supabase/migrations/`의 기존 번호 파일은 절대 수정하지 않습니다. 변경은 항상 새 번호 파일로 추가합니다.
- **비밀 값**: API 키 · VAN 키 · Supabase service role 키는 저장소에 넣지 않습니다. `.env.example`에 이름만 적습니다.
- **글꼴은 앱에 포함**: 매장 인터넷이 끊겨도 화면이 같아야 하므로 글꼴은 런타임 다운로드가 아니라 앱 자산으로 넣습니다.
- **문서 언어**: 문서 · 커밋 메시지 · 화면 문구는 한국어. 코드 식별자는 영어.

## 6. 커밋 규칙

```
[task-007] 메뉴 화면: 카테고리 탭 · 품절 표시

- 무엇을 했는지
- 확인한 방법 (윈도우 / 에뮬레이터 / 실기)
```

## 7. 자주 쓰는 명령 (`.claude/commands/`)

- `/next-task` — 다음 대기 작업을 찾아 계획을 세우고 진행
- `/check` — 정적 분석 · 테스트 · 포맷 확인 후 결과 요약
- `/sync-design` — 업종 설계 저장소의 화면 명세와 현재 구현 차이 점검
