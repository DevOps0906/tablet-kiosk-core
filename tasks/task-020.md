# task-020 쿠폰 서버

- **Phase**: 5. 확장
- **선행 작업**: task-005
- **확인 위치**: 로컬 Supabase

## 목표

쿠폰 캠페인 · 시리얼과 검증 · 예약 · 사용 함수를 만든다.

## 참고 문서

- `docs/06-coupon.md`

## 할 것

- [ ] 마이그레이션: coupon_campaigns, coupon_codes
- [ ] Edge Functions: coupon-issue, coupon-check, coupon-reserve, coupon-redeem, coupon-release
- [ ] 시리얼 생성 규칙(32자, 접두어, 중복 검사)
- [ ] 불가 사유 코드
- [ ] 기기당 호출 제한

## 안 할 것 (범위 밖)

- 대시보드 화면(task-022)
- 키오스크 화면(task-021)

## 완료 조건

- [ ] 함수별 테스트(기간 · 최소 금액 · 중복 사용 · 예약 충돌)
- [ ] 시리얼에 0 · O · 1 · I 없음

## 완료 보고

| 완료 조건 | 결과 | 확인 방법 |
|---|---|---|
| | | |
