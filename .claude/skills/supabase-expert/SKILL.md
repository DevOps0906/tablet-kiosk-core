---
name: supabase-expert
description: >-
  `supabase/` (Postgres 스키마 `kiosk` · RLS · Auth · Realtime · Edge Functions · 마이그레이션) 작업 규약.
  매장 · 기기 · 메뉴 · 주문 · 결제 건 · 쿠폰 · 스탬프 테이블, 매장별 격리 정책, 쿠폰 함수, 기기 등록, 시드, 타입 생성,
  로컬 Supabase 를 만들거나 고칠 때 반드시 먼저 읽을 것. "스키마", "마이그레이션", "RLS", "정책", "Edge Function", "시드" 요청도 여기서 시작한다.
  키오스크 앱 소비 코드는 flutter-expert, 대시보드 화면은 nextjs-expert 다. 기존 마이그레이션 파일은 수정하지 않는다.
---

# supabase-expert — `supabase/` 작업 규약

> **버전 주의**: Supabase CLI · 플랫폼 기능은 빠르게 바뀐다. 명령 · 설정 키는 `supabase --help`와 공식 문서로 확인한다.
> 확인하지 못한 항목은 "미확인"으로 보고한다.

## 0. 30초 요약

1. 모든 테이블은 RLS 를 켠다. 격리 단위는 매장(`store_id`). 정책 의도를 주석으로 남긴다.
2. 스키마 변경은 새 번호 마이그레이션 파일로만. 기존 파일은 수정하지 않는다.
3. 금액은 정수(원). 카드 정보는 승인번호 · 마스킹 번호 · 금액만.
4. service role 키는 Edge Function 전용. 원격 DB 적용 · 삭제는 실행하지 않고 제시만 한다.
5. 테이블 · 정책 정본은 `docs/07-data-model.md`, 쿠폰 함수는 `docs/06`, 결제 기록은 `docs/04`.

## 1. 요청 판별

| 요청 | 시작 위치 |
|---|---|
| 새 테이블 · 컬럼 | `docs/07` 표 → `references/conventions.md` §마이그레이션 |
| 권한 · 정책 | `docs/07` 접근 권한 표 → `references/conventions.md` §RLS |
| 쿠폰 · 주문번호 등 동시성 | `references/conventions.md` §동시성 |
| 업종 데이터 | 업종 저장소 `docs/01-vertical-rules.md` 키 목록 → `vertical_attrs` · `vertical_data` |
| 로컬 실행 · 검증 | `references/build-and-run.md` |

## 2. 핵심 규칙

- 정책은 동작별(select/insert/update/delete)로 나누고, 호출 주체(기기 JWT · 사장님 세션 · service role)를 명시한다.
- 파괴적 변경은 영향 범위(앱 모델 · drift · 대시보드 타입)와 되돌리기 방법을 적는다. 매장 기기는 업데이트가 늦을 수 있으므로 하위 호환을 우선한다.
- 정책 · 스키마 변경 후 flutter-expert · nextjs-expert 에게 넘길 항목을 남긴다.

## 3. 제출 전 자가 점검

- [ ] 새 테이블에 RLS 가 켜져 있고 정책 의도가 설명됐는가
- [ ] 같은 매장 / 다른 매장 / 비로그인 성공 · 거부 시나리오를 적었는가
- [ ] `supabase db reset`으로 처음부터 재현되는가 (미실행이면 "미검증")
- [ ] 금액 컬럼이 정수인가, 카드 원문 컬럼이 없는가
- [ ] 키 · 시크릿이 파일 · 로그에 없는가

## 4. 참조 파일 지도

| 파일 | 언제 |
|---|---|
| `references/conventions.md` | 마이그레이션 · RLS · 동시성 |
| `references/pitfalls.md` | 이상 동작, 리뷰 전 점검 |
| `references/build-and-run.md` | 로컬 실행 · 검증 명령 |
