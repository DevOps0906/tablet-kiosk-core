# task-021 쿠폰 키오스크 화면

- **Phase**: 5. 확장
- **선행 작업**: task-011, task-020
- **확인 위치**: 윈도우(시리얼 · HID 스캐너), 갤럭시탭(카메라)

## 목표

결제 방법 화면에서 시리얼 입력 · 바코드 스캔으로 쿠폰을 적용한다.

## 참고 문서

- `docs/06-coupon.md 4장`
- `../tablet-kiosk-cafe/specs/coupon.md`
- `../tablet-kiosk-cafe/screenshots/hw-coupon-serial.png`
- `../tablet-kiosk-cafe/screenshots/sw-coupon-scan.png`

## 할 것

- [ ] CouponEntryBar 활성화
- [ ] 시리얼 탭: SerialKeypad(32키), 12자 입력 시 자동 확인
- [ ] 스캔 탭: HID 스캐너 + 카메라(`mobile_scanner`, 안드로이드만)
- [ ] DiscountResultCard, 불가 사유 문구
- [ ] 결제 시작 reserve · 완료 redeem · 취소 release
- [ ] `docs/00` D4 결정 반영

## 완료 조건

- [ ] 쿠폰 적용 → 결제 → 사용 처리 → 재사용 거부
- [ ] 인터넷 끊김 시 안내

## 완료 보고

| 완료 조건 | 결과 | 확인 방법 |
|---|---|---|
| | | |
