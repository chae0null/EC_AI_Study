# EC AI Study

고객의 과거 금융 이용 정보로 다음 기간의 채무불이행(연체) 여부를 예측하며 머신러닝의 기본 흐름을 익히는 스터디입니다. 교육용으로 수정된 데이터이며 실제 개인의 금융 기록으로 해석하지 않습니다.

## 데이터

`data/dataset.zip`에는 다음 세 파일만 들어 있습니다.

- `train.csv`: 학습 데이터 21,009행. 입력 변수와 정답 `target`을 포함합니다.
- `test.csv`: 예측할 데이터 8,991행. 정답은 없습니다.
- `sample_submission.csv`: 제출 형식 예시. 0으로 채워진 값은 정답이 아닙니다.

`id`는 행 식별자이며 학습에서 제외합니다. 입력은 신용 한도, 나이, 교육·혼인 구분, 과거 구간별 지연·청구·납부 정보입니다. 빈 값은 결측치입니다.

출처: I-Cheng Yeh (2009), [Default of Credit Card Clients](https://doi.org/10.24432/C55S3H), UCI Machine Learning Repository. [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)에 따라 제공하며, 교육 목적으로 식별자·변수 표현을 변경하고 요약·결측치 추가·학습/평가 분할을 적용했습니다.

## Target

- `0`: 다음 기간 채무불이행이 관측되지 않음
- `1`: 다음 기간 채무불이행 발생

## 평가 방식

**점수 = 100 × Balanced Accuracy = 50 × (양성 재현율 + 음성 재현율)**

0~100점이며 높을수록 좋습니다. 모든 행을 같은 값으로 예측하면 50점입니다. 제출값은 확률이 아닌 정수 0 또는 1입니다. Baseline의 validation 점수는 train의 일부로 계산하므로 최종 test 점수와 다를 수 있습니다.

## Baseline 실행

Python 3.10 이상을 권장합니다. 저장소를 내려받고 루트 폴더에서 실행하세요.

```bash
python -m pip install -r baseline/requirements.txt
python -m notebook baseline/baseline.ipynb
```

노트북에서 셀을 위에서부터 모두 실행하면 루트에 `submission.csv`가 생성됩니다. ZIP은 자동으로 읽습니다. 기본 전처리와 로지스틱 회귀 모델 하나를 사용합니다.

## 제출 파일 형식

`sample_submission.csv`와 동일한 `id,target` 두 열을 사용합니다. 모든 test ID를 정확히 한 번 포함하고, `target`에는 정수 0 또는 1을 입력합니다. CSV 저장 시 DataFrame 인덱스는 포함하지 않습니다.

## 스터디 규칙

- 외부 원본 데이터에서 test 정답을 찾아오거나, 원본과 test 행을 매칭해 정답을 복원하는 행위는 금지합니다.
- AI 사용은 가능하지만 사용한 방법과 결과를 이해하고 설명할 수 있어야 합니다.

이 규칙은 스터디 참여·평가 규칙이며 데이터 라이선스의 이용 권리를 제한하는 추가 저작권 조건이 아닙니다.
