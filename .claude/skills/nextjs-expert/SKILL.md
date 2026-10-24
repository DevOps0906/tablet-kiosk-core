---
name: nextjs-expert
description: >-
  `apps/admin` (사장님 대시보드 — Next.js App Router · TypeScript · Tailwind v4 · shadcn/ui) 작업 규약.
  페이지 · 레이아웃 · 서버/클라이언트 컴포넌트 · 서버 액션 · Route Handler · Supabase SSR 세션(@supabase/ssr) ·
  쿠폰 발행 폼 · 반응형 3구간을 만들거나 고칠 때 반드시 먼저 읽을 것. "대시보드", "쿠폰 관리", "사장님 웹" 요청도 여기서 시작한다.
  DB 스키마 · RLS · Edge Function 은 supabase-expert, 키오스크 앱은 flutter-expert 다. Pages Router 로 만들지 않는다.
---

# nextjs-expert — `apps/admin` 작업 규약

> **버전 주의**: Next.js · React · @supabase/ssr 는 메이저 변경이 잦다. 새 코드를 쓰기 전 `package.json`의 실제 버전과
> 공식 문서를 확인한다. 확인하지 못한 항목은 "미확인"으로 보고한다.

## 0. 30초 요약

1. 서버 컴포넌트가 기본이다. 상호작용 · 브라우저 API · 상태가 필요한 말단만 `"use client"`.
2. 비밀은 서버에만. `NEXT_PUBLIC_*`는 브라우저에 노출된다. service role 키는 `apps/admin`에 두지 않는다.
3. 데이터 접근의 최종 방어선은 RLS(supabase-expert)다. 클라이언트 검사는 UX 일 뿐이다.
4. 반응형 3구간과 구간별 글자 크기는 `apps/admin/CLAUDE.md` 표가 정본이다.
5. 근거(task 번호 · 명세 경로)를 보고에 인용한다.

## 1. 요청 판별

| 요청 | 시작 위치 |
|---|---|
| 새 화면 | `references/conventions.md` §라우트 → 업종 저장소 `specs/coupon.md` · `design/coupon-*.dc.html` |
| 인증 · 보호 라우트 | `references/conventions.md` §인증 세션 → supabase-expert 정책 확인 |
| 데이터 로딩 · 캐싱 이상 | `references/pitfalls.md` |
| Edge Function 호출 | `references/conventions.md` §서버 호출 → `docs/06` 함수 표 |
| 실행 · 검증 | `references/build-and-run.md` |

## 2. 핵심 규칙

- 라우트 파일 규약(`page` · `layout` · `loading` · `error` · `route`)을 따른다.
- 폼은 서버 측 검증이 정본, 클라이언트 검증은 보조. 에러 · 로딩 · 빈 상태를 항상 처리한다.
- 서버 액션 · Route Handler 는 입력을 신뢰하지 않는다 (검증 · 매장 소유 확인).
- 스타일 값은 CSS 변수 토큰으로만 (hex · 임의 값 직접 사용 금지). Tailwind v4 문법.
- 금액은 정수(원)로 받고 표시만 포맷한다 (JetBrains Mono, 세 자리 쉼표 + `원`).

## 3. 제출 전 자가 점검

- [ ] lint · typecheck · test · build 결과를 보고했는가 (미실행이면 "미검증")
- [ ] 비밀 값이 클라이언트 번들 · 로그에 없는가
- [ ] 375 · 1024 · 1440 너비에서 확인했는가
- [ ] 에러 · 로딩 · 빈 상태가 처리됐는가
- [ ] 근거를 인용했는가

## 4. 참조 파일 지도

| 파일 | 언제 |
|---|---|
| `references/conventions.md` | 새 화면 · 인증 · 서버 호출 |
| `references/pitfalls.md` | 이상 동작, 리뷰 전 점검 |
| `references/build-and-run.md` | 실행 · 검증 명령 |
