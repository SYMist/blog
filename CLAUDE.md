# 블로그 프로젝트 지침

> ⚠️ **운영방침 우선**: 작업 전 `operating_policy.md`를 먼저 읽는다. (2026-05-30 **수확 모드 — 신규 글 발행 중단, 제휴 회수 중심** → 2026-06-16 볼트 판정으로 **passive-only 종결**. 아래 작성 워크플로보다 이 방침이 상위.)

## 프로젝트 구조
- 2개 블로그 운영: **tistory.deluxo** (소상공인 정책) + **essencial** (고CPC 비교형)
- 모든 파일은 블로그별로 `deluxo/`, `essencial/` 하위 폴더에 분리

## 블로그 글 작성 시 필수 절차
1. `writing_guide.md`를 먼저 읽고 대상 블로그·Silo·가이드라인·템플릿 경로 확인
2. 해당 블로그의 `series_todo.md`에서 작성할 키워드 확인
3. 해당 가이드라인 읽기 (deluxo: `templates/deluxo/guidelines.md` / essencial: `templates/essencial/essencial_guidelines.md`)
4. 해당 템플릿 복사 → { } 채우기
5. 가이드라인의 발행 전 체크리스트 확인
6. 완성 파일은 `posts/{블로그명}/`에 저장

## 파일 네이밍 규칙

### essencial HTML 파일명
기존 게시글과 동일한 형식 사용: `E-{번호}_{한글키워드_언더스코어}_2026.html`
- 예: `E-62_부모_운전자보험_자녀가입_vs_본인가입_vs_미가입_비교_2026.html`
- publish.md도 동일한 이름 사용: `E-62_..._2026.publish.md`
- **영문 슬러그 형식(예: `parents_driver_insurance_comparison_2026.html`) 사용 금지**

### 이미지 저장 경로

- **deluxo 카드 (5장)**: `assets/deluxo/cards/<슬러그>/` — 슬러그 이름 폴더를 만들어 저장
  - 예: `assets/deluxo/cards/fire_liability_insurance_guide_2026/summary_card_1080_fire_liability_insurance_guide_2026.svg`
- **deluxo 썸네일 (2장)**: `assets/deluxo/thumbnails/<슬러그>/` — 슬러그 이름 폴더를 만들어 저장
  - 예: `assets/deluxo/thumbnails/fire_liability_insurance_guide_2026/thumb_1080_fire_liability_insurance_guide_2026.svg`
- **essencial (5장)**: `assets/essencial/` — 플랫 구조 유지

## publish.md 작성 규칙

### 태그 형식
태그는 **쉼표로 구분하여 한 줄**로 작성한다.
```
## 태그
1인법인, 개인사업자 법인전환, 법인세율 2026, 종합소득세 세율, 세금 절약
```
- 한 줄에 하나씩 나열하는 방식 **사용 금지**

## 공통 규칙
- 종료·폐지된 지원사업은 주제로 선정하지 않는다 (사업 상태 반드시 확인)
- 본문의 모든 링크는 접속 가능 여부를 확인한다
- 보험·금융 글에는 면책 문구 필수
- 모든 금액·금리·보험료에 기준 시점 명시

---

## Avatar 볼트 연동

이 프로젝트의 발행·작업 기록은 Avatar 볼트에도 저장한다.

- Avatar 볼트 경로: `/Users/suyeon/Library/Mobile Documents/iCloud~md~obsidian/Documents/Avatar/`

### ⚠️ 로그 항목 타입 선택 (ingest vs handoff) — 먼저 판단

Avatar log.md에 기록할 때 **타입을 반드시 구분**한다. 잘못 고르면 다음 세션 맥락 주입이 깨진다.

| 타입 | 언제 | 효과 |
|---|---|---|
| **ingest** | raw/ 에 원본·요약 파일을 **추가**할 때 (예: `/post-next` 발행본 요약). raw/ 또는 wiki/ 갱신을 동반하는 "자료 유입"만. | wiki 지식화 대상 |
| **handoff** | 세션을 **마무리**하며 작업 상태·다음 액션을 넘길 때. raw/wiki 추가 없이 "무엇을 했고 다음에 뭘 할지"만 보고하는 경우(예: 쿠팡 제휴 부착, 글 일괄 수정, 수확 모드 작업). | SessionStart 훅이 **자동 주입**해 다음 세션이 이어받음 |

판단 규칙:
- raw/ 에 새 요약 파일을 만들었나? → **ingest**
- 파일 추가 없이 "작업 완료 + 남은 일" 보고인가? (사용자가 "마무리했어 / 정리해줘"라고 한 경우 포함) → **handoff**
- 둘 다 해당하면(발행 + 세션 종료) 둘 다 작성한다.

handoff 형식 (Avatar log.md 맨 위 `---` 아래에 추가):
```
## [YYYY-MM-DD] handoff | louisville — {제목}

{한 줄 맥락 — 어느 작업 세션에서 뭘 넘기는지}

**한 일**
- (이번 세션 핵심 작업 2~4개)

**참고**: 관련 wiki/raw 링크
```

> 🔴 **「이어서 할 일」 필드는 폐지됐다 (볼트 2026-08-23 개정).** 할 일의 정본은 볼트 `TASKS.md`다 — handoff에 목록을 다시 적으면 그 순간 사본이 되고, `log.md`는 append-only라 낡아도 못 고친다. 넘길 다음 액션이 있으면 **볼트 `TASKS.md`에 등록**하고, handoff엔 *「이번 세션이 `TASKS.md`를 어떻게 바꿨나」 한 줄*(추가·삭제 건수 + 특기사항)만 쓴다.

