# 08 업종 모듈 구조 — 식당 · 카페 · 버거를 끼우는 방법

> 원칙: **앱은 하나, 업종은 모듈.** 공통 코드는 업종을 모르고, 업종 모듈은 정해진 확장 지점에만 붙습니다.

## 1. 위치

```
apps/kiosk/lib/verticals/
├── vertical_module.dart        인터페이스 (확장 지점 정의)
├── vertical_registry.dart      업종 코드 → 모듈 연결
├── restaurant/                 설계: tablet-kiosk-restaurant
├── cafe/                       설계: tablet-kiosk-cafe
└── burger/                     설계: tablet-kiosk-burger
```

각 업종 폴더 구성 (필요한 것만 만듭니다):

```
verticals/cafe/
├── cafe_module.dart            VerticalModule 구현
├── theme.dart                  업종 테마 토큰 값 (DESIGN.md 3장)
├── preset.dart                 기본 분류 · 예시 메뉴 · 문구
├── item_config/                메뉴 선택 시 옵션 화면 (음료 옵션)
├── payment_hooks/              결제 전후 동작 (전화번호 · 스탬프)
├── print_blocks/               주문서 · 영수증 추가 블록
├── setup/                      사장님 세팅 추가 항목 (스탬프 규칙)
└── test/
```

## 2. 확장 지점

| 확장 지점 | 하는 일 | 식당 | 카페 | 버거 |
|---|---|---|---|---|
| `theme` | 업종 테마 토큰 | 제이드 그린 | 브라운 | 레드 |
| `preset` | 세팅 3단계 기본 분류 · 예시 메뉴 | 고기 · 식사 · 찌개 · 주류 · 음료 | 커피 · 음료 · 디저트 | 버거 · 세트 · 사이드 · 음료 |
| `labels` | 업종 문구 | 호출번호 | 주문번호 | 주문번호 (TV 호출) |
| `menuCardDecorator` | 메뉴 카드 배지 · 안내 | 주류 `19` 배지, 인분 표기 | 인기 · 신메뉴 | 세트 할인 표시 |
| `categoryBanner` | 분류 상단 안내 | 주류 · 음료: 19세 이상 안내 | — | — |
| `itemConfigurator` | 메뉴를 눌렀을 때 담기 전 과정 | 인분 수 선택 | 음료 옵션 화면 | 단품 / 세트 / 라지 → 사이드 · 음료 → 재료 변경 |
| `cartRules` | 장바구니 검사 | 최소 인분, 주류 안내 확인 | — | 세트 필수 단계 완료 여부 |
| `splitOptions` | 더치페이 추가 규칙 | 고기 인분 단위로 나누기 | — | — |
| `paymentHooks.beforePart` | 결제 건 시작 전 | — | 결제자 전화번호 입력(선택, 동의) | — |
| `paymentHooks.afterPart` | 결제 건 승인 후 | — | 결제자별 스탬프 적립 | — |
| `paymentHooks.afterPaid` | 주문 확정 후 | — | 10개 달성 시 무료 쿠폰 발급 | 주문번호 TV 등록 |
| `printBlocks.kitchen` | 주방 주문서 변형 | 고기 / 식사 / 찌개 분류별 분할 | 옵션 강조 | 재료 변경 강조 |
| `printBlocks.receipt` | 영수증 추가 줄 | — | 스탬프 현황 | 주문번호 크게 |
| `doneScreenExtras` | 완료 화면 추가 | 호출번호 안내 | 스탬프 현황 | TV 안내 |
| `setupExtras` | 세팅 5단계 추가 항목 | 주방 프린터 분류 매핑 | 스탬프 규칙 (10개 = 1잔) | 주문번호 TV 연결 |
| `adminExtras` | 대시보드 추가 메뉴 | — | 스탬프 회원 | 주문번호 TV 화면 URL |

모든 확장 지점은 **기본 구현(아무것도 안 함)**이 있어서, 업종 모듈은 필요한 것만 덮어씁니다.

## 3. 공통 화면과 업종 화면

| 단계 | 공통 화면 (core / features) | 업종 모듈이 끼어드는 곳 |
|---|---|---|
| 시작 | 매장 / 포장 선택 | 문구 · 테마 |
| 메뉴 | 분류 · 메뉴 카드 · 장바구니 요약 | 카드 배지, 분류 배너 |
| 메뉴 선택 | — | `itemConfigurator` 전체 (카페 옵션, 버거 세트 · 재료) |
| 주문 확인 | 항목 · 수량 · 합계 | `cartRules` |
| 결제 방법 | 전체결제 / 더치페이 / 쿠폰 | — |
| 더치페이 | N등분 · 메뉴별 · 금액 | `splitOptions`, `paymentHooks` |
| 완료 | 번호 · 처음으로 | `doneScreenExtras` |
| 사장님 세팅 | 1–5단계 | `setupExtras` |

## 4. 규칙

1. `core` · `features`에서 업종 이름으로 분기하지 않습니다 (`if (vertical == ...)` 금지).
2. 두 업종 이상이 같은 기능을 필요로 하면, 업종 모듈에서 꺼내 **core의 일반 기능 + 설정값**으로 옮깁니다.
3. 업종 모듈은 다른 업종 모듈을 import하지 않습니다.
4. 업종 전용 데이터는 `vertical_attrs` · `vertical_data`(jsonb)에 넣고, 키 목록은 업종 설계 저장소 `docs/01-vertical-rules.md`에 정의합니다.
5. 업종 모듈마다 테스트 폴더를 두고, 설계 저장소 `specs/`의 시나리오를 테스트로 옮깁니다.

## 5. 업종 선택과 전환

- 사장님 세팅 **2단계(매장 정보)**에서 업종을 고르면 `stores.vertical`에 저장되고, 앱은 시작할 때 레지스트리에서 모듈을 꺼내 주입합니다.
- 업종 변경은 사장님 PIN + 확인 후 앱 재시작으로만 가능 (메뉴 구조가 달라지므로).
- 개발 중에는 `--dart-define=VERTICAL=cafe` 또는 개발 도구 막대로 즉시 전환.

## 6. 새 업종 추가 절차 (예: 분식, 베이커리)

1. 설계 저장소 `tablet-kiosk-<업종>` 생성 (PRD · DESIGN · specs · design)
2. `verticals/<업종>/` 폴더 생성, `VerticalModule` 구현 (필요한 확장 지점만)
3. `vertical_registry.dart`에 등록, `stores.vertical` 허용 값 추가 (새 마이그레이션)
4. 업종 테마 토큰을 `DESIGN.md` 3장 표에 추가
