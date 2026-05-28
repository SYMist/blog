# 블로그 프로젝트 지침

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

## 공통 규칙
- 종료·폐지된 지원사업은 주제로 선정하지 않는다 (사업 상태 반드시 확인)
- 본문의 모든 링크는 접속 가능 여부를 확인한다
- 보험·금융 글에는 면책 문구 필수
- 모든 금액·금리·보험료에 기준 시점 명시

---

## Avatar 볼트 연동

이 프로젝트의 발행 기록은 아래 경로의 Avatar 볼트에도 저장한다.

**Avatar 볼트 경로**: `/Users/jeongsuyeon/Library/Mobile Documents/iCloud~md~obsidian/Documents/Avatar/`

**업데이트 트리거**: `/post-next` 작업 완료 후 series_todo.md에서 키워드가 체크될 때마다

**저장 방식**:
1. `raw/blog/tistory-{블로그명}/summaries/YYYY-MM-DD_{slug}.md` 파일 생성 (아래 형식)
   - deluxo: `raw/blog/tistory-deluxo/summaries/`
   - essencial: `raw/blog/tistory-essencial/summaries/`
2. Avatar `log.md`에 항목 추가: `## [YYYY-MM-DD] ingest | louisville — {블로그} "{제목}" 발행`

**raw/ 파일 형식** (Avatar 볼트의 기존 142편 요약본과 동일 형식 유지):
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

**태그 slug 매핑**:
- blog: `deluxo` | `essencial`
- silo slug (한글 → 영문 kebab):
  - deluxo: 소상공인 정책→`sb-policy`, 채무·신용회복→`debt-recovery`, 취업·노동→`labor`, 주거·부동산→`housing`, 건강보험·복지→`welfare`, 출산·육아·돌봄→`childcare`, 지역 지원금→`regional`, 연금·노후→`retirement`, 자동차→`auto`, 세금·절세→`tax`, 보험 비교→`insurance`, 청년정책→`youth`, 건강·의료→`health`
  - essencial: 자동차→`auto`, 건강·의료→`health`, 보험 비교→`insurance`, 대출·금융→`finance`
- cluster: Avatar 볼트의 `wiki/blog/what-works.md`에 정의된 18개 클러스터 중 해당 글이 속하는 것. 해당 없으면 생략.
  - essencial: auto-tco, auto-ev, auto-lease-rent, auto-tax-procedure, finance-policy, finance-tax-savings, finance-credit-loan, finance-season, health-eye, health-dental, health-weightloss, health-50s, health-insurance-claim, insurance-medical, insurance-auto, insurance-life
  - deluxo: sb-quarterly-fund, sb-regional-grant, sb-startup-operation, sb-tax, sb-loan, sb-labor-insurance, debt-rehabilitation, debt-compare, debt-creditloan

**클러스터 토픽 인덱스도 갱신 필요한 경우**:
- 새 글이 기존 클러스터에 속하면 Avatar의 `wiki/blog/topics/{cluster-slug}.md`의 "포함 포스팅" 섹션에 wiki link 추가
- 글 수 3편 이상이 된 신규 클러스터가 발견되면 토픽 인덱스 페이지 신규 생성 검토 (이건 사용자와 상의)

**추가 업데이트 트리거** (아래 상황에서는 wiki 파일도 함께 업데이트):
- 블로그 전략 변경 시 → `wiki/blog/overview.md`
- 잘 되는 패턴 또는 실패 패턴 발견 시 → `wiki/blog/what-works.md`
