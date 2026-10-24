# `.claude/agents/` — 키오스크 개발팀

이 폴더의 에이전트는 **팀장(주 세션)** 이 작업을 나눠 맡기는 팀원입니다. 운영 규칙은 [`docs/11-multi-agent.md`](../../docs/11-multi-agent.md).
팀장 모델은 `.claude/settings.json`(`claude-opus-5-5`)에서 정합니다.

## 1. 직급 (일반 실무)

| 직급 | 파일 | 모델 | 맡는 일 |
|---|---|---|---|
| 고문 | `advisor.md` | `claude-fable-5-1` | 팀장이 2회 이상 막힌 문제의 진단 · 권고 (읽기 전용, 비상용) |
| 팀장 | (주 세션) | `claude-opus-5-5` | task 해석 · 분해 · 위임 · 결과 검토 · 커밋 |
| 대리 | `sub-agent-1.md` | `claude-sonnet-5-5` | 분야에 속하지 않는 판단 필요 실무 (문서, 여러 영역에 걸친 작은 수정, 리뷰 지적 반영) |
| 사원 | `sub-agent-2.md` | `claude-haiku-5-5` | 규칙이 정해진 단순 반복 (탐색, 설계 저장소 값 추출, 시드 정리, 형식 점검) |

## 2. 분야 에이전트 (구현)

| 파일 | 영역 | 짝 스킬 | 모델 |
|---|---|---|---|
| `flutter-expert.md` | `apps/kiosk` · `packages/kiosk_devices` | `flutter-expert` | `claude-sonnet-5-5` |
| `nextjs-expert.md` | `apps/admin` | `nextjs-expert` | `claude-sonnet-5-5` |
| `supabase-expert.md` | `supabase/` | `supabase-expert` | `claude-sonnet-5-5` |

## 3. 검증 에이전트

| 파일 | 언제 | 쓰기 | 모델 |
|---|---|---|---|
| `plan-challenger.md` | 결제 · 쿠폰 · 출력 · 기기 · DB · 업종 구조 task 의 **착수 전** 계획 공격 | 없음 | `claude-opus-5-5` |
| `review-expert.md` | 모든 구현 task 의 **변경 후** 리뷰 · 추적성 | 없음 | `claude-sonnet-5-5` |
| `contract-reviewer.md` | 앱 ↔ DB ↔ 대시보드, 공통 ↔ 업종 모듈, 앱 ↔ 기기 패키지 경계를 넘는 변경 | 없음 | `claude-sonnet-5-5` |
| `security-auditor.md` | 결제 · 쿠폰 · 기기 등록 · 잠금 · 개인정보 변경, 시범 매장 · 출시 전 | 없음 | `claude-sonnet-5-5` |
| `test-writer.md` | 리뷰가 "검증 근거 없음"을 냈을 때, 수용 시나리오 고정 | 테스트 경로만 | `claude-sonnet-5-5` |

## 4. 모델 바꾸기

- 정본은 각 파일 frontmatter 의 `model:`입니다. 바꾸면 이 표와 `docs/11` 3장도 함께 고칩니다.
- 보안 감사를 더 깊게 보려면 `security-auditor.md`만 `claude-opus-5-5`로 올립니다.
- 착수 전 계획 검토를 고문급으로 하려면 `plan-challenger.md`를 `claude-fable-5-1`로 바꿉니다 (비용 큼 — 결제 task 에만 권장).

## 5. 에이전트 추가

1. 성격이 가까운 파일을 복사해 `<이름>.md`로 저장하고 `name` · `description` · `tools` · `model`을 고칩니다.
2. 이 표와 `docs/11` 2장에 한 줄 추가합니다.
3. 대리 · 사원 설명에서 넘겨준 업무를 뺍니다.
4. `/agent-check`로 확인합니다.
