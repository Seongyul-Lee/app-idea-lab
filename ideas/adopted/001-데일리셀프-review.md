# 데일리셀프 (DailySelf) — 4단계 정합성 판별 리뷰

> 판별일: 2026-01-31
> 대상: `ideas/001-데일리셀프-prd.md` (v2.0 — 4단계 리뷰 반영판)
> 검증자: Stage 4 비판적 리뷰어
> 리뷰 회차: 2차 (v1.0 리뷰 결함 보완 확인)

---

## v1.0 리뷰 결함 보완 현황

| # | 심각도 | v1.0 결함 | v2.0 보완 | 상태 |
|---|--------|----------|----------|------|
| D-C1 | Critical | 화면 구조 / UI 명세 완전 누락 | 섹션 8 신설 — 네비게이션 트리, 10개 화면 UI 구성, 화면-데이터-API 매핑 작성 | ✅ 해소 |
| D-M1 | Major | KPI / Success Metrics 누락 | 섹션 15 신설 — North Star Metric, KPI 11개(목표치 포함), Aptabase 이벤트 15개, 모니터링 대시보드 | ✅ 해소 |
| A-m1 | Minor | LTV "평균 구독 기간 8개월" 근거 부재 | 섹션 10-3에서 "6개월"로 하향 수정, 습관 앱 이탈률 48% + 구독 앱 churn rate 월 6~8% 근거 명시 | ✅ 해소 |
| B-m1 | Minor | Supabase Free→Pro 전환 트리거 미정의 | R-08에서 구체적 트리거 명시 (동시접속 400+, DB 400MB+, Edge Function 월 400K+) | ✅ 해소 |
| C-m1 | Minor | generate-plan 스코어링 계산식 불명확 | 섹션 7-6 Edge Function 로직에서 score 계산 공식 구체화 (base_score=10, energy_match_bonus 공식, mood_bonus, recent/variety bonus 수치) | ✅ 해소 |
| C-m2 | Minor | daily_plans 집계 필드 갱신 주체 미명시 | 섹션 7-8 매핑표 FR-07에서 "**클라이언트**가 completed_count, total_count, completion_rate를 재계산하여 daily_plans PATCH 호출" 명시 | ✅ 해소 |
| D-m1 | Minor | Roadmap/Milestones 미존재 | 섹션 14 신설 — 12주 로드맵, 주차별 작업/산출물, 마일스톤 4개 | ✅ 해소 |

**v1.0 지적 사항 7건 전부 해소됨.**

---

## 영역별 판정 요약

| 영역 | 판정 | Critical | Major | Minor |
|------|------|----------|-------|-------|
| A. 사업성 검증 | **통과** | 0 | 0 | 1 |
| B. 리스크 검증 | **통과** | 0 | 0 | 0 |
| C. 기술 검증 | **통과** | 0 | 0 | 2 |
| D. 문서 품질 검증 | **통과** | 0 | 0 | 1 |
| **합계** | — | **0** | **0** | **4** |

---

## A. 사업성 검증 — 통과

### A-1. 시장 규모·경쟁분석 정합성 ✅

PRD v2.0의 데이터와 2단계 산출물 대조 검증:

| 항목 | PRD (섹션 2-2) | 시장분석 | 일치 |
|------|---------------|---------|------|
| 직장인 야근 경험률 | 63% | 63% | ✅ |
| 자기계발 실패 1위 | 정시퇴근 어려움 62.4% | 62.4% | ✅ |
| 번아웃 경험률 | 69~93% | 69~93% | ✅ |
| 습관 앱 이탈률 | 48% | 48% | ✅ |
| TAM | 320억 원 (Sensor Tower) | 320억 원 | ✅ |
| SAM 인구 (직장인) | 710만 명 | 710만 명 | ✅ |
| SOM 1년차 | 5~10만 / 1~3억 원 | 5~10만 / 1~3억 원 | ✅ |

경쟁사 6개(루티너리·챌린저스·투두메이트·마이루틴·루빗·앳플리) 분석이 경쟁분석 보고서와 일치하며, "컨디션 적응형 루틴 미제공"이라는 차별점 결론도 동일.

### A-2. 차별점 방어 가능성 ✅

