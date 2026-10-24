# task-031 직원 호출 · 서빙 알림

- **Phase**: 6b. 테이블오더
- **선행 작업**: task-029, task-030
- **확인 위치**: 윈도우 + 로컬 Supabase

> 운영 방식 작업입니다. 업종 모듈이 아니라 core 공통 기능으로 만듭니다 (`docs/12`, `docs/08` 4-1장).
> 착수 전 plan-challenger 로 계획을 점검합니다 (`docs/11` 3.2).

## 목표

테이블 태블릿 호출 → 카운터 현황판 · 서빙 알림 → 처리까지 연결한다.

## 참고 문서

- `../goki-kiosk-restaurant/specs/table-order.md` 7장
- `../goki-kiosk-restaurant/docs/03-operation-modes.md` 6장
- `docs/08-vertical-module.md` `labels.staffCallItems`

## 할 것

- [ ] 호출 화면 (업종 `labels.staffCallItems` + 직접 쓰기 40자)
- [ ] 같은 항목 처리 전 중복 방지
- [ ] 현황판 노랑 · 호출 목록 · `처리` → 손님 화면 `처리됨`
- [ ] `계산 요청` → 테이블 상태 계산 요청(파랑)
- [ ] 소리 · 깜빡임 알림 (설정으로 끔), 서빙 알림(직원 폰)은 2차

## 안 할 것 (범위 밖)

- 호출 출력 (설정 옵션, 2차)

## 완료 조건

- [ ] `specs/table-order.md` 호출 시나리오 · `specs/counter.md` 호출 처리 시나리오 통과

## 완료 보고

| 완료 조건 | 결과 | 확인 방법 |
|---|---|---|
| | | |
