# CS 질문 답변 기록 3

## ML CS

, bias, k-mean, kin

- **인공지능, 머신러닝, 딥러닝 간 관계**
  - **AI > ML > DL**

#### AI

- 인공지능 (Artificial Inteligence), AI

#### ML

- **ML(Machine Learning)은 인공지능의 한 분야**로, **컴퓨터가 학습할 수 있도록 하는 알고리즘과 기술을 개발하는 분야**를 말한다. 
  - ex) 기계학습을 통해 수신한 이메일이 스팸인지 평범한 내용인지를 구분하는 훈련 
  - ML의 핵심은 표현(representation)과 일반화(generalization)에 있다.
    - 표현은 데이터의 평가이며, 일반화는 아직 알 수 없는 데이터에 대한 처리를 의미한다. 

#### Deep Learning

- 딥러닝 (Deep Learning), 심층학습이다. 
- 기계학습 알고리즘의 한 종류로 ML의 일종이라고 할 수 있다. 

#### Normalization

- 정규화 (Normalization) 는 모든 데이터 포인트가 동일한 정도의 스케일(중요도)로 반영되도록 해주는 것을 의미한다.
- **Data Normalization**
  - **데이터의 범위를 사용자가 원하는 범위로 제한하는 것**이다.
    - ex) 이미지를 가중치를 부여할 단위로 쪼갠 배열로 변환

#### classification vs regression 차이

- **classification** (식별)
  - **객체를 예측하는 것이 classification**이다.
  - **주어진 데이터를 정해진 카테고리에 따라 분류하는 문제**
    - **예 / 아니오 로 구분되는 문제를 식별하는 것은 Binary Classification**이라고 한다.
  - ex) 어떤 text를 입력했을 때, 그것이 어떤 class에 속하는지 예측하는 것
  - ex) 어떤 이미지를 촬영했을때 그 이미지가 어떤 속성을 가졌는지를 예측하는 것
- **Regression** (회귀)
  - **회귀 (Regression)은 예측값이 연속된 값인 문제들을 해결하는데 사용**한다. 
  - 연속된 값을 예측하는데, 주로 **어떤 패턴이나 트렌드, 경향을 예측할 때 사용**한다.
