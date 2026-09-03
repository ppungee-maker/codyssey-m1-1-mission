# 📈 엔비디아 주가, 2년치 데이터로 파헤쳐보기

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)
![Data](https://img.shields.io/badge/데이터-Yahoo%20Finance-6f42c1)
![No Auth](https://img.shields.io/badge/API%20키-필요없음-brightgreen)
![AI 사전평가](https://img.shields.io/badge/AI%20사전평가-100%25%20(17%2F17)-success)

> 🎓 코디세이 `AI 응용 학습 (AI Native Master)` 과정 미션 **M1-1** 답안입니다.
> 미션 원문이 궁금하면 [`problem.md`](problem.md), 분석 전체를 제대로 읽고
> 싶으면 [`REPORT.md`](REPORT.md)로 가세요. 이 README는 "일단 뭘 한 건지"만
> 빠르고 쉽게 보여드리는 안내판이에요.

---

## 🙋 이게 뭐하는 프로젝트예요?

한 줄로 말하면: **"엔비디아(NVDA) 주가가 지난 2년 동안 어떻게 움직였는지,
숫자로 직접 확인해본 것"**이에요.

주식 얘기가 나오면 복잡해 보이지만, 사실 하는 일은 단순해요.

1. 엔비디아의 최근 2년치 하루 주가 기록(502일치)을 인터넷에서 받아온다
2. 이상한 값(빠진 값, 말이 안 되는 값)이 있는지 확인하고 정리한다
3. "얼마나 올랐나", "언제 많이 흔들렸나" 같은 질문에 답을 그래프로 그려본다
4. 발견한 내용을 사람이 읽을 수 있는 글(리포트)로 정리한다

이 저장소엔 그 전체 과정 — **원본 데이터, 분석 코드, 결과 그래프, 최종 글**까지
전부 들어있어서, 코드를 안 돌려봐도 결과를 바로 확인할 수 있어요.

---

## ✨ 발견한 것 3가지 (전문 용어 없이)

| 발견 | 쉽게 풀면 |
|---|---|
| 📈 **2년간 +107.8% 상승** (108.00 → 224.41달러) | 2년 전에 100만원 넣었으면 지금 약 208만원이 됐다는 뜻이에요. |
| 📉 **중간에 -60% 급락** (2025년 4월경) | 그런데 쭉 오르기만 한 게 아니라, 중간에 최고점 대비 반토막 넘게 떨어진 적이 있어요. "그냥 사놓고 기다리면 됐다"는 말은 절반만 맞는 얘기죠. |
| 😌 **최근이 더 안정적** (변동폭 2.97% → 2.33%) | 초반엔 하루하루 가격이 크게 출렁였는데, 뒤로 갈수록 흔들림이 잦아들었어요. |

> 더 자세한 근거 수치와 그래프는 👉 [`REPORT.md`](REPORT.md)에서 하나씩 설명해요.

---

## 🖼 그래프로 보기

| 그래프 | 뭘 보여주나요? |
|---|---|
| [`01_price_trend.png`](images/final/01_price_trend.png) | 종가(하루 마감 가격)와 그 흐름을 부드럽게 이어 그린 선 두 개(단기·중기 평균) |
| [`02_volatility.png`](images/final/02_volatility.png) | 하루하루 가격이 얼마나 출렁였는지 |
| [`03_monthly_stats.png`](images/final/03_monthly_stats.png) | 한 달 단위로 뭉쳐서 본 큰 흐름 |
| [`04_decomposition.png`](images/final/04_decomposition.png) | 🎁(보너스) 가격 변화를 "큰 흐름" + "요일 패턴" + "나머지 흔들림"으로 3등분해서 보기 |
| [`05_aggregation_comparison.png`](images/final/05_aggregation_comparison.png) | 🎁(보너스) 똑같은 데이터도 "하루 단위"로 볼 때랑 "일주일 단위"로 볼 때 숫자가 달라진다는 걸 실제로 비교 |

---

## 🚀 직접 실행해보고 싶다면

컴퓨터에 Python이 설치돼 있다면, 아래 세 줄이면 끝이에요.

```bash
pip install -r requirements.txt      # ① 필요한 도구 설치
python notebooks/analyze.py          # ② 데이터 정리 + 분석 + 그래프 5장 생성
python notebooks/build_dashboard.py  # ③ (보너스) 클릭해서 갖고 노는 대시보드 만들기
```

> 💡 이미 결과 파일이 다 커밋돼 있어서, 이 명령어를 안 돌려도 위 그래프와
> [`REPORT.md`](REPORT.md)만 봐도 충분히 결과를 확인할 수 있어요.
> 명령어는 "내가 직접 재현해보고 싶을 때"만 실행하면 돼요.

---

## 📂 저장소 구조 (뭐가 어디에 있나요)

```
REPORT.md                    ⭐ 분석 결과를 정리한 글 (이걸 제일 먼저 읽으세요)
problem.md                    미션 원문(문제)
docs/01-AI사용로그.md         AI를 어떻게, 어디까지 썼는지 기록
notebooks/
  ├─ fetch_data.py            데이터 받아오기
  ├─ analyze.py                데이터 정리 + 분석 + 그래프 만들기
  └─ build_dashboard.py        (보너스) 대시보드 만들기
data/nvda_2y_daily.csv        원본 데이터 (502일치)
images/final/                 그래프 파일 5장
dashboard/index.html          (보너스) 브라우저에서 바로 열리는 대시보드
captures/dashboard/           (보너스) 대시보드 실제로 써본 화면 캡처
```

---

## 🎁 보너스로 더 해본 것

- **인터랙티브 대시보드**: `dashboard/index.html`을 브라우저로 열면, 기간(3개월/
  6개월/1년/전체) 버튼을 눌러서 그래프가 바로바로 바뀌는 걸 볼 수 있어요.
- **한 걸음 더 들어간 분석**: 가격 변화를 "큰 흐름 vs 반복 패턴 vs 우연한 흔들림"
  으로 쪼개보기, 그리고 "최근 흐름이 계속된다면?"을 가정한 아주 단순한 예측
  (+ 그 예측이 왜 완벽하지 않은지도 같이 설명).

---

## 📊 데이터는 어디서 났나요?

**Yahoo Finance**라는, 누구나 무료로 쓸 수 있는 주가 정보 사이트의 공개
API에서 받았어요. 회원가입이나 API 키 같은 게 전혀 필요 없어서, `notebooks/fetch_data.py`
를 실행하면 이 글을 쓴 시점 이후의 최신 데이터로도 다시 받아올 수 있어요.

---

<details>
<summary>🔍 평가자용 — REPORT.md 항목별 위치 안내 (펼치기)</summary>

아래 표는 요약본만으로는 확인하기 어려운 세부 항목이 `REPORT.md`의 어디에
있는지 안내합니다.

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

</details>
