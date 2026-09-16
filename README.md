# EC AI Study

표 형태의 데이터로 이진 분류 모델을 만들고, 같은 Baseline과 검증 기준에서 매주 직접 개선하는 8주 스터디입니다. 교육용으로 수정된 데이터이며 실제 개인의 금융 기록으로 해석하지 않습니다.

## 참가자 자료

```text
EC_AI_Study-main/
├── README.md
├── baseline/
│   ├── baseline.ipynb
│   └── requirements.txt
└── data/
    └── dataset.zip
```

`data/dataset.zip`에는 다음 네 파일이 들어 있습니다. ZIP은 Baseline이 직접 읽으므로 압축을 풀 필요가 없습니다.

- `train.csv`: 학습 데이터 21,009행. 입력 변수와 정답 `target`을 포함합니다.
- `test.csv`: 예측할 데이터 8,991행. 정답은 없습니다.
- `sample_submission.csv`: `id,prediction` 제출 형식 예시입니다. 0으로 채워진 값은 정답이 아닙니다.
- `validation_folds.csv`: 모든 참가자가 공통으로 사용하는 공식 검증 분할입니다.

`id`는 행 식별자이며 모델 입력에서 제외합니다. 입력은 신용 한도, 나이, 교육·혼인 구분, 과거 구간별 지연·청구·납부 정보입니다. 빈 값은 결측치입니다.

## Target과 평가 방식

- `target=0`: 다음 기간 채무불이행이 관측되지 않음
- `target=1`: 다음 기간 채무불이행 발생

점수는 `100 × Balanced Accuracy`입니다. 0과 1 각각의 재현율을 동일한 비중으로 평가하며 높을수록 좋습니다. 모든 행을 같은 값으로 예측하면 50점입니다.

## 공식 검증 분할

Baseline은 `validation_folds.csv`를 자동으로 읽습니다.

- fold 0: 공통 검증 데이터
- fold 1~4: 학습 데이터
- fold 번호는 모델 입력에 사용하지 않습니다.
- 데이터와 분할은 행 순서가 아니라 `id`로 연결합니다.

같은 검증 분할을 사용해야 Baseline과 이후 실험의 점수를 공정하게 비교할 수 있습니다. 웹 점수만 보고 설정을 반복해서 바꾸지 말고 내부 검증 결과와 실험 기록을 함께 확인하세요.

## Baseline 실행

Python 3.10 이상을 권장합니다. 저장소를 내려받고 최상위 폴더에서 실행합니다.

```bash
python -m pip install -r baseline/requirements.txt
python -m notebook
```

Jupyter에서 `baseline/baseline.ipynb`를 열고 위에서부터 모두 실행합니다. 기본 전처리와 로지스틱 회귀를 사용해 공식 검증 점수를 계산한 뒤 저장소 최상위에 `submission.csv`를 생성합니다.

## 제출 파일

제출 파일은 다음 조건을 만족해야 합니다.

- 파일 이름: `submission.csv`
- 열: `id,prediction`
- 모든 test ID를 정확히 한 번 포함
- `prediction`은 정수 0 또는 1
- DataFrame 인덱스를 저장하지 않은 UTF-8 CSV

제출 웹: https://ec-ai-study-chae0nulls-projects.vercel.app

## 스터디 진행 원칙

- 제공된 Baseline을 공통 출발점으로 사용합니다.
- 주차별 완성 코드는 제공하지 않습니다. Baseline을 복사해 직접 실험합니다.
- 한 번에 바꾼 내용, 검증 점수, 웹 점수와 결과 해석을 기록합니다.
- 특정 점수나 매주 점수 상승보다 변경 이유와 결과를 설명하는 것이 중요합니다.
- 외부 원본 데이터에서 test 정답을 찾거나 test 행을 매칭해 정답을 복원하는 행위는 금지합니다.

## 출처

I-Cheng Yeh (2009), [Default of Credit Card Clients](https://doi.org/10.24432/C55S3H), UCI Machine Learning Repository. [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)에 따라 제공하며 교육 목적으로 식별자·변수 표현 변경, 기간 요약, 결측치 추가와 학습·평가 분할을 적용했습니다.
