# writing_guide.md
# 블로그 글 작성 라우팅 가이드 v1.0

> 글 쓰기 전 이 파일을 먼저 열어 **어떤 가이드라인 + 어떤 템플릿**을 사용할지 확인하세요.

---

## 프로젝트 폴더 구조

```
louisville/
├── posts/
│   ├── deluxo/           ← tistory.deluxo 포스트 + series_todo.md
│   └── essencial/        ← essencial 포스트 + series_todo.md
├── templates/
│   ├── deluxo/           ← 소상공인 정책 가이드라인 + 템플릿
│   └── essencial/        ← 고CPC 비교형 가이드라인 + 템플릿 4개
├── assets/
│   ├── deluxo/           ← deluxo 이미지 (cards/, thumbnails/)
│   └── essencial/        ← essencial 이미지
└── writing_guide.md      ← 이 파일 (라우팅 가이드)
```

---

## 블로그별 역할

| 블로그 | 역할 | 주요 유입 채널 | 콘텐츠 성격 |
|--------|------|---------------|------------|
| **tistory.deluxo** | 트래픽 뼈대 | 다음 | 소상공인 정책·보조금 (신청 가이드형) |
| **essencial** | 수익 엔진 | 구글·네이버 | 고CPC 비교·의사결정형 |

---

## tistory.deluxo (소상공인 정책·보조금)

| 참고 파일 | 경로 | 용도 |
|-----------|------|------|
| 가이드라인 | `templates/deluxo/guidelines.md` | 콘텐츠 규칙, 키워드 전략, DO/DON'T |
| 템플릿 | `templates/deluxo/tistory_policy_template.html` | HTML 본문 템플릿 |
| 키워드 목록 | `posts/deluxo/series_todo.md` | 키워드 목록 + 진행 현황 |
| 포스트 저장 | `posts/deluxo/` | 완성된 HTML 파일 |
| 이미지 저장 | `assets/deluxo/cards/`, `assets/deluxo/thumbnails/` | 카드·썸네일 이미지 |

**작성 흐름:**
1. `posts/deluxo/series_todo.md`에서 다음 키워드 확인
2. `templates/deluxo/guidelines.md` 체크리스트 확인
3. `templates/deluxo/tistory_policy_template.html` 복사 → { } 채우기
4. `templates/deluxo/guidelines.md` §12 발행 전 체크리스트 확인
5. 완성 파일 → `posts/deluxo/`에 저장

---

## essencial (고CPC 비교형)

### 가이드라인 (공통 1개)

| 참고 파일 | 경로 | 용도 |
|-----------|------|------|
| 가이드라인 | `templates/essencial/essencial_guidelines.md` | 비교형 콘텐츠 공통 규칙, 구글/네이버 SEO, DO/DON'T |

### 템플릿 (Silo별 4개)

| Silo | 경로 | 사용 시점 |
|------|------|----------|
| 건강·의료 | `templates/essencial/essencial_template_health.html` | 비용 비교, 보험 적용, 시술/검사 비교 |
| 자동차 | `templates/essencial/essencial_template_auto.html` | 절세, 행정 절차, 셀프 vs 대행 비용 비교 |
| 보험 비교 | `templates/essencial/essencial_template_insurance.html` | 갱신 vs 비갱신, 보험 상품 A vs B |
| 대출·금융 | `templates/essencial/essencial_template_finance.html` | 대출 상품 비교, 금리, 자격 자가진단 |

### 키워드 목록 + 저장 위치

| 용도 | 경로 |
|------|------|
| 키워드 목록 | `posts/essencial/series_todo.md` |
| 포스트 저장 | `posts/essencial/` |
| 이미지 저장 | `assets/essencial/` |

**작성 흐름:**
1. 키워드가 어떤 Silo에 해당하는지 확인 (아래 판단 기준 참조)
2. `templates/essencial/essencial_guidelines.md` 확인 (공통 규칙 + 해당 Silo 섹션)
3. 해당 Silo 템플릿 복사 → { } 채우기
4. `templates/essencial/essencial_guidelines.md` §12 발행 전 체크리스트 확인
5. 완성 파일 → `posts/essencial/`에 저장

---

## Silo 판단 기준 (애매할 때)

| 이런 키워드라면 | 이 Silo |
|---------------|---------|
| 병원 비용, 시술 가격, 건강보험 적용, 실비 청구 | 건강·의료 |
| 자동차세, 이전등록, 폐차, 유류세, 리스/렌트 | 자동차 |
| 보험 갈아타기, 보장 비교, 보험료 차이 | 보험 비교 |
| 대출 금리, 신용점수, 전세대출, 적금/예금 비교 | 대출·금융 |
| 자동차보험 (보험료·보장 비교 중심) | 보험 비교 |
| 자동차보험 (세금·절세 중심) | 자동차 |

---

## 공통 주의사항
- 보험·금융 글에는 반드시 **면책 문구** 포함
- 모든 금액·금리·보험료에 **기준 시점** 명시
- 본문 모든 링크 **접속 가능 여부 확인**
- **종료된 사업·상품은 다루지 않음**
