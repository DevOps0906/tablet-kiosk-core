# task-033 ① 카운터 키오스크 나갈 때 결제 옵션

- **Phase**: 6b. 테이블오더
- **선행 작업**: task-030
- **확인 위치**: 윈도우 + 로컬 Supabase

> 운영 방식 작업입니다. 업종 모듈이 아니라 core 공통 기능으로 만듭니다 (`docs/12`, `docs/08` 4-1장).
> 착수 전 plan-challenger 로 계획을 점검합니다 (`docs/11` 3.2).

## 목표

카운터 키오스크에서 테이블 번호를 입력해 결제 없이 계산서에 쌓는 옵션을 붙인다.

## 참고 문서

- `../goki-kiosk-restaurant/specs/counter-kiosk.md` 4-2
- `../goki-kiosk-restaurant/screenshots/sw-02b-table.png`

## 할 것

- [ ] 설정 `counter_postpaid_enabled`일 때 주문 확인 다음 테이블 번호 입력
- [ ] `table-order-submit` 호출 (결제 단계 건너뜀), 완료 화면 문구 변경
- [ ] 등록되지 않은 번호 안내

## 안 할 것 (범위 밖)

- 테이블 태블릿 화면 변경

## 완료 조건

- [ ] `specs/counter-kiosk.md` 나갈 때 결제 시나리오 통과

## 완료 보고

| 완료 조건 | 결과 | 확인 방법 |
|---|---|---|
| | | |
