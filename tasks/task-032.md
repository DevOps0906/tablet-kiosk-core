# task-032 운영 방식 세팅 · 테이블 배치 · 태블릿 역할 지정

- **Phase**: 6b. 테이블오더
- **선행 작업**: task-014, task-028
- **확인 위치**: 윈도우 + 에뮬레이터 2대

> 운영 방식 작업입니다. 업종 모듈이 아니라 core 공통 기능으로 만듭니다 (`docs/12`, `docs/08` 4-1장).
> 착수 전 plan-challenger 로 계획을 점검합니다 (`docs/11` 3.2).

## 목표

사장님이 운영 방식을 고르고, 테이블을 등록하고, 태블릿을 테이블 · 카운터 · 입구 키오스크로 짝짓는다.

## 참고 문서

- `../goki-kiosk-restaurant/specs/owner-setup.md` 2-2 · 4-2 · 4-3
- `../goki-kiosk-restaurant/screenshots/set-02b-mode.png` · `set-04b-tables.png` · `set-04c-pair.png`
- `docs/12-operation-modes.md` 2장

## 할 것

- [ ] 세팅 2-2 운영 방식 카드 3장 + 옵션 (업종 `preset.defaultOperationMode` 기본값)
- [ ] 세팅 4-2 구역 · 테이블 수 · 번호 · 이름, 연결 QR · 6자리 코드 (`device-pair`)
- [ ] 4-3 새 기기 역할 지정 (카운터 · 테이블 번호 · 입구 키오스크), 번호 중복 확인
- [ ] 운영 방식 변경 시 매장 기기 재시작 안내

## 안 할 것 (범위 밖)

- ③ PG 가맹 신청 화면

## 완료 조건

- [ ] `specs/owner-setup.md` 테이블오더 수용 시나리오 통과

## 완료 보고

| 완료 조건 | 결과 | 확인 방법 |
|---|---|---|
| | | |
