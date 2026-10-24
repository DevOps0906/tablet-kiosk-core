# flutter-expert — pitfalls (리뷰 1순위 체크리스트)

| # | 함정 | 증상 · 위험 | 확인 방법 |
|---|---|---|---|
| 1 | 결제 버튼 중복 탭 | 같은 금액 두 번 승인 | 요청 중 버튼 비활성화, 멱등 키가 시도마다 규칙대로 바뀌는지 (`docs/04` 6장) |
| 2 | `CommError`를 거절로 처리하고 재승인 | 이중 결제 | 같은 키로 상태 조회 · 망취소 먼저 (`docs/03`) |
| 3 | 금액에 `double` · `/` 사용 | 1원 오차, 합계 불일치 | Grep `double`, `/ ` in `core/money`, 분할은 `~/` + 나머지는 마지막 결제자 |
| 4 | 화면 · 도메인에서 기기 직접 호출 | 가짜 기기로 테스트 불가, 진짜 기기 교체 불가 | Grep `Socket`, `MethodChannel` 이 `packages/kiosk_devices` 밖에 있는지 |
| 5 | 공통 코드의 업종 분기 | 업종 추가마다 공통 코드 수정 | Grep `vertical ==`, `'cafe'`, `'restaurant'`, `'burger'` in `core/` · `features/` |
| 6 | 카드 · 전화번호 원문 로그 | 개인정보 · 카드 정보 노출 | Grep `print(`, `log(`, `debugPrint` 주변 값 |
| 7 | 결제 중 무입력 초기화 | 결제 도중 세션 삭제 | 초기화 타이머가 결제 상태에서 멈추는지 |
| 8 | 인터넷 끊김 시 주문 유실 | 승인됐는데 서버 기록 없음 | 승인 → outbox 저장이 서버 전송보다 먼저인지 |
| 9 | 출력 실패를 무시 | 주방이 주문을 모름 | 실패 시 대기열 저장 · 사장님 재출력 경로 |
| 10 | 위젯에 색 코드 · 고정 크기 | 업종 테마 · 두 레이아웃 깨짐 | Grep `Color(0x`, 숫자 크기 상수 |
| 11 | 글꼴 런타임 다운로드 | 인터넷 끊기면 화면 달라짐 | `google_fonts` 런타임 사용 금지, `pubspec.yaml` 자산 |
| 12 | 비동기 후 `mounted` 미확인 | dispose 후 상태 변경 오류 | `await` 뒤 `context.mounted` / `ref.mounted` |
| 13 | prod 빌드에 fake 기본값 | 매장에서 가짜 결제 | `DEVICE_MODE` · `APP_ENV` 기본값, 개발 도구 막대 조건 |
| 14 | drift 스키마 버전 미증가 | 업데이트 후 앱 시작 실패 | `schemaVersion` · migration 단계 |
| 15 | Lock Task 를 개발 중 켬 | 에뮬레이터 · 실기에서 빠져나오지 못함 | dev 환경에서 잠금 기본 꺼짐 |