### 발행 기록 push — `/post-next` 완료 시 (이 레포 → Avatar, **ingest**)

업데이트 트리거: `/post-next` 작업 완료 후 series_todo.md에서 키워드가 체크될 때마다.

1. `raw/blog/tistory-{블로그명}/summaries/YYYY-MM-DD_{slug}.md` 파일 생성 (아래 형식)
   - deluxo: `raw/blog/tistory-deluxo/summaries/`
   - essencial: `raw/blog/tistory-essencial/summaries/`
2. Avatar `log.md`에 항목 추가: `## [YYYY-MM-DD] ingest | louisville — {블로그} "{제목}" 발행`

raw/ 파일 형식 (Avatar 볼트의 기존 요약본과 동일 형식 유지):
```
---
date: YYYY-MM-DD
blog: deluxo | essencial
silo: Silo명 (한글)
keyword: 타겟 키워드
title: 포스팅 제목
tags: [blog/{blog-slug}, silo/{silo-slug}, cluster/{cluster-slug}]
---

## 핵심 내용
(2~3줄 — 이 글이 다루는 핵심 주제와 독자에게 제공하는 가치)

## 타겟 독자
(어떤 상황의 독자가 이 글을 찾을지)

## 주요 포인트
- 포인트 1 (구체적 수치 포함 — 금액·요율·기간 등)
- 포인트 2
- 포인트 3
- (필요 시 4~5번까지)

## FAQ 키워드
(JSON-LD FAQ 질문들 또는 본문 H2 제목에서 검색 의도 키워드 3~5개)
```

태그 slug 매핑:
- blog: `deluxo` | `essencial`
- silo slug (한글 → 영문 kebab):
  - deluxo: 소상공인 정책→`sb-policy`, 채무·신용회복→`debt-recovery`, 취업·노동→`labor`, 주거·부동산→`housing`, 건강보험·복지→`welfare`, 출산·육아·돌봄→`childcare`, 지역 지원금→`regional`, 연금·노후→`retirement`, 자동차→`auto`, 세금·절세→`tax`, 보험 비교→`insurance`, 청년정책→`youth`, 건강·의료→`health`
  - essencial: 자동차→`auto`, 건강·의료→`health`, 보험 비교→`insurance`, 대출·금융→`finance`
- cluster: Avatar `wiki/blog/what-works.md`에 정의된 클러스터 중 해당 글이 속하는 것. 해당 없으면 생략.
  - essencial: auto-tco, auto-ev, auto-lease-rent, auto-tax-procedure, finance-policy, finance-tax-savings, finance-credit-loan, finance-season, health-eye, health-dental, health-weightloss, health-50s, health-insurance-claim, insurance-medical, insurance-auto, insurance-life
  - deluxo: sb-quarterly-fund, sb-regional-grant, sb-startup-operation, sb-tax, sb-loan, sb-labor-insurance, debt-rehabilitation, debt-compare, debt-creditloan

클러스터 토픽 인덱스 갱신:
- 새 글이 기존 클러스터에 속하면 Avatar `wiki/blog/topics/{cluster-slug}.md`의 "포함 포스팅" 섹션에 wiki link 추가.
- 같은 클러스터 글이 **2편 이상**이 된 신규 클러스터면 토픽 인덱스 신규 생성 검토 (사용자와 상의). ※ 2026-05-21 기준 기존 "3편"에서 완화됨.

추가 업데이트 트리거 (아래 상황에선 wiki 파일도 함께 업데이트):
- 블로그 전략 변경 시 → `wiki/blog/overview.md`
- 잘 되는/실패 패턴 발견 시 → `wiki/blog/what-works.md`

### 역할 경계 & 참조 방향 (Avatar ↔ 이 레포)

이 레포 = **실행 세션**(글 작성·발행·투두). 분석·지식은 **Avatar 볼트**가 보유한다.

- **경계**: 데이터 분석·지식화 = Avatar / 글 발행·투두 실행 = 이 레포.
- **작업 시작 전 참조**: Avatar `TASKS.md`(할 일 정본) + `log.md` 최신 **handoff**(맥락 복원용) + 관련 wiki. ⚠️ **둘이 어긋나면 `TASKS.md`가 이긴다** — `log.md`는 append-only라 낡아도 못 고친다.
  - 전략·방향: `wiki/blog/overview.md`, `wiki/blog/seo-status.md`
  - 성과·패턴: `wiki/blog/performance.md`, `wiki/blog/what-works.md`
- **데이터 분석은 Avatar에서**: GSC·애널리틱스 원본은 Avatar `raw/blog/`에 두고 Avatar 세션이 분석→wiki로 종합. 이 레포는 결론(wiki)을 참조해 실행만 한다.
- **이 레포의 실행 투두는 이 레포에서 관리**(`series_todo.md`) — 볼트 밖(볼트 순수성, 2026-05-30). ⚠️ **2026-08-23 범위 명확화**: 「Avatar엔 투두를 두지 않는다」가 아니다. 볼트 밖에 두는 건 **작업세션 실행 투두**이고, **Avatar 자기 몫 목록은 볼트 `TASKS.md`**에 있다. 이 레포 투두를 `TASKS.md`에 베끼는 것도 금지(정본이 갈라진다).
- (현재 방침: 수확 모드 — 신규 발행 중단. `operating_policy.md` 상위. **2026-06-16 볼트 판정으로 blog 도메인은 passive-only 종결** — 지휘 대상이 아니고 유입 급변 신호만 모니터한다. 재론엔 새 실측 필요.)