- "컨디션 인식 → 난이도 자동 조절"은 규칙 기반 알고리즘으로 기술적 해자는 낮음
- PRD 섹션 9-3에서 방어 전략을 3축(기술·데이터·실행 속도)으로 분류하고, 데이터 해자와 실행 속도 해자에 집중
- 경쟁분석에서 가장 유사한 루빗·앳플리도 "컨디션 기반 루틴 자동 조절" 미제공 확인

### A-3. 수익 모델 ✅

- 월 3,900원 / 연 29,900원은 마이루틴(월 3,900원 / 연 28,000원)과 동일 가격대로 시장 검증됨 (섹션 10-2)
- 수익 예측 4개 시나리오 제시 (1년차 보수적~2년차 낙관적)
- Progressive Paywall 전략(무료 가치 체감 → 자연스러운 업셀)이 구체적

### A-4. TAM/SAM/SOM 논리적 근거 ✅

- TAM: 320억 원 (Sensor Tower 실측 기반) — 보수적이고 적절
- SAM: 85억 원 (710만 × 4% × 연 29,900원) — 논리적
- SOM: 1년차 1~3억 원 — 마이루틴 2년 50만 사례 참조, 현실적

**Minor 발견:**
- [A-m1] PRD 섹션 10-3 수익 예측에서 "1년차 기본" 시나리오(10만 사용자 × 4% × 연 29,900원 = 1.2억)와 본문의 SOM "1~3억 원" 사이에 경미한 불일치. 4,000명 × 29,900원 = 1.196억으로 "1~3억" 범위 내이므로 문제는 없으나, 보수적 시나리오(1,500명 × 29,900원 = 4,500만)는 SOM 하한 1억에 미달. 시나리오별 범위를 명확히 하면 좋음. (Minor, 문서 결함)

---

## B. 리스크 검증 — 통과

### B-1. 핵심 리스크 식별 ✅

섹션 11에서 10개 리스크를 유형(사업/기술/법률/운영)·발생확률·영향도로 분류하고 대응 방안을 명시:

| 유형 | 리스크 수 | 대응 방안 존재 |
|------|----------|--------------|
| 사업 | 5개 (R-01~R-05) | ✅ 전부 |
| 기술 | 3개 (R-06~R-08) | ✅ 전부 |
| 법률 | 1개 (R-09) | ✅ |
| 운영 | 1개 (R-10) | ✅ |

시장분석의 5대 리스크가 PRD의 R-01~R-05와 정확히 매핑됨.

### B-2. 외부 의존성 리스크 ✅

| 외부 서비스 | 의존도 | 장애 시 영향 | 대응 |
|------------|--------|------------|------|
| Supabase | 높음 | 데이터 CRUD 불가 | Offline-First (op-sqlite) 최대 24시간 독립 운영 |
| RevenueCat | 중간 | 결제 불가 | 무료 기능 정상 작동 |
| OAuth | 중간 | 신규 가입 불가 | 기존 세션 유효 시 영향 없음 |
| Expo Push | 낮음 | 알림 미수신 | P1 기능, 앱 내 유도로 대체 |
| Aptabase | 낮음 | 분석 미수집 | 핵심 기능 영향 없음 |

v1.0에서 Minor였던 Supabase Free→Pro 전환 트리거가 R-08에서 구체화됨 (동시접속 400+, DB 400MB+, Edge Function 월 400K+).

---

## C. 기술 검증 — 통과

### C-1. React Native + TypeScript + Supabase 구현 가능성 ✅

PRD에 명세된 모든 P0 기능(FR-01~FR-08)은 기술 스택 범위 내에서 구현 가능:

- 소셜 로그인: Supabase Auth + OAuth 연동은 표준적 구현
- 아침 체크인: 슬라이더/탭 UI는 React Native Paper 표준 컴포넌트
- 적응형 플랜: 규칙 기반 알고리즘은 Edge Function(Deno)에서 구현 가능, 외부 AI API 불필요
- 주간 리포트: PostgreSQL Function + Victory Native 차트 조합으로 구현 가능
- 오프라인 지원: MMKV + op-sqlite + Sync Queue 패턴은 검증된 접근법

### C-2. 1인 개발 규모 적정성 ✅

- 테이블 8개(+ routine_categories), Edge Function 2개, RPC 4개, REST 엔드포인트 14개
- Zustand Store 8개로 상태 관리
- Expo Managed Workflow 선택으로 네이티브 빌드 부담 최소화
- 12주 로드맵이 기능 단위로 분할되어 현실적

### C-3. 3개월 MVP 범위 현실성 ✅

