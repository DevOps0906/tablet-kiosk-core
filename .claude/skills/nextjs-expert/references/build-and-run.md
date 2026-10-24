# nextjs-expert — build & run

패키지 매니저는 **pnpm** 이다 (`apps/admin/CLAUDE.md`). 명령은 `apps/admin/package.json`의 `scripts`가 정본이다.

| 목적 | 명령 | 비고 |
|---|---|---|
| 의존성 설치 | `pnpm install` | 잠금 파일이 정본 |
| 개발 서버 | `pnpm dev` | 환경 변수는 `.env.local` (커밋 금지) |
| 타입체크 | `pnpm typecheck` 또는 `pnpm exec tsc --noEmit` | 스크립트 없으면 보고 |
| 린트 | `pnpm lint` | |
| 테스트 | `pnpm test` | 없으면 "테스트 없음"으로 보고 |
| 빌드 | `pnpm build` | 산출물(`.next/`) 커밋 금지 |

- 환경 변수 목록은 루트 `.env.example`이 정본이다. 값은 저장소에 두지 않는다.
- 로컬 Supabase 연결은 `docs/02-dev-environment.md` 6장.
- 실행하지 못한 명령은 "미검증"으로 쓰고 통과로 간주하지 않는다.
