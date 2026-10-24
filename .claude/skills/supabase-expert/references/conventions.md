# supabase-expert — conventions

> 프로젝트의 실제 설정 · 기존 마이그레이션이 우선한다. 불일치는 보고한다.

## 마이그레이션

- 위치 `supabase/migrations/`. 파일명은 CLI 가 만드는 접두를 따른다.
- 한 마이그레이션 = 하나의 의도 (테이블 생성 / 정책 추가 / 인덱스 추가). 섞지 않는다.
- 이미 있는 파일은 수정하지 않는다. 고칠 때는 새 마이그레이션으로.
- 스키마는 `kiosk`. 테이블 · 컬럼 이름은 `docs/07` 표와 같게 쓴다.

## RLS

- 테이블 생성과 같은 마이그레이션에서 RLS 를 켠다.
- 기본 정책: JWT 의 `store_id` 클레임 = 행의 `store_id`. 정책 조건 컬럼(`store_id`)에는 인덱스.
- update 정책은 using 과 with check 를 모두 쓴다 (다른 매장으로 옮기기 방지).
- 사용자가 고칠 수 있는 메타데이터를 권한 근거로 쓰지 않는다.
- service role 은 RLS 를 우회한다 — Edge Function 에서만, 사용 이유를 주석으로.

## 동시성

- 주문번호 발급(`daily_order_counters`), 쿠폰 reserve/redeem 은 함수 안에서 행 잠금 또는 조건부 갱신(`update ... where status = 'issued' returning`)으로 한 번만 성공하게 한다.
- `payments.idempotency_key`는 고유 제약. 같은 키로 다시 기록하면 첫 기록을 돌려준다 (`docs/04` 6장).

## 개인정보 · 결제

- 전화번호(카페 스탬프)는 암호화 저장 + 조회용 해시를 분리한다 (카페 저장소 `docs/01`).
- 카드 번호 원문 · 유효기간 컬럼을 만들지 않는다.

## 타입 · 시드

- DB 변경 후 대시보드 타입을 재생성한다. 생성 파일은 직접 수정하지 않는다.
- 시드는 업종 저장소 `docs/02-menu-seed.md` 값을 쓰고, 실제 개인정보 · 키를 넣지 않는다.
