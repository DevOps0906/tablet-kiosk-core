# CLAUDE.md — apps/admin (사장님 대시보드)

> 루트 `CLAUDE.md`의 규칙을 먼저 따르고, 이 파일은 대시보드에만 해당합니다.
> 이 폴더는 아직 비어 있습니다. **task-022**에서 Next.js 프로젝트를 생성합니다. (MVP 단계의 메뉴 · 품절 관리는 키오스크 앱 사장님 화면에서 처리)

## 생성 규칙 (task-022)

- Next.js 16.4 이상 (App Router, TypeScript, Tailwind v4, Turbopack) — `create-next-app` 최신으로 생성
- shadcn/ui 초기화, 패키지 매니저 pnpm
- Supabase: `@supabase/ssr`로 서버 · 클라이언트 세션 처리

## 화면 (1차)

| 경로 | 화면 | 디자인 |
|---|---|---|
| `/login` | 사장님 로그인 | (디자인 없음 — 단순 폼) |
| `/` | 홈: 오늘 주문 수 · 매출 | (2차) |
| `/coupons` | 쿠폰 관리 대시보드 | 업종 저장소 `coupon-dashboard` |
| `/coupons/new` | 쿠폰 발행 | `coupon-create` |
| `/menu` | 메뉴 · 품절 관리 | 2차 |
| `/devices` | 기기 · 프린터 상태 | 2차 |

## 반응형 규칙 (필수)

| 구간 | 너비 | 제목 | 소제목 | 본문 | 작은 글씨 | KPI | 여백 |
|---|---|---|---|---|---|---|---|
| 데스크탑 | ≥1200px | 30px | 20px | 16px | 14px | 32px | 32px |
| 태블릿 | 768–1199px | 26px | 18px | 15px | 13px | 28px | 24px |
| 모바일 | ≤767px | 22px | 17px | 14px | 12px | 24px | 16px |

- CSS 변수(`--fs-h1` 등)로 정의하고 Tailwind 테마에 연결합니다. 디자인 원본 `coupon-dashboard.dc.html`의 `<style>` 블록과 같은 값입니다.
- 왼쪽 메뉴: 데스크탑은 세로 사이드바, 태블릿 · 모바일은 위쪽으로 접힘.
- 쿠폰 목록 표는 좁아지면 가로 스크롤.
- 업종 테마 색은 로그인한 매장의 `vertical`에 따라 CSS 변수로 바꿉니다 (DESIGN.md 3장).

## 규칙

- 서버 작업(쿠폰 발행 등)은 Edge Function 또는 Route Handler(서버)에서만. 클라이언트에 service role 키 금지.
- 금액 표시는 JetBrains Mono, 세 자리 쉼표 + `원`.
- 숫자 데이터 화면에는 "예시 데이터" 표시를 실제 데이터 연결 전까지 유지.
