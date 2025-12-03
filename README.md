# ⚾ MLB 투구 구종 예측 모델 (Pitch Type Prediction)

> **Ensemble Learning with XGBoost & AutoGluon** \> **Target Player:** Yoshinobu Yamamoto (2025 Season)

## 📖 프로젝트 개요 (Overview)

이 프로젝트는 **2025년 MLB Statcast 데이터**를 활용하여 투수의 다음 투구 구종을 예측하는 머신러닝 모델을 구축한 연구입니다.
단일 알고리즘의 한계를 극복하기 위해 **XGBoost**와 **AutoGluon**을 결합한 **앙상블(Ensemble)** 기법을 적용하였으며, 특히 **구종 범주화(Pitch Categorization)** 전략을 통해 데이터 불균형 문제를 해결하고 예측의 실효성을 높이는 데 초점을 맞추었습니다.

이 연구는 단순히 물리적 트래킹 데이터(구속, 회전수 등)에 의존하지 않고, **볼카운트, 주자 상황, 점수 차 등 '경기 맥락(Game Context)' 변수**만으로 투수의 심리와 전술을 예측했다는 점에서 의의가 있습니다.

-----

## 📂 파일 구성 (File Structure)

| 파일명 | 설명 (Description) |
| :--- | :--- |
| **`model1.ipynb`** | **[Baseline Model] 세부 구종 예측 모델** <br> - 6가지 세부 구종(FF, FC, SI, SL, FS, CU)을 개별적으로 예측 <br> - 데이터 불균형 및 유사 구종 간 오분류 문제 확인 |
| **`model2.ipynb`** | **[Proposed Model] 구종 범주화 예측 모델** <br> - 유사 구종을 3개 범주(Fastball, Breaking, Offspeed)로 통합 <br> - 정확도 및 F1-Score 대폭 향상 <br> - 볼카운트/주자/좌우타자별 심층 분석 및 시각화 포함 |

-----

## 🛠 사용 기술 (Tech Stack)

  * **Language:** Python 3.10+
  * **Data Collection:** `pybaseball` (MLB Statcast)
  * **ML Libraries:**
      * `XGBoost` (Gradient Boosting)
      * `AutoGluon` (AutoML Framework)
      * `Scikit-learn` (Preprocessing & Evaluation)
  * **Visualization:** `Matplotlib`, `Seaborn`

-----

## 📊 연구 방법론 (Methodology)

### 1\. 데이터 수집 및 전처리

  * **대상:** 야마모토 요시노부 (Yoshinobu Yamamoto, LAD) 2025시즌 투구 데이터
  * **Feature:** 경기 상황 변수만 사용 (물리 데이터 배제)
      * `balls`, `strikes`, `outs`, `inning`, `score_diff`
      * `on_1b`, `on_2b`, `on_3b` (주자 유무)
      * `stand` (좌/우 타자)
  * **Split:** Train/Test (8:2), Stratified Split 적용

### 2\. 모델링 전략

  * **앙상블 (Ensemble):** XGBoost (가중치 0.6) + AutoGluon (가중치 0.4) -\> **Weighted Soft Voting**
  * **범주화 (Categorization):**
      * **Fastball Group:** 포심(FF), 싱커(SI), 커터(FC)
      * **Breaking Group:** 슬라이더(SL), 커브(CU), 스위퍼(ST)
      * **Offspeed Group:** 스플리터(FS), 체인지업(CH)

-----

## 📈 실험 결과 (Results)

### 1\. 성능 비교 (Model 1 vs Model 2)

구종 범주화 전략(Model 2)을 적용했을 때, 세부 구종 모델(Model 1) 대비 **약 47%의 성능 향상**을 달성했습니다.

| 모델 | 타겟 클래스 | Accuracy | Weighted F1-Score | 비고 |
| :--- | :---: | :---: | :---: | :--- |
| **Model 1** | 6개 (세부 구종) | 0.36 | 0.33 | 유사 구종 혼동 다수 |
| **Model 2** | **3개 (범주화)** | **0.53** | **0.48** | **Fastball Recall: 0.78** |

### 2\. 주요 분석 시각화

`model2.ipynb`에서는 다음과 같은 다양한 상황별 투구 패턴 분석을 제공합니다.

  * **Confusion Matrix:** 모델의 오분류 패턴 분석
  * **Ball Count Heatmap:** 볼카운트별(유리/불리) 투구 성향 분석
  * **Platoon Split:** 좌타자 vs 우타자 상대 전략 비교
  * **Clutch Situation:** 득점권/만루 위기 시 투구 변화 분석
  * **Strategy Sheet:** 현장에서 활용 가능한 타자별 공략 가이드 시각화

-----

## 📝 결론 (Conclusion)

본 연구는 복잡한 트래킹 장비 없이 **경기 상황 데이터**만으로도 투수의 전략적 흐름을 읽어낼 수 있음을 입증했습니다. 특히 **구종 범주화**는 모델의 예측 신뢰도를 높여, 타자의 타이밍 싸움과 전력 분석팀의 전략 수립에 실질적인 도움을 줄 수 있는 방법론입니다.

-----
