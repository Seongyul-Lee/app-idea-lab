## 3단계: PRD 문서 작성

대상 아이디어: $ARGUMENTS

## 목적
채택된 아이디어에 대해 구체적인 제품 요구사항 문서를 작성한다.

## 입력
- `ideas/NNN-아이디어명.md` — 평가 완료 아이디어 문서
- `research/competitors/NNN-경쟁분석.md` — 경쟁사 분석
- `research/market-data/NNN-시장분석.md` — 시장 분석

## 사용 도구
| 도구 | 역할 |
|------|------|
| Skill: `sc:design` | Technical Architecture 섹션(시스템 구조, DB 스키마, API 설계) 작성 |

## PRD 작성 구조
입력 문서를 모두 읽은 뒤, 아래 14개 섹션으로 PRD를 작성한다. 각 섹션에서 2단계 산출물(시장분석·경쟁분석)의 데이터를 근거로 인용한다.

1. **Executive Summary** — 핵심 가치 제안 한 문단
2. **Problem Statement** — 2단계 시장분석 기반, 구체적 pain point 기술
3. **Target Users & Personas** — 주요 사용자 세그먼트 2-3개, 각 페르소나 정의
4. **User Stories** — 핵심 3-5개, `As a [사용자], I want [기능], so that [가치]` 형식
5. **Functional Requirements** — MVP 범위의 기능 목록, 우선순위(P0/P1/P2) 명시. 각 P0 요구사항에 수용 기준(acceptance criteria)을 구체적으로 기술한다.
6. **Non-functional Requirements** — 성능, 보안, 접근성 등
7. **Technical Architecture** — `sc:design`을 1회 호출하여 작성. React Native + TypeScript + Supabase 기준으로 아래 요소를 포함한다:
   - 시스템 구조도 (텍스트 기반, 주요 컴포넌트 간 데이터 흐름 포함)
   - DB 스키마: 주요 테이블별 컬럼·타입·제약조건, 테이블 간 FK 관계, RLS 정책 방향, 필수 인덱스
   - API 설계: 핵심 엔드포인트(경로·메서드·요청/응답 구조), Supabase RPC vs REST 선택 근거
   - **기능-테이블-API 매핑표**: P0 기능 요구사항 각각이 어떤 테이블·API에 대응하는지 대조표 작성
8. **Competitive Differentiation** — 2단계 경쟁분석 기반 차별화 전략
9. **Monetization Strategy** — 수익 모델 구체화
10. **Risk Matrix** — 사업·기술·운영 리스크 및 대응 방안
11. **Assumptions & Constraints** — 사업적 가정, 외부 의존성, 기술 제약 명시
12. **Out of Scope** — MVP에서 명시적으로 제외하는 기능·영역
13. **MVP Roadmap** — 3개월 일정, 월별 마일스톤
14. **Success Metrics** — 측정 가능한 KPI 정의

### 기술 설계 제약
- React Native + TypeScript + Supabase(PostgreSQL) 전용
- 1인 개발 규모에 적합한 설계
- 3개월 MVP 출시 가능한 범위로 한정

### sc:design 호출 지침
- 호출 시점: 섹션 1~6 작성 완료 후
- 입력 컨텍스트: Functional Requirements(P0/P1), Non-functional Requirements, 기술 설계 제약을 전달
- 출력: 시스템 구조도, DB 스키마, API 설계, 기능-테이블-API 매핑표
- 출력물을 PRD 섹션 7에 통합

### 작성 완료 후 자체 점검
PRD 초안 완성 후, 아래 항목을 대조 확인한다:
1. P0 기능 요구사항 각각에 대응하는 DB 테이블과 API 엔드포인트가 매핑표에 존재하는가
2. DB 스키마의 FK 관계가 기능 간 데이터 흐름과 일치하는가
3. API 엔드포인트가 각 P0 기능의 수용 기준(acceptance criteria)을 충족할 수 있는가

## 산출물
| 파일 | 위치 |
|------|------|
| PRD 문서 | `ideas/NNN-아이디어명-prd.md` |

## 전환
- PRD 전체 섹션 작성 완료, 사용자 확인 → "4단계: `/stage-4 NNN-아이디어명`" 안내
- 작성 중 기술적 실현 불가 판단 → "2단계 회귀: `/stage-2 NNN-아이디어명`" 안내
