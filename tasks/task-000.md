# task-000 멀티에이전트 팀 이식

- **Phase**: 0. 개발 환경
- **선행 작업**: 없음
- **상태**: 완료 (2026-10-24)

## 목표

개발을 시작하기 전에 core 에 멀티에이전트 팀(에이전트 · 스킬 · 명령)을 넣어, task-001 부터 팀장이 나눠 맡기고 검증하며 진행할 수 있게 한다.

## 참고 문서

- `docs/11-multi-agent.md` (전체)
- 원본: [MultiAgent-Service-Fullstack-Tree-Framwork](https://github.com/DevOps0906/MultiAgent-Service-Fullstack-Tree-Framwork) `.claude/agents/`, `.claude/skills/`, `docs/reference/Agents-CLAUDE.md`

## 한 것

- [x] 직급 구조: `.claude/settings.json`(팀장 Opus 5.5), `advisor`(고문 Fable 5.1), `sub-agent-1`(대리 Sonnet 5.5), `sub-agent-2`(사원 Haiku 5.5)
- [x] 분야 에이전트: `flutter-expert`(새로 작성), `nextjs-expert` · `supabase-expert`(apps/admin · 키오스크 규칙으로 고침)
- [x] 검증 에이전트: `plan-challenger` · `review-expert` · `contract-reviewer` · `security-auditor` · `test-writer` (결제 · 기기 · 업종 모듈 · RLS 기준으로 재작성)
- [x] 스킬: `.claude/skills/{flutter-expert, nextjs-expert, supabase-expert}` (SKILL.md + references)
- [x] 명령: `/agent-check` 추가, `/next-task`를 팀 진행 순서로 고침
- [x] 루트 `CLAUDE.md` 8장(팀 운영 · 운영 원칙 4원칙), `NOTICE`, `docs/11`, README, `docs/02` 작업 폴더 안내

## 안 한 것 (범위 밖 — 이유는 `docs/11` 7장)

- 워커 풀(`claude-main` · `claude-reviewer`) · 승인 게이트 스크립트 · `tasks/<task>/` 폴더 · `log.md`
- `docs/file/` 산출물 등록부, 개발 위키, KNOT vault, FastAPI, 디자인 스킬

## 완료 조건

- [x] 에이전트 파일명 = frontmatter `name`, 읽기 전용 에이전트에 `Write` · `Edit` 없음
- [x] 에이전트 · 스킬이 가리키는 문서 경로가 실제로 있음
- [ ] PC 에서 `/agent-check` 실행 확인 (첫 작업 시작 전에 사용자가 확인)
