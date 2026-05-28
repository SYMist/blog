---
description: series_todo.md의 다음 키워드로 리서치 + 본문 HTML + 카드 이미지 + 퍼블리시 헬퍼 일괄 생성
argument-hint: <deluxo|essencial> [키워드]
---

# /post-next — 블로그 글 1편 자동 작성

블로그 글 1편을 처음부터 끝까지(리서치 → HTML 본문 → 카드 이미지 → 퍼블리시 헬퍼) 작성하는 일괄 커맨드.

**입력 인자**: `$ARGUMENTS`
- 첫 번째 토큰: 블로그 이름 (`deluxo` 또는 `essencial`) — 필수
- 두 번째 이후 토큰: 키워드 직접 지정(선택). 미지정 시 `series_todo.md`의 첫 번째 미완료(☐) 항목을 자동 선택

---

## 절차

### 0. 인자 파싱 + 사전 점검
1. `$ARGUMENTS`에서 블로그 이름과 (있다면) 키워드 추출
2. 블로그 이름이 `deluxo`/`essencial`이 아니면 즉시 중단하고 사용자에게 알림
3. `writing_guide.md` 읽기 — 라우팅 규칙 재확인

### 1. 키워드 선택
- 키워드를 인자로 받았으면: 그 키워드 사용
- 받지 않았으면: `posts/<blog>/series_todo.md`를 위에서 아래로 스캔하여 **첫 번째 미완료(☐) 항목**을 선택
  - 모든 항목이 ✅이면 다음 메시지 출력 후 **즉시 중단**:
    > `series_todo.md`의 모든 항목이 완료 상태입니다. 새 키워드 추가가 필요합니다. 추가 후 다시 호출해주세요.
- 선택한 키워드 / 행 위치 / Silo 정보(essencial인 경우)를 사용자에게 1줄로 보고

### 2. 슬러그 결정
- 파일명용 영문 슬러그를 결정 (예: `workers_comp_mistakes_2026`, `cataract_lens_cost_2026`)
- 슬러그는 소문자 + 언더스코어 + 연도 포함, 길이 60자 이내
- 동일 슬러그 파일이 이미 있으면 사용자에게 확인 후 진행

### 3. Silo·템플릿 라우팅 (essencial 한정)
essencial인 경우 키워드를 다음 4개 Silo 중 하나에 매칭:

| Silo | 템플릿 | 매칭 신호 |
|------|--------|-----------|
| 건강·의료 | `templates/essencial/essencial_template_health.html` | 병원 비용/시술/건강보험/실비/검진 |
| 자동차 | `templates/essencial/essencial_template_auto.html` | 자동차세/이전등록/유류세/리스/렌트/폐차/하이브리드/전기차 |
| 보험 비교 | `templates/essencial/essencial_template_insurance.html` | 실비/암보험/운전자보험/간병/치아/생명보험 비교·갈아타기 |
| 대출·금융 | `templates/essencial/essencial_template_finance.html` | 대출 금리/신용점수/예적금/세제혜택/연금·IRP/종합소득세/재산세 |

애매하면 `writing_guide.md`의 "Silo 판단 기준" 표를 따른다. 자동차보험은 비용·보장 비교 중심이면 보험, 세금·절세 중심이면 자동차로 분류.

deluxo는 단일 템플릿(`templates/deluxo/tistory_policy_template.html`).

### 4. 가이드라인 + 템플릿 읽기
- deluxo: `templates/deluxo/guidelines.md` + 위 템플릿
- essencial: `templates/essencial/essencial_guidelines.md` + 라우팅된 Silo 템플릿
- 가이드라인은 **전체** 읽기 (체크리스트 절차/§12 발행 전 체크리스트 포함)

### 5. 리서치 (필수)
이 단계는 절대 건너뛰지 않는다.

- `research/<blog>/research_<slug>.md` 파일이 이미 있으면 그 내용을 그대로 활용 (재리서치 불필요)
- 없으면 WebSearch/WebFetch로 리서치 진행:
  - 공식 사이트(정부 부처·공공기관·은행·보험사 약관 등)를 1차 출처로 사용
  - 본문에 들어갈 모든 외부 링크는 WebFetch로 접속 가능 여부를 확인하고, 깨진 링크는 대체하거나 제거
  - **사업/제도 상태 확인**: 종료·폐지된 사업이면 즉시 중단하고 사용자에게 보고
  - 모든 금액/금리/보험료/비용은 **기준 시점 명시** (예: "2026년 4월 기준")
  - 보험·금융 주제는 약관/금감원 자료 등 공신력 있는 출처 1개 이상 포함
