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

## 분석 과정·검증 (REPORT.md 섹션 안내)

요약본만으로는 확인하기 어려운 항목들이 `REPORT.md`에 명시적으로 들어있습니다 —
평가자는 아래 섹션을 참고해 주세요.

| 확인 항목 | REPORT.md 위치 |
|---|---|
| 데이터 로딩→정제→분석→시각화 단계별 흐름 | [3.1 분석 파이프라인](REPORT.md#31-분석-파이프라인) |
| 결측치/이상치 처리 기준과 그 이유 | [3절 정제 기준](REPORT.md#3-데이터-설명) |
| 시각화 집계 단위(일/월) 선택 이유 | [3절 집계 단위 선택 이유](REPORT.md#3-데이터-설명) |
| 각 시계열 기법이 "무엇을 보려는 것"인지 | [4절 적용한 시계열 분석 기법](REPORT.md#4-적용한-시계열-분석-기법) |
| 트렌드/계절성/노이즈를 그래프에서 구분하는 법 | [8-A절 추세/계절성 분해](REPORT.md#a-추세계절성-분해) |
| 인사이트 1개의 Fact→Why→Action 흐름 | [6.1 인사이트 심화](REPORT.md#61-인사이트-심화--fact--why--action-예시) |
| 반례(다른 집계 단위, 실측 차트 포함) | [7.1 반례](REPORT.md#71-반례--이-결론이-달라질-수-있는-경우) + [`05_aggregation_comparison.png`](images/final/05_aggregation_comparison.png) |
| 한계점 + 추가로 필요한 데이터 제안 | [7절/7.1절](REPORT.md#7-결론-및-한계점) |
| 인사이트별 행동(Action) 권고 | [6절 인사이트](REPORT.md#6-인사이트) 각 항목 "행동" 문장 |
| AI 검증 방법 + AI 없이 결론 재구성 | [9절 AI 활용 및 검증](REPORT.md#9-ai-활용-및-검증) |
| AI 사용 로그(프롬프트/응답 요약) | [`docs/01-AI사용로그.md`](docs/01-AI사용로그.md) |

## 구조

```
REPORT.md                   필수 산출물 — 분석 리포트 본체
docs/01-AI사용로그.md        AI 프롬프트/응답 요약 + 검증 지점
notebooks/
  fetch_data.py              데이터 수집 (Yahoo Finance, 인증 불필요)
  analyze.py                 정제 + 시계열 분석(이동평균/변화율/월별집계) + 시각화 + 보너스(분해/예측/집계비교)
  build_dashboard.py         [보너스] 인터랙티브 대시보드 HTML 생성
data/nvda_2y_daily.csv       원본 데이터 (502건, 2024-09-03~2026-09-02)
images/final/                시각화 5개 (필수 3 + 보너스 1 + 반례 1)
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
