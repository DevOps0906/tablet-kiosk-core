# task-004 기기 패키지 · 가짜 기기 모드

- **Phase**: 1. 기반
- **선행 작업**: task-001
- **확인 위치**: 윈도우

## 목표

`packages/kiosk_devices`를 만들고 4개 기기 인터페이스와 가짜 구현을 완성해, 윈도우에서 기기 없이 전체 흐름을 돌릴 수 있게 한다.

## 참고 문서

- `docs/03-device-integration.md`
- `docs/02-dev-environment.md 4장`
- `packages/kiosk_devices/README.md`

## 할 것

- [ ] 플러그인 패키지 생성 (android, windows)
- [ ] 결과 타입(`ApproveResult` 등)
- [ ] CardTerminal / ReceiptPrinter / BarcodeInput / KioskLock 인터페이스
- [ ] 가짜 구현: 카드 결과 선택 대화상자, 프린터 미리보기 + `print-logs` 저장, 스캔 입력란, 잠금 배지
- [ ] HID 스캐너 입력 수집기(키보드 연속 입력 → 스캔 1건) — 실제 USB 스캐너로 윈도우에서 확인 가능
- [ ] `KioskDevices.create(mode, overrides)` 팩토리

## 안 할 것 (범위 밖)

- VAN 실제 연동
- TCP 프린터 실제 연결(task-016)

## 완료 조건

- [ ] 가짜 카드: 승인 / 거절 / 시간 초과 / 통신 오류 4가지 결과 반환 테스트
- [ ] 가짜 프린터: 미리보기 창 표시 + 파일 저장
- [ ] 패키지가 apps/kiosk를 import하지 않음

## 완료 보고

| 완료 조건 | 결과 | 확인 방법 |
|---|---|---|
| | | |
