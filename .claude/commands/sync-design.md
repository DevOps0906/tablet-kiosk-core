---
description: 업종 설계 저장소의 화면 명세와 현재 구현 차이 점검
---
인자: 업종 이름 (restaurant | cafe | burger). 예: `/sync-design cafe`

1. `../tablet-kiosk-$ARGUMENTS/specs/`의 화면 명세와 `DESIGN.md`를 읽는다 (`--add-dir`로 열려 있어야 함).
2. `apps/kiosk/lib/features/`, `apps/kiosk/lib/verticals/$ARGUMENTS/`의 구현과 비교한다.
3. 화면별로 "명세 항목 / 구현 여부 / 차이" 표를 만든다.
4. 코드는 고치지 않는다. 필요한 작업은 `tasks/README.md`의 "발견한 문제" 표에 제안으로 적을지 사용자에게 묻는다.