- P0 기능 8개(FR-01~FR-08)가 6주차까지 핵심 루프 완성
- 9주차에 오프라인/동기화, 10주차에 P1 기능, 11주차 결제, 12주차 QA/출시
- 마일스톤 4개(M1~M4)로 진행도 추적 가능
- 핵심 차별화 기능(FR-05)의 알고리즘이 규칙 기반이므로 복잡한 ML 파이프라인 불필요

### C-4. DB 스키마·API 설계 정합성 ✅

- 8개 테이블의 FK 관계가 데이터 흐름과 일치
- RLS 정책이 CRUD 권한 매트릭스와 일치 (plan_items의 서브쿼리 기반 RLS 포함)
- API 엔드포인트 20개가 P0 기능 요구사항을 모두 커버
- 기능-테이블-API 매핑표(섹션 7-8)에서 FR-01~FR-08 전체 매핑 확인

### C-5. 장애 시나리오 대응 ✅

- 네트워크 오류: Sync Queue(재시도 5회, 지수 백오프)로 처리
- 서버 다운: Offline-First(op-sqlite 캐시)로 핵심 기능 유지, 최대 24시간 독립 운영
- 체크인 스킵: get_recent_avg_condition RPC로 최근 7일 평균 기반 기본 플랜 제공(AC-03-5)

### C-6. 오프라인 우선 설계 ✅

- 저장소별 역할 분담 명확 (MMKV: 설정/토큰, op-sqlite: 구조화 캐시, Supabase: 원본)
- op-sqlite 로컬 스키마 정의 완료 (sync_queue, local_checkins, local_daily_plans, local_plan_items, local_routines)
- 동기화 큐 로직: created_at ASC 순서, 배치 10개, 재시도 5회, 지수 백오프
- 동기화 트리거: 앱 포그라운드 진입, 네트워크 상태 변경, 수동 새로고침
- 충돌 해결: Server Wins 정책, 시나리오별(체크인 중복, 플랜 변경, 루틴 수정) 처리 방식 명시

### C-7. 핵심 DB Function SQL 본문 ✅

5개 DB Function 모두 완성된 SQL 본문 제공 (스텁이 아닌 실행 가능한 SQL):
- `get_weekly_stats`: JSON 응답 구조, 인사이트 2개 유형(에너지-달성 상관, 수면-에너지 상관) 계산 로직 포함
- `get_user_routine_count`: 구독 상태별 한도 계산 포함
- `get_recent_avg_condition`: 최근 N일 평균 + 최빈 mood 계산 포함
- `seed_default_routines`: 카테고리별 템플릿 INSERT 포함
- `handle_new_user`: profiles + subscriptions 자동 생성 포함

### C-8. TypeScript 인터페이스 ✅

18개 인터페이스 정의 완료 — 요청/응답 타입이 모두 작성됨:
- 데이터 모델: Profile, Routine, Checkin, DailyPlan, PlanItem, Reflection
- 요청: CreateRoutineRequest, UpdateRoutineRequest, CreateCheckinRequest, UpdatePlanItemRequest, GeneratePlanRequest, DeleteAccountRequest, CreateReflectionRequest, UpdateProfileRequest
- 응답: GeneratePlanResponse, DeleteAccountResponse, WeeklyStatsResponse, RoutineCountResponse
- 공통: Mood, PlanType, SubscriptionStatus

### C-9. 상태 관리 구조 ✅

Zustand Store 8개 정의 (섹션 7-7):
- useAuthStore, useCheckinStore, useRoutineStore, usePlanStore, useReportStore, useSubscriptionStore, useSettingsStore, useSyncStore
- 각 Store별 주요 상태 필드, 역할, persist 전략(MMKV/op-sqlite/없음) 명시

**Minor 발견:**
- [C-m1] generate-plan Edge Function에서 "기존 플랜 존재 시 삭제 후 재생성"하는데, 이때 사용자가 이미 일부 루틴을 완료 체크한 상태에서 체크인을 다시 하면 완료 기록이 소실된다. 하루 1회 체크인(UNIQUE 제약)이므로 체크인 수정(UPDATE) 시나리오에서만 발생하나, 이 경우 사용자 경고 여부가 미정의. (Minor, 문서 결함)
- [C-m2] op-sqlite 로컬 스키마에서 local_daily_plans 테이블에 completed_count, total_count, completion_rate 필드가 누락되어 있음. 서버 스키마(daily_plans)에는 존재. 오프라인 상태에서 달성률 표시를 위해 로컬에도 필요할 수 있음. (Minor, 문서 결함)