- 결과를 `research/<blog>/research_<slug>.md`에 저장 (구조: 개요, 핵심 사실, 비교/계산 자료, 공식 링크 목록, 출처)
- **작성 글 1편당 외부 링크는 최소 3개 이상 검증된 것만 사용**

### 6. 본문 HTML 작성
1. 해당 템플릿을 복사 → `posts/<blog>/<slug>.html`
2. 가이드라인의 작성 요령(deluxo §5 / essencial §4)에 따라 모든 `{ }` 플레이스홀더를 실제 내용으로 채움
3. **이미지는 실제 `<img>` 태그로 본문에 삽입** (주석 처리 금지). 형식:
   ```html
   <img src="<filename>.png" alt="<alt 텍스트>" style="width:100%;margin:16px 0;" />
   ```
   - deluxo: 7장 체제 (§9). `summary_card`, `quick_guide`, `compare_card`, `rejection_card`, `checklist_card`, `thumb_1080`, `thumb_1200x630`
   - essencial: 5장 체제 (§7). `compare_summary`, `compare_matrix`, `scenario`, `thumb_1080`, `thumb_1200x630`
4. 인아티클 광고 코드는 템플릿에 박혀 있는 것 **그대로 보존** (deluxo 슬롯 `7020031076`, essencial 슬롯 `2039167138`)
5. Schema.org JSON-LD의 BlogPosting + FAQPage 채우기 — 발행일/수정일은 오늘 날짜
6. 업데이트 로그에 오늘 날짜 + "최초 발행" 기록
7. **관련 글 영역의 내부 링크는 placeholder 유지** (티스토리 발행 후 사용자가 실제 URL로 교체) — 단, placeholder 텍스트는 같은 Silo의 실제 글 제목으로 기입해서 어떤 글로 연결할지 명확히

### 7. 카드 이미지 (SVG) 생성
- deluxo 7장 / essencial 5장. 가이드라인의 네이밍 규칙·치수·컬러를 준수
- SVG만 생성 (PNG 변환 불필요)
- 저장 경로:
  - deluxo: `assets/deluxo/cards/<filename>.svg`, `assets/deluxo/thumbnails/<filename>.svg`
  - essencial: `assets/essencial/<filename>.svg`
