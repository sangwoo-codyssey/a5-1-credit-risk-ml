# A5-1 - 대출 여부를 판단하는 AI (credit-risk-ml)

> 🚧 **미착수** — 디렉터리·레포 준비만 완료

과제에서 제공한 코드로 만든 가상 금융 데이터(10,000건)를 가지고 규칙 기반 베이스라인과 ML 모델을 비교하고,
같은 데이터로 신용 점수(회귀)와 연체 위험(분류)을 함께 예측한다. 누수 방지 파이프라인, L1/L2 규제,
불균형 처리, 앙상블 튜닝까지 지도학습 파이프라인 전체를 다룬다.

- 과제 원문: 로컬 `../a5-1-credit-risk-ml.md`
- AI 심화 학습 · 머신러닝 · 80시간 · 필수 · 개인
- Python 3.10 이상 · `requirements.txt` 필수
- **A5-2 의 선행 미션** — A5-2 가 이 미션의 `finance_data.csv` 와 학습한 분류 모델을 그대로 쓴다

## 설치 및 실행

```bash
uv venv --python 3.12 .venv && source .venv/bin/activate
uv pip install -r requirements.txt   # uv 가 없으면 python -m venv .venv 후 pip install -r requirements.txt
```

진입점은 착수 때 정한다.

## 데이터 (과제 §4-1·§7)

- 과제의 데이터 생성 코드를 `data_gen.py` 로 저장·실행해 `finance_data.csv` 를 만든다 — **임의 수정·외부 데이터 금지**
- `*.csv` 는 `.gitignore` 로 막혀 있다 (과제 §4-1 명시)

## 라이브러리 제약 (과제 §7)

| 구분 | 내용 |
|---|---|
| 필수 | Scikit-learn, Pandas, NumPy, Matplotlib/Seaborn 만 |
| 선택 | imbalanced-learn(SMOTE), XGBoost — 쓰면 `requirements.txt` 에 버전 명시 |
| 금지 | PyTorch·TensorFlow |
| 형상 관리 | 기능 단위(전처리·모델링·문서화)로 커밋 로그를 남긴다 |

> ⚠️ A5-2 는 XGBoost·LightGBM 을 **금지**한다(Scikit-learn 내장 모델만). 앙상블을 Random Forest 로 하면
> A5-2 에서 이 모델을 그대로 SHAP 해석에 이어 쓸 수 있다.

## 제출물 체크리스트

- [ ] 규칙 기반 베이스라인 — if-else 규칙 5개 이상, Accuracy·Precision·Recall·F1
- [ ] 파이프라인 — `Pipeline`/`ColumnTransformer`, 수치형 대치→스케일링·범주형 인코딩, fit 은 Train 에서만
- [ ] 분할·재현성 — 8:2 (stratified 권장), `random_state=42`, 5-fold CV 권장
- [ ] 회귀 — Ridge·Lasso, Alpha 0.01·0.1·1·10·100 계수 변화 그래프, RMSE·MAE·R² 중 2개 이상
- [ ] 분류 — `class_weight='balanced'` 또는 SMOTE, Confusion Matrix, ROC-AUC 곡선 + AUC 값
- [ ] 앙상블 — Random Forest 또는 XGBoost + GridSearchCV (조합 100개 이하 권장), (권장) 특징 중요도 + 해석 3줄
- [ ] README — 개요·실행 방법·베이스라인 vs ML 성능 비교표 (Accuracy·F1·AUC)
- [ ] `requirements.txt`

## 보너스

- [ ] Custom Transformer (`BaseEstimator` 상속 파생변수 생성기)
- [ ] 모듈화 (노트북 → `.py` 스크립트)
- [ ] Learning Curve (데이터 크기별 Train/Validation 성능)
