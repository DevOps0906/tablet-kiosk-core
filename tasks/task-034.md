# task-034 ③ 테이블 선불 간편결제 (PG)

- **Phase**: 6b. 테이블오더
- **선행 작업**: task-030, D9 결정
- **확인 위치**: 윈도우 + PG 테스트 환경

> 운영 방식 작업입니다. 업종 모듈이 아니라 core 공통 기능으로 만듭니다 (`docs/12`, `docs/08` 4-1장).
> 착수 전 plan-challenger 로 계획을 점검합니다 (`docs/11` 3.2).

## 목표

테이블 태블릿에서 휴대폰 간편결제(QR)로 주문할 때 결제한다.

## 참고 문서

- `../goki-kiosk-restaurant/specs/table-prepay.md`
- `docs/04-payment.md` 10장
- `docs/00-overview.md` D9

## 할 것

- [ ] D9 결정 후 PG 연동 문서 확인 · 이 task 상세 보강
- [ ] `table-prepay-create` (QR · 5분 유효) · `table-prepay-webhook` (승인 확인 → 주문 sent)
- [ ] `pg_order_id` 멱등 처리, 웹훅 중복 수신
- [ ] "나갈 때 카운터에서 결제" 미결제 경로
- [ ] PG 비밀 키는 Edge Function 환경 변수 (`.env.example`에 이름만)

## 안 할 것 (범위 밖)

- 테이블에 카드 단말 두기

## 완료 조건

- [ ] `specs/table-prepay.md` 수용 시나리오 통과 (PG 테스트 결제)

## 완료 보고

| 완료 조건 | 결과 | 확인 방법 |
|---|---|---|
| | | |
