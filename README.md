# M1-1 「AI 데이터 분석: 데이터 기반 트렌드 분석」

> 코디세이 `AI 응용 학습 (AI Native Master)` 과정 미션 답안입니다.
> 미션 원문은 [`problem.md`](problem.md). **분석 리포트 본체는 [`REPORT.md`](REPORT.md).**

NVDA(엔비디아) 2년 일봉(502건, Yahoo Finance 공개 API)을 정제·분석해 추세·변동성·
계절성 인사이트를 도출한 시계열 분석 리포트입니다.

## 빠른 실행

```bash
pip install -r requirements.txt
python notebooks/analyze.py            # 정제+분석+차트4종 생성
python notebooks/build_dashboard.py    # [보너스] 인터랙티브 대시보드
```

`data/nvda_2y_daily.csv`(원본), `images/final/*.png`(차트), `REPORT.md`(리포트)가
전부 이 레포에 커밋되어 있어 코드를 돌리지 않아도 결과를 바로 확인할 수 있습니다.

## 핵심 인사이트 요약

- 2년간 +107.8% 상승(108.00 → 224.41), 다만 중간에 고점 대비 -60% 조정을 겪음
- 20일 변동성이 분석 전반부(2.97%) > 후반부(2.33%) — 초반 불확실성이 컸다가 안정화
- 요일 계절성은 사실상 무시 가능한 수준(분해 결과 절대값 <0.5)
- 자세한 내용·근거 수치는 [`REPORT.md`](REPORT.md) 참고

## 구조

```
REPORT.md                   필수 산출물 — 분석 리포트 본체
notebooks/
  fetch_data.py              데이터 수집 (Yahoo Finance, 인증 불필요)
  analyze.py                 정제 + 시계열 분석(이동평균/변화율/월별집계) + 시각화 + 보너스(분해/예측)
  build_dashboard.py         [보너스] 인터랙티브 대시보드 HTML 생성
data/nvda_2y_daily.csv       원본 데이터 (502건, 2024-09-03~2026-09-02)
images/final/                시각화 4개 (필수 3 + 보너스 1)
dashboard/index.html         [보너스] 순수 JS+SVG 대시보드 (배포 없이 로컬에서 바로 열림)
captures/dashboard/          [보너스] 위 대시보드를 실제 조작한 캡처 3장 + 필터 시나리오 설명
```

## 보너스

| 항목 | 구현 |
|---|---|
| 대시보드 서비스화 | `dashboard/index.html` — 기간 필터(3개월/6개월/1년/전체) 클릭 시 차트·통계 즉시 재계산. 제출은 "로컬 실행 캡처" 방식(`captures/dashboard/`) |
| 시계열 심화 | (A) 추세/계절성 분해 + (B) 베이스라인 예측(가정/한계 명시) 둘 다 구현 |

## 데이터 출처

Yahoo Finance 공개 차트 API(`query1.finance.yahoo.com/v8/finance/chart/NVDA`) —
API 키/인증 불필요. `notebooks/fetch_data.py`로 재수집 가능(최신 거래일까지 갱신됨).
