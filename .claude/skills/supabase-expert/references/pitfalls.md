# supabase-expert — pitfalls (리뷰 1순위 체크리스트)

| # | 함정 | 증상 · 위험 | 확인 방법 |
|---|---|---|---|
| 1 | 테이블에 RLS 미설정 | 공개 키로 전 매장 데이터 접근 | `enable row level security` 유무 |
| 2 | 정책이 `true`로 열려 있음 | 사실상 무방비 | 정책 using/with check |
| 3 | `store_id` 클레임 출처가 사용자 수정 가능 값 | 다른 매장 데이터 접근 | 정책의 JWT 클레임 출처 |
| 4 | update 정책에 with check 누락 | 행을 다른 매장으로 옮김 | update 정책 |
| 5 | 정책 컬럼 인덱스 없음 | 전 쿼리 지연 | `store_id` 인덱스 |
| 6 | 기존 마이그레이션 수정 | 환경 간 스키마 불일치 | git 이력의 기존 파일 변경 |
| 7 | 금액 컬럼을 `numeric`/`float`로 | 앱 int 와 불일치 · 오차 | 컬럼 타입 |
| 8 | 쿠폰 redeem · 주문번호 발급 경쟁 | 같은 쿠폰 두 번 사용 · 번호 중복 | 잠금 · 조건부 갱신 |
| 9 | `idempotency_key` 고유 제약 누락 | 결제 기록 중복 | 제약 유무 |
| 10 | service role 키 노출 | 전권 노출 | Grep `service_role`, 환경 변수 |
| 11 | 생성 타입을 직접 수정 | 재생성 시 소실 | 타입 파일 diff |
| 12 | 시드에 실데이터 · 키 · 실제 전화번호 | 정보 유출 | seed 파일 |
