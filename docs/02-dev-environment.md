# 02 개발 환경 — 윈도우 PC에서 개발 · 확인하기

> 앱은 안드로이드 태블릿용이지만, **대부분의 개발과 확인은 윈도우 PC에서** 합니다.
> 실제 기기가 꼭 필요한 일(카드 결제, 블루투스, 키오스크 잠금)만 갤럭시탭을 연결해서 확인합니다.

## 1. 확인 방법 4단계

| 단계 | 방법 | 명령 | 되는 것 | 안 되는 것 |
|---|---|---|---|---|
| ① 매일 개발 | **윈도우 앱으로 실행** | `flutter run -d windows` | 전체 화면 흐름, 수정 즉시 반영(Hot Reload), 가짜 기기로 결제 · 출력 미리보기, LAN 프린터 실제 출력 | 블루투스 카드 리더, 카메라 스캔, 키오스크 잠금 |
| ② 안드로이드 동작 | **Android Studio 에뮬레이터** (갤럭시탭 크기 가상 기기) | `flutter run -d emulator-5554` | 안드로이드 권한 · 화면 회전 · 뒤로가기 동작 | 실제 카드 결제, 블루투스 기기 |
| ③ 실기 연동 | **갤럭시탭을 USB로 연결** (USB 디버깅) | `flutter run -d <기기ID>` | 카드 단말, 프린터, 스캐너, 키오스크 잠금 전부 | — |
| ④ 대시보드 | **크롬 브라우저** | `pnpm dev` (apps/admin) | 사장님 대시보드 전체 | — |

> 윈도우용 안드로이드 하위 시스템(WSA)은 지원이 종료되어 사용하지 않습니다.

## 2. 설치할 것 (윈도우)

| 도구 | 용도 |
|---|---|
| Flutter SDK (stable) | 앱 빌드 · 실행 |
| Visual Studio (C++ 데스크톱 개발 워크로드) | 윈도우 앱 실행에 필요 |
| VS Code + Flutter · Dart 확장 | **메인 편집기** — `kiosk/` 폴더를 통째로 열어 core 와 업종 설계서를 함께 봄 |
| Android Studio + Android SDK | 에뮬레이터, 안드로이드 빌드 (코드 편집에는 거의 안 씀) |
| Node.js LTS + pnpm | 사장님 대시보드 |
| Docker Desktop + Supabase CLI | 로컬 Supabase (`supabase start`) |
| scrcpy (선택) | 연결한 갤럭시탭 화면을 PC에 띄워 보기 · 녹화 |
| Git, Claude Code CLI | 작업 |

설치 확인: `flutter doctor`에서 Windows · Android 항목이 모두 체크되어야 합니다.

### 작업 폴더

```
kiosk/                          ← VS Code 로 이 폴더를 엶
├── tablet-kiosk-core/          ← Claude Code 는 여기서 실행
└── tablet-kiosk-<업종>/        ← core 옆에 클론 (core 안에 넣지 않음)
```

```bash
cd tablet-kiosk-core
claude --add-dir ../tablet-kiosk-cafe     # 처음 한 번 /agent-check, 이후 /next-task
```

Claude Code 는 core 의 `.claude/`(팀 에이전트 · 스킬 · 명령)를 읽습니다. 멀티에이전트 운영은 `docs/11-multi-agent.md`.

## 3. 화면 크기 맞추기

| 형태 | 윈도우 창 크기 | 에뮬레이터 |
|---|---|---|
| 갤럭시탭형 | 1280 × 800 | 태블릿 하드웨어 프로필 직접 생성 (1920×1200, 240dpi → 1280×800dp), 가로 |
| 스탠드형 | 800 × 1280 | 같은 프로필, 세로 |

- `dev` 환경에서는 창 크기를 지정해서 띄우는 옵션을 둡니다. 예: `--dart-define=WINDOW=1280x800`
- 개발용 화면 상단에 작은 **개발 도구 막대**(형태 전환, 업종 전환, 기기 모드 표시)를 둡니다. `prod` 빌드에는 포함하지 않습니다.

## 4. 가짜 기기 모드 (fake)

`packages/kiosk_devices`의 모든 기기는 진짜(real) / 가짜(fake) 구현을 가집니다. `DEVICE_MODE=fake`이면 가짜를 씁니다.

| 기기 | 가짜 구현 동작 |
|---|---|
| 카드 단말 | 결제 요청 시 개발 도구 대화상자: **승인 성공 / 거절(한도 초과) / 시간 초과 / 통신 오류** 중 선택. 승인번호는 `FAKE-` + 시각 |
| 프린터 | 실제 출력 대신 **주문서 미리보기 창**(80mm 폭 텍스트)을 띄우고, 바이트를 `build/print-logs/`에 저장. 실패 시뮬레이션 스위치 |
| 바코드 스캐너 | 개발 도구 막대의 입력란에 시리얼을 넣으면 스캔한 것처럼 전달. 실제 USB 스캐너는 키보드처럼 동작하므로 윈도우에서도 그대로 테스트 가능 |
| 카메라 스캔 | 윈도우에서는 "카메라 없음" 안내 + 위 입력란 사용 |
| 키오스크 잠금 | 잠금 상태를 화면 배지로만 표시 (실제 잠금 없음) |

> LAN 프린터는 네트워크(TCP 9100)로 보내므로 **윈도우 PC에서도 실제 출력 테스트**가 됩니다. `DEVICE_MODE=fake`여도 프린터만 real로 바꾸는 개별 설정을 둡니다. 예: `--dart-define=PRINTER=real`

## 5. 실행 예

```bash
# 윈도우, 카페, 갤럭시탭형, 가짜 기기
flutter run -d windows \
  --dart-define=APP_ENV=dev \
  --dart-define=DEVICE_MODE=fake \
  --dart-define=VERTICAL=cafe \
  --dart-define=WINDOW=1280x800

# 갤럭시탭 실기, 진짜 기기
flutter run -d <기기ID> --dart-define=APP_ENV=staging --dart-define=DEVICE_MODE=real
```

`VERTICAL` 값은 개발 편의용입니다. 실제 앱은 사장님 세팅에서 고른 업종을 저장해 씁니다.

## 6. 로컬 Supabase

```bash
supabase start            # 로컬 Postgres · Auth · Studio 실행 (Docker 필요)
supabase db reset         # migrations + seed 다시 적용
supabase functions serve  # Edge Functions 로컬 실행
```

- 개발용 시드 데이터: 업종별 예시 메뉴는 각 설계 저장소의 `docs/02-menu-seed.md`를 기준으로 `supabase/seed.sql`에 넣습니다.
- 에뮬레이터에서 PC의 로컬 Supabase에 접속할 때는 `localhost` 대신 `10.0.2.2`를 씁니다.

## 7. 갤럭시탭 실기 연결

1. 태블릿 설정 → 휴대전화 정보 → 소프트웨어 정보 → 빌드번호 7번 눌러 개발자 옵션 켜기
2. 개발자 옵션 → USB 디버깅 켜기
3. USB로 PC 연결 → 태블릿에서 "USB 디버깅 허용"
4. `flutter devices`로 기기 확인
5. (선택) `scrcpy`로 화면을 PC에 띄워 확인 · 녹화

키오스크 잠금(Device Owner) 테스트는 **초기화한 테스트 전용 태블릿**에서만 합니다. (`docs/03` 5장)
