# task-019 카페 모듈 2차: 스탬프

- **Phase**: 5. 확장
- **선행 작업**: task-018
- **확인 위치**: 윈도우 + 로컬 Supabase

## 목표

전화번호 스탬프 적립 · 결제자별 적립 · 10개 무료 쿠폰을 만든다.

## 참고 문서

- `../tablet-kiosk-cafe/docs/01-vertical-rules.md (스탬프)`
- `../tablet-kiosk-cafe/specs/customer-flow.md (스탬프)`
- `../tablet-kiosk-cafe/screenshots/05-stamp.png`

## 할 것

- [ ] 마이그레이션: stamp_members, stamp_ledger (전화번호 암호화 · 해시)
- [ ] 개인정보 수집 동의 화면
- [ ] 전화번호 입력 키패드, 적립 · 조회 Edge Function
- [ ] 결제자별 적립 배분 규칙
- [ ] 10개 달성 → 자동 쿠폰 발급 (task-020 이후 연결, 그 전엔 기록만)
- [ ] 완료 화면 · 영수증 스탬프 현황

## 안 할 것 (범위 밖)

- 문자 발송(2차)

## 완료 조건

- [ ] 카페 설계 저장소 스탬프 시나리오 통과
- [ ] 전화번호 원문이 로그 · 평문 컬럼에 없음

## 완료 보고

| 완료 조건 | 결과 | 확인 방법 |
|---|---|---|
| | | |