---

## D. 문서 품질 검증 — 통과

### D-1. 목표·기능·기술 명세 간 모순 검사 ✅

P0 기능 요구사항(FR-01~FR-08)의 입력/출력/제한사항이 DB 스키마 및 API 설계와 일관됨:

| 확인 항목 | 결과 |
|----------|------|
| FR-03 수면 시간 "0.5시간 단위" ↔ DB sleep_hours NUMERIC(3,1) | ✅ 일치 |
| FR-04 무료 루틴 5개 한도 ↔ get_user_routine_count max_custom=5 | ✅ 일치 |
| FR-05 에너지 1~2 → 최대 2개 ↔ generate-plan max_routines 정의 | ✅ 일치 |
| FR-07 달성률 계산식 ↔ daily_plans.completion_rate | ✅ 일치 |
| FR-08 최소 3일 데이터 ↔ AC-08-3 | ✅ 일치 |
| 섹션 10 가격 ↔ 섹션 5 FR-11 구독 가격 | ✅ 일치 |
| 섹션 14 로드맵 ↔ P0/P1/P2 우선순위 | ✅ 일치 (P0 1~8주, P1 10주, 결제 11주) |

### D-2. 섹션 존재 여부 ✅

| # | 필수 섹션 | PRD 존재 | 상태 |
|---|----------|---------|------|
| 1 | Executive Summary | 섹션 1 | ✅ |
| 2 | Problem Statement | 섹션 2 | ✅ |
| 3 | Target Users & Personas | 섹션 3 | ✅ |
| 4 | User Stories | 섹션 4 | ✅ |
| 5 | Functional Requirements | 섹션 5 | ✅ |
| 6 | Non-functional Requirements | 섹션 6 | ✅ |
| 7 | Technical Architecture | 섹션 7 | ✅ |
| 8 | **Screen Map & UI 명세** | **섹션 8** | ✅ **(v2.0 신설)** |
| 9 | Competitive Differentiation | 섹션 9 | ✅ |
| 10 | Monetization Strategy | 섹션 10 | ✅ |
| 11 | Risk Matrix | 섹션 11 | ✅ |
| 12 | Assumptions & Constraints | 섹션 12 | ✅ |
| 13 | Out of Scope | 섹션 13 | ✅ |
| 14 | **MVP Roadmap** | **섹션 14** | ✅ **(v2.0 신설)** |
| 15 | **Success Metrics** | **섹션 15** | ✅ **(v2.0 신설)** |

**15개 섹션 전체 존재.** v1.0에서 누락되었던 3개 섹션(8, 14, 15)이 모두 추가됨.

### D-3. 수용 기준(AC) 검증 ✅

모든 P0 기능(FR-01~FR-08)에 AC-XX-X 형식의 수용 기준이 존재:

| P0 기능 | AC 개수 | 검증 가능성 |
|---------|---------|-----------|
| FR-01 소셜 로그인 | AC-01-1~3 (3개) | ✅ 조건문 형태 |
| FR-02 온보딩 | AC-02-1~3 (3개) | ✅ 조건문 형태 |
| FR-03 체크인 | AC-03-1~5 (5개) | ✅ 조건문 형태 |
| FR-04 루틴 CRUD | AC-04-1~4 (4개) | ✅ 조건문 형태 |
| FR-05 적응형 플랜 | AC-05-1~5 (5개) | ✅ 조건문 형태 |
| FR-06 플랜 수동 조정 | AC-06-1~3 (3개) | ✅ 조건문 형태 |
| FR-07 완료 체크 | AC-07-1~3 (3개) | ✅ 조건문 형태 |
| FR-08 주간 리포트 | AC-08-1~3 (3개) | ✅ 조건문 형태 |

총 29개 AC, 모두 검증 가능한 조건문 형태.

### D-4. User Story 커버리지 ✅

27개 User Story가 9개 Epic으로 분류 (온보딩·인증·체크인·루틴·플랜·회고·리포트·설정·결제). 27개 ≥ 15개 최소 요건 충족.

### D-5. Screen Map ✅ (v2.0 신설)

