# kiosk_devices

키오스크 기기(카드 단말 · 프린터 · 바코드 · 키오스크 잠금) 연동 패키지. **task-004**에서 Flutter 플러그인 패키지로 생성합니다.

```bash
cd packages
flutter create --template=plugin --platforms=android,windows --org kr.nomadaifactory kiosk_devices
```

## 구조 (계획)

```
lib/
├── kiosk_devices.dart          공개 API (인터페이스 + 팩토리)
├── src/
│   ├── card_terminal/          CardTerminal 인터페이스, FakeCardTerminal, VanCardTerminal(플랫폼 채널)
│   ├── printer/                ReceiptPrinter 인터페이스, FakePrinter, TcpPrinter(9100)
│   ├── barcode/                BarcodeInput 인터페이스, HidScannerInput, CameraInput, FakeBarcodeInput
│   ├── kiosk_lock/             KioskLock 인터페이스, AndroidLockTask, FakeKioskLock
│   └── result.dart             결과 타입 (Approved / Declined / Timeout / CommError …)
android/                        Kotlin: VAN SDK · 앱투앱 호출, Lock Task, Device Admin 리시버
windows/                        (비워 둠 — 윈도우는 가짜 구현 + TCP 프린터만)
```

## 규칙

- 앱 코드(`apps/kiosk`)를 import하지 않습니다.
- 진짜 / 가짜 선택은 팩토리 한 곳: `KioskDevices.create(mode: DeviceMode.fake | real, overrides: {...})`
- VAN SDK 파일(AAR 등)은 라이선스상 저장소에 넣을 수 있는지 확인 후 결정. 넣을 수 없으면 설치 가이드만 둡니다.

자세한 동작은 `docs/03-device-integration.md`.
