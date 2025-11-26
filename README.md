# ⚾ MLB Pitcher Mind: 상황 기반 투구 예측 AI 시스템

![Python](https://img.shields.io/badge/Python-3.8%2B-blue) ![XGBoost](https://img.shields.io/badge/XGBoost-Ensemble-green) ![AutoGluon](https://img.shields.io/badge/AutoML-AutoGluon-orange) ![Statcast](https://img.shields.io/badge/Data-PyBaseball-red)

## 📖 프로젝트 개요 (Overview)
이 프로젝트는 MLB 투수의 투구 패턴을 분석하여, **"특정 경기 상황(볼카운트, 주자, 점수차 등)에서 투수가 어떤 구종을 던질지"** 예측하는 AI 모델입니다.
단일 모델의 한계를 극복하기 위해 **XGBoost**와 **AutoGluon(AutoML)**을 결합한 **앙상블(Ensemble)** 기법을 적용했으며, 최종적으로 코칭 스태프가 활용할 수 있는 **'상황별 구종 전략 시트(Strategy Sheet)'**를 도출하는 것을 목표로 합니다.

## 💡 핵심 기능 (Key Features)
* **상황 기반 예측 (Context-Aware Prediction):** 투구 릴리스 포인트나 구속 등 '투구 후' 데이터가 아닌, **투구 전(Pre-pitch)** 알 수 있는 정보(볼카운트, 주자 상황, 이닝 등)만을 사용하여 실전성을 높였습니다.
* **고성능 앙상블 모델링:** 전통적인 강자 **XGBoost**와 최신 AutoML 프레임워크인 **AutoGluon**의 예측 확률을 가중 평균하여 정확도와 일반화 성능을 극대화했습니다.
* **자동화된 전략 리포트:** 192가지 경기 상황(볼카운트 × 주자 × 타자 손잡이)에 대한 최적 구종을 분석하여 `csv` 및 `시각화 표`로 자동 생성합니다.
* **데이터 시각화:** Confusion Matrix, 볼카운트별 히트맵, 타자 유형별 전략 비교표 등을 통해 모델의 판단 근거를 시각적으로 제시합니다.

## 🛠 사용 기술 (Tech Stack)
* **Data Collection:** `pybaseball` (Statcast API)
* **Preprocessing:** `Pandas`, `NumPy`
* **Modeling:** `XGBoost`, `AutoGluon.tabular`, `Scikit-learn`
* **Visualization:** `Matplotlib`, `Seaborn`

## 📊 분석 프로세스 (Methodology)
1.  **Data Acquisition:** MLB Statcast 데이터를 실시간으로 수집합니다.
2.  **Feature Engineering:**
    * 범주형 변수(타자/투수 손잡이) 인코딩 (L/R → 0/1)
    * 희귀 구종 제거 및 데이터 밸런싱
    * 상황 변수(볼카운트, 점수차, 주자 유무) 추출
3.  **Model Training:**
    * **Model A:** XGBoost Classifier (Hyperparameter Tuning)
    * **Model B:** AutoGluon Tabular Predictor (Multi-model Stacking)
    * **Ensemble:** Soft Voting (Weighted Average)
4.  **Strategy Generation:** 모든 경우의 수(Batch Prediction)를 입력하여 상황별 최적 전략 도출

## 📈 결과물 예시 (Result)
*(여기에 코드 실행 후 나온 '전략 시트 이미지'나 '히트맵 이미지'를 캡처해서 넣으세요)*

### 1. 우타자/좌타자 상대 전략 시트
투수가 타자의 손잡이와 주자 상황에 따라 구종 배합을 어떻게 가져가는지 분석한 결과입니다.
*(이미지 삽입)*

### 2. 모델 성능 평가
* **XGBoost + AutoGluon Ensemble Accuracy:** XX.X% (예시)
* **F1-Score:** 0.XX

## 🚀 실행 방법 (How to Run)
```bash
# 1. 필수 라이브러리 설치
pip install pybaseball autogluon.tabular scikit-learn xgboost matplotlib seaborn

# 2. 코드 실행
python pitch_prediction.py