- 카드 이미지(deluxo #1~#6 / essencial #1~#3)에는 칩/태그 장식 요소를 넣지 않는다. 칩은 썸네일에만 사용.
- 폰트는 시스템 sans-serif 사용 (`font-family="-apple-system, sans-serif"` 등). 한글 텍스트는 SVG `<text>`로 직접 삽입.

### 8. 발행 전 체크리스트 자동 검증
가이드라인 §12를 자동으로 통과시킨다. 항목별로 통과/미통과를 표시하고, **하나라도 실패하면 그 항목을 수정한 뒤 재검사**.

**deluxo 검증 항목**
- 제목 맨 앞에 메인키워드
- 5줄 요약에 가능/신청처/핵심조건/기간·지급/주의 포함
- 한눈에 표 1개 이상
- 공식 링크 버튼 2~3개
- 인아티클 광고 슬롯 `7020031076` 본문 존재
- 모든 외부 링크 접속 가능 (WebFetch로 확인)
- 종료 사업 아님
- 서류 "기본+상황별" 분리
- FAQ 8개 이상
- 업데이트 로그 날짜 기입
- 7개 카드 이미지 `<img>` 태그 모두 본문에 존재
- **§4 정부 안내에 없는 실측 정보 sub-block 중 최소 2~3개 채워짐** (소요 시간/자주 혼동되는 포인트/대표 케이스 시뮬레이션/공식 가이드에 없는 운영 팁 중) — 가이드라인 §13 DO-5 참조. 1인칭 fabricated 톤 금지(3인칭/객관 톤)
- 차별화 sub-block은 ul/li가 아닌 p 태그 또는 table로 서술
- **도입(.lead)에 "공식 안내에 없는 ~ 정보가 이 글에 있다"는 차별화 신호 1문장 포함**
- publish.md에 **티스토리 발행 옵션 메타 description (150자, 검색결과 클릭 유도형)** 항목 채워짐
- 관련 글 placeholder는 같은 토픽의 실제 발행 가능한 글 제목으로 기입 (`href="#"` 또는 빈 텍스트 금지)

**essencial 검증 항목**
- 상단 3줄에 상황별 결론
- 비교표 1개 이상
- 시나리오 추천("~라면 A, ~라면 B") 존재
- 인아티클 광고 슬롯 `2039167138` 시나리오 직후
- 금액/금리/보험료에 기준 시점 명시
- 보험·금융 글이면 면책 문구 ("개인 상황에 따라 다를 수 있으며, 가입 전 약관 확인 필요" 류) 존재
- 모든 외부 링크 접속 가능
- meta description 작성 (Schema.org description)
- Schema.org BlogPosting + FAQPage
- 본문 길이 2,000자 이상
- 5개 이미지 `<img>` 태그 모두 본문에 존재
- H3 60% 이상 질문형
- **자주 놓치는 포인트와 실수 사례 섹션 채워짐** (사례 2~3개, p태그 서술, 3인칭 일반화 톤). 가이드라인 §11 DO-6 #5 참조. 1인칭 fabricated 톤 금지
- **차별화 5가지 중 최소 2~3개 명시 적용** (비교 매트릭스/시나리오/숨겨진 비용/갈아타기 ROI/자주 놓치는 사례). 가이드라인 §11 DO-6 참조
- 갈아타기·리파이낸싱 비교 글이면 ROI 계산 박스 주석 해제하여 채움 (해당 시)
- publish.md에 **티스토리 발행 옵션 메타 description (150자, 검색결과 클릭 유도형)** 항목 채워짐
- 관련 글 placeholder는 같은 Silo의 실제 발행 가능한 글 제목으로 기입 (`href="#"` 또는 빈 텍스트 금지)

### 9. 퍼블리시 헬퍼 작성
`posts/<blog>/<slug>.publish.md` 파일을 다음 구조로 생성:

```markdown
# 퍼블리시 헬퍼: <제목>

## 메타
- 슬러그: <slug>
- 카테고리: <추천 카테고리>
- 발행 예정일: <YYYY-MM-DD>
- 본문 파일: posts/<blog>/<slug>.html

## 제목 (그대로 복붙)
<완성 제목>

## 메타 디스크립션 (티스토리 설정 > 기본설정)
<150자 이내>

## 태그 (한 줄에 하나씩 — `#태그입력` 영역에 차례로 입력)
<태그1>
<태그2>
<태그3>
...

## 이미지 매핑 (본문 `<img>` 위치별 — 커서 두고 '사진 삽입' 클릭)
| # | 본문 위치 | 파일 경로 | alt 텍스트 |
|---|----------|----------|----------|
| 1 | 5줄 요약 아래 | assets/<blog>/cards/summary_card_1080_<slug>.svg | ... |
| 2 | ... | ... | ... |

## 썸네일 (티스토리 설정에서 지정)
- 정사각: assets/<blog>/(cards 또는 thumbnails)/thumb_1080_<slug>.svg
- 가로: assets/<blog>/(cards 또는 thumbnails)/thumb_1200x630_<slug>.svg

## 관련 글 (placeholder 위치별 — 티스토리에서 실제 URL로 교체)
| 본문 위치 | 추천 글 제목 (같은 Silo) | 비고 |
|----------|------------------------|------|
| 1분 체크리스트 섹션 하단 #1 | <같은 Silo의 발행된 글 제목> | 티스토리에서 검색해 URL 가져오기 |
| 1분 체크리스트 섹션 하단 #2 | ... | ... |

## 발행 후 할 일
- [ ] 본문 복붙 → 이미지 7장(또는 5장) 직접 삽입 → 관련 글 URL 교체
- [ ] 태그 입력 (위 목록 참고)
- [ ] 썸네일 지정
- [ ] 메타 디스크립션 입력
- [ ] 발행 후 URL을 series_todo.md의 "메모" 칸에 기록 (선택)
```

관련 글 후보는 같은 블로그·같은 Silo의 **이미 ✅ 완료**된 항목 중 주제 인접도가 높은 2~3개를 series_todo.md에서 골라 추천한다.

### 10. series_todo.md 업데이트
- 자동 선택한 키워드의 상태를 ☐ → ✅로 바꾸고, "메모" 칸에 작성일과 상태(예: "2026-04-30 HTML+SVG 완료, 발행 대기") 기록
- 인자로 직접 받은 키워드라 series_todo에 없으면 건너뜀

### 11. Avatar 볼트 연동 (CLAUDE.md "Avatar 볼트 연동" 절차)

**Avatar 볼트 경로**: `/Users/jeongsuyeon/Library/Mobile Documents/iCloud~md~obsidian/Documents/Avatar/`

해당 절차는 series_todo.md에서 키워드가 ☐ → ✅로 체크된 직후 실행한다. 인자로 직접 받은 키워드라 series_todo 업데이트를 건너뛴 경우에도 Avatar 연동은 수행한다.

#### 11-1. raw 파일 생성
경로: `<Avatar 볼트>/raw/blog/<블로그명>/<YYYY-MM-DD>_<slug>.md`

형식 (frontmatter + 4개 섹션):

```markdown
---
date: YYYY-MM-DD
blog: deluxo | essencial
silo: Silo명 (한글, 예: "자동차" / "보험 비교" / "건강·의료" / "대출·금융")
keyword: 타겟 롱테일 키워드
title: 포스팅 제목 (publish.md의 제목 그대로)
tags: [blog/<blog-slug>, silo/<silo-slug>, cluster/<cluster-slug>]
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
(JSON-LD FAQ 질문들 또는 본문 H2/H3에서 검색 의도 키워드 3~5개)
```

**태그 slug 매핑** (CLAUDE.md 참조):
- blog: `deluxo` 또는 `essencial`
- silo slug:
  - essencial: 자동차→`auto` / 건강·의료→`health` / 보험 비교→`insurance` / 대출·금융→`finance`
  - deluxo: 소상공인 정책→`sb-policy` / 채무·신용회복→`debt-recovery` / 취업·노동→`labor` / 주거·부동산→`housing` / 건강보험·복지→`welfare` / 출산·육아·돌봄→`childcare` / 지역 지원금→`regional` / 연금·노후→`retirement` / 자동차→`auto` / 세금·절세→`tax` / 보험 비교→`insurance` / 청년정책→`youth` / 건강·의료→`health`
- cluster slug (Avatar `wiki/blog/what-works.md`의 18개 클러스터 중 선택, 해당 없으면 생략):
  - essencial: `auto-tco`, `auto-ev`, `auto-lease-rent`, `auto-tax-procedure`, `finance-policy`, `finance-tax-savings`, `finance-credit-loan`, `finance-season`, `health-eye`, `health-dental`, `health-weightloss`, `health-50s`, `health-insurance-claim`, `insurance-medical`, `insurance-auto`, `insurance-life`
  - deluxo: `sb-quarterly-fund`, `sb-regional-grant`, `sb-startup-operation`, `sb-tax`, `sb-loan`, `sb-labor-insurance`, `debt-rehabilitation`, `debt-compare`, `debt-creditloan`

#### 11-2. Avatar log.md 항목 추가
경로: `<Avatar 볼트>/log.md`

파일 맨 위 또는 가장 최근 날짜 섹션 아래에 다음 한 줄을 추가:

```
## [YYYY-MM-DD] ingest | louisville — <블로그명> "<제목>" 발행
```

#### 11-3. 클러스터 토픽 인덱스 갱신 (해당 시)
- 글이 기존 클러스터에 속하면 `<Avatar 볼트>/wiki/blog/topics/<cluster-slug>.md`의 "포함 포스팅" 섹션에 wiki link `[[YYYY-MM-DD_<slug>]]` 형태로 추가
- 토픽 인덱스 파일이 없으면 그대로 건너뜀 (신규 토픽 인덱스 생성은 사용자 상의 사항)

#### 11-4. 추가 wiki 갱신 (선택)
다음 상황이 명확하면 함께 갱신:
- 블로그 전략 변경 신호 발견 → `<Avatar 볼트>/wiki/blog/overview.md`
- 잘 되는/실패 패턴 발견 → `<Avatar 볼트>/wiki/blog/what-works.md`

판단 모호하면 건너뛰고 최종 보고에서 사용자에게 검토 요청만 남긴다.

### 12. 최종 보고
다음을 한 번에 출력:
- 작성한 파일 목록 (HTML, 리서치, SVG 7개/5개, publish.md, Avatar raw 파일)
- 발행 전 체크리스트 통과 결과
- Avatar 연동 결과 (raw 파일 경로 / log.md 추가 줄 / 토픽 인덱스 갱신 여부)
- 사용자가 다음에 할 액션 1줄 요약 ("티스토리 글쓰기 진입 → posts/.../<slug>.publish.md 보면서 작업")

---

## 공통 주의

- 한국어로 작성. 본문 HTML 안의 텍스트도 한국어
- 오늘 날짜는 동적으로 (시스템 컨텍스트의 currentDate 또는 `date +%Y-%m-%d`)
- 종료된 사업·상품은 절대 다루지 않는다 (리서치 단계에서 발견 시 즉시 중단)
- 보험·금융 글은 면책 문구 필수
- 본문 모든 링크는 WebFetch로 접속 검증
- 작업 중간에 사용자 결정이 필요한 분기점이 생기면(슬러그 충돌, 종료 사업 의심, Silo 모호 등) 멈추고 1줄로 질문
