# 🏠 집스캐너 (ZipScanner)

> **"진짜 시세를 보여주는, 당신의 매물 분석 파트너 - 집스캐너"**  
> **"지금 보는 집, 시세보다 싼 걸까? 집스캐너로 한눈에 분석하세요!"**

---

## 📌 개요

`집스캐너`는 공공 실거래가 데이터를 기반으로 사용자가 입력한 매물이 실제 시세 대비 저렴한지 분석하고, 이를 시각적으로 제공하는 주거 매물 분석 서비스입니다.

또한, **AI 분석 서버**를 통해 공공데이터 기반의 통계 정보를 요약하고, 해당 매물에 대한 자연어 인사이트를 제공함으로써 부동산 정보에 익숙하지 않은 사용자도 쉽게 이해할 수 있도록 돕는 것이 핵심입니다.

- **사용자 대상**: 실거주 목적자, 부동산 관심자, 투자자 등
- **분석 대상**: 아파트 → 향후 오피스텔/빌라/상가 확장 예정
- **1차 기능**: 로얄동/로얄층, 층별 시세 분포, 유사 매물 가격 비교 및 분석 결과 제공
- **AI 활용 포인트**:
  - 유사 매물 가격 분포 기반으로 자연어 요약 제공
  - "이 매물은 시세보다 8% 저렴하며, 로얄층으로 판단됩니다" 등 사용자 맞춤형 설명 제공

---

## 🌐 시스템 구성도
``` text
[사용자]
   │
   ▼ REST API 호출
[프론트엔드 (React, Vite)]
   │
   ▼
[백엔드 API 서버 (Spring Boot, H2/MySQL)]
   │       ├────────▶ [공공 실거래가 API 수집기]
   │       └────────▶ [AI 분석 서버 (FastAPI, LLM)]
   ▼
[DB 저장소]
```

## 📄 요구사항 정의서

| 구분 | 항목 | 설명 |
|------|------|------|
| 필수 | 실거래가 조회 | 사용자가 입력한 아파트명, 평형, 층수 등으로 유사 매물 시세 조회 |
| 필수 | 유사 매물 비교 | ±2층, ±1평 유사 매물의 평균가, 최고가, 최저가 계산 |
| 필수 | 분석 결과 시각화 | 매물의 시세 적정 여부 시각적으로 표시 (그래프, 컬러 등) |
| 선택 | 자연어 분석 결과 | AI가 요약해주는 "이 매물은 시세보다 약 8% 저렴합니다" 등의 설명 |

---

## 🔧 기능 정의서 (1차 기준)

| 분류 | 기능 | 설명 |
|------|------|------|
| 사용자 | 매물 분석 요청 | 아파트명, 평형, 층수, 희망가격 입력 후 분석 요청 |
| 시스템 | 실거래가 필터링 | 입력 기준 ±2층, ±1평 범위 내 과거 실거래가 조회 |
| 시스템 | 시세 분포 분석 | 평균, 중앙값, 분산 등 통계 정보 제공 |
| 시스템 | 로얄동/로얄층 판단 | 평균가 기준으로 동·층별 위치별 프리미엄 판단 |
| 시스템 | 분석 결과 리포트 | 시각화 및 자연어 분석 요약 출력 (AI 서버 연동 예정) |

---

## 🖥️ 화면 정의서 (1차)

| 화면 | 구성 요소 | 설명 |
|------|-----------|------|
| 메인 | 매물 입력 폼 | 아파트명, 평형, 층수, 희망가격 입력 |
| 결과 | 분석 요약 카드 | 시세보다 몇 % 저렴/비쌈 여부 표시 |
| 결과 | 시세 분포 그래프 | 해당 매물의 위치 및 유사 매물 분포 시각화 |
| 결과 | AI 요약 결과 | 매물에 대한 자연어 분석 설명 (AI 연동 시) |

---

## 🚀 개발 차수 계획

| 차수 | 목표 | 주요 기능 |
|------|------|-----------|
| 1차 | MVP 완성 | 공공 API 연동, DB 저장, 시세 분석 및 기본 UI 구성 |
| 2차 | AI 분석 도입 | FastAPI 기반 AI 서버 구축, LLM 요약 기능 연동 |
| 3차 | 확장 기능 | 단지별 평균가 비교, 학군/지하철 정보 연동, 로그인 기능 등 |

---

## ⚙️ 기술 스택

| 영역 | 기술 | 비고 |
|------|------|------|
| Front-End | React, TypeScript, Vite | MUI 기반 디자인 예정 |
| Back-End | Java, Spring Boot, H2 → MySQL 전환 | REST API 기반 |
| AI 분석 | Python, FastAPI, LLM API (Gemini/Claude 등) | 자연어 설명용 |
| 데이터 | 공공데이터포털 실거래가 API | 국토교통부 아파트 실거래가 |
| 배포 예정 | Vercel(프론트), EC2(백엔드/AI), RDS(MySQL) | 초기 개발은 로컬/내부망 |

---

## 📁 프로젝트 및 Git Repository 명

| 영역 | 프로젝트명 | Git 저장소명 |
|------|-------------|--------------------|
| Front-End | 집스캐너-프론트 | `zip-scanner-fe` |
| Back-End | 집스캐너-백엔드 | `zip-scanner-be` |
| AI Server | 집스캐너-AI | `zip-scanner-ai` |
