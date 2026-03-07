# HANEUL 예산 관리 프로젝트

## 프로젝트 개요
토스 스타일 예산 관리 대시보드. 지출 데이터를 JSON으로 관리하고 HTML 보고서로 시각화.

## 파일 구조
```
budget-report-2026/
├── CLAUDE.md              # 프로젝트 설정
├── budget-data.json       # 예산 데이터 (원본)
├── budget-report.html     # 토스 스타일 보고서
└── backup/
    └── {연도}/
        └── {월}/
            └── budget-data-YYYYMMDD-HHMMSS.json
```

## 작업 규칙

### 데이터 추가 시
1. `backup/{연도}/{월}/budget-data-YYYYMMDD-HHMMSS.json` 백업
2. `budget-data.json` 업데이트
3. `budget-report.html` 내 budgetData 객체 동기화
4. summary 재계산 (totalExpenses, remainingBudget, dailyAvailable)

### 백업 명령어
```bash
cp budget-data.json backup/$(date +%Y)/$(date +%m)/budget-data-$(date +%Y%m%d-%H%M%S).json
```

### 지출 입력 형식
```
날짜 항목 금액 [카테고리]
예: 2/16 점심 12000원 식비
예: 2/16 커피 4500
```

### 카테고리
- 식비, 장보기, 카페, 경조사, 교통, 쇼핑, 투자, 여가

### 예산 계산
- 총 예산: budget.february2025.totalBudget
- 남은 예산: totalBudget - totalExpenses
- 일 가용액: remainingBudget / daysRemaining

## 현재 상태 (2026-03)
- 월 사용한도: 900,000원
- 급여: 6,370,000원
- 마지막 업데이트: 2026-03-01

### 3월 저축/투자
- 연금저축: 500,693원
- ISA: 500,000원
- 비상금 CMA: 600,000원
- IRP: 250,000원
- **합계**: 1,850,693원

## 이전 상태 (2025-02)
- 예산: 1,300,000원
- 기본 예산: 900,000원 + 추가수입 400,000원

## Skills 참조
- `/Users/ihaneul/claude/skills/toss-react-ui.skill`
- `/Users/ihaneul/claude/skills/toss-style-wiki.skill`

## 보고서 확인
```bash
open budget-report.html
```