섹션 8에서:
- **네비게이션 구조 트리**: Expo Router 파일 기반 라우팅 구조 (`(auth)`, `(tabs)`, `(modal)`) 완전 정의
- **핵심 화면 10개**: 로그인, 온보딩 2개, 홈(플랜), 체크인 모달, 루틴 관리, 루틴 생성 모달, 주간 리포트, 설정, 구독 관리 — 각 화면별 영역·구성 상세 기술
- **네비게이션 흐름**: 앱 시작 → 인증 분기 → 각 화면 이동 흐름 도식화
- **화면-데이터-API 매핑**: 10개 화면별 Zustand Store + API 호출 + 데이터 흐름 매핑 완료

### D-6. 기능-테이블-API 매핑표 ✅

섹션 7-8에 매핑표 존재. P0 기능 FR-01~FR-08 전체가 매핑됨. v1.0 대비 FR-07에 "클라이언트가 집계 필드 재계산" 명시 추가.

### D-7. KPI ✅ (v2.0 신설)

섹션 15에서:
- **North Star Metric**: "주 3일 이상 체크인하는 사용자 비율" 선정 + 선정 근거
- **핵심 KPI 11개**: 사용자(DAU/MAU, D1/D7/D30 리텐션), 제품(체크인 빈도, Weekly Active Checkin Rate, 리포트 조회율, 평균 달성률), 비즈니스(유료 전환율, MRR, 앱 스토어 평점)
- **KPI별 목표치**: 1개월/3개월/6개월 목표 수치 제시
- **Aptabase 이벤트 15개**: 트리거 시점 + 속성(properties) 정의
- **모니터링 대시보드**: 4개 도구별(Aptabase/RevenueCat/Supabase/앱스토어) 주요 지표

**Minor 발견:**
- [D-m1] 섹션 7-9 자체 점검 결과 #8에서 "✅ 충족"으로 기재되어 있으나, 이는 v2.0 보완 후의 상태를 반영한 것이므로 문서 이력상 v1.0에서 미충족이었다가 v2.0에서 충족된 것이 명확하지 않음. 문서 이력 관리 측면의 경미한 이슈. (Minor, 문서 결함)

---

## 미달 목록 종합

| # | 심각도 | 유형 | 영역 | 내용 |
|---|--------|------|------|------|
| A-m1 | Minor | 문서 결함 | A | 수익 예측 "보수적 1년차"(4,500만) 시나리오가 SOM 하한(1억)에 미달하나, SOM 자체가 범위이므로 실질적 모순 아님 |
| C-m1 | Minor | 문서 결함 | C | 체크인 수정(UPDATE) 시 기존 완료 기록이 소실되는 시나리오의 사용자 경고 미정의 |
| C-m2 | Minor | 문서 결함 | C | op-sqlite local_daily_plans에 completed_count/total_count/completion_rate 필드 누락 (오프라인 달성률 표시에 필요할 수 있음) |
| D-m1 | Minor | 문서 결함 | D | 자체 점검 결과의 버전 이력 미반영 (v1.0→v2.0 변경 추적 불명확) |

---

## 최종 판정

### 판정: **통과**

**근거:**
- v1.0에서 지적된 Critical 1건(화면 구조 누락), Major 1건(KPI 누락)이 모두 **완전히 해소**됨
- v1.0의 Minor 5건도 전부 보완됨
- v2.0에서 새로 발견된 결함은 **Minor 4건**에 불과하며, Critical/Major 없음
- 사업성(A), 리스크(B), 기술(C), 문서 품질(D) **4개 영역 모두 통과**
- **CLAUDE.md의 Task Master 투입 요건** 전체 충족:
  - ✅ 기능 명세: P0/P1/P2 우선순위, 입력/출력/제한사항
  - ✅ 수용 기준: 29개 AC-XX-X 형식 조건문
  - ✅ DB 스키마: CREATE TABLE SQL 8개, FK, 인덱스, RLS 정책, DB Function SQL 5개 완성
  - ✅ API 설계: 20개 엔드포인트, TypeScript 인터페이스 18개
  - ✅ 아키텍처 상세도: 기술 스택, 시스템 구조도, Zustand Store 8개, 기능-테이블-API 매핑표
  - ✅ 화면 구조 / UI 명세: 네비게이션 트리, 10개 화면별 UI 구성, 화면-데이터-API 매핑
  - ✅ 오프라인/동기화 설계: MMKV/op-sqlite 역할 분담, Sync Queue 로직, Server Wins 충돌 해결

### 다음 단계

→ 5단계: **`/stage-5 001-데일리셀프 채택`**
