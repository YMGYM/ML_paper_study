# AAAI 2021 Meta Learning Tutorial - Meta learning

본 파일은 [링크](https://sites.google.com/mit.edu/aaai2021metalearningtutorial/home) 의 영상 내용을 정리해 둔 파일입니다.

개인 공부의 노트 필기용도로 작업했습니다.



## Meta Learning

- 사람과 비슷한 학습 방법
- 지난 학습들에 기반해서 bias를 학습 (inductive bias)
- 다음과 갈은 구조
  - 아키텍처, 파이프라인
  - 학습 알고리즘
  - 학습 환경



## 학습방법



### bilevel optimization

- 특정 작업에 대해 적합한 작업 파라미터를 찾는 것.
- 파라미터 집합 중 특정 파라미터를 꺼내오는 느낌



### black-box models

- 작업별로 숨겨진 임베딩값 $theta$를 전달해서 예측
- 메타 학습기의 파라미터를 알 수가 없음(?)
- 작업별로 문제 $D_{test}$가 주어짐



## Taxonomy

- 메타러닝을 통해서 시작지점을 가깝게 하거나 (Gradient based Method)
- 학습 자체를 더 빨리 할 수 있게 할 수 있다.
- 메타 파라미터, 메타 옵티마이저, 메타 목적함수도 많은 종류가 있다.



### Gradient Based Method

- pretrain 느낌으로 사용한다.
- 파라미터를 Fine-Tuning 해서 사용한다.
- Model Agnostic meta-learning(MAML) : Task 별로 그래디언트의 방향의 합으로 학습을 진행한다.
- Scalability, Generalizability를 가진다.



### Baysian Meta Learning

- 작업 분포의 불확실성을 해소하기 위함
- x, y값이 발생할 때 결과값/파라미터 가 나올 확률로 접근한다.
- Fully Bayesian meta-learning 방법도 존재



## Meta - learning optimizers

- 우리 뇌는 역전파를 수행하지 않는다.
- 학습 방향에 신경망을 넣어서 진행하는 방법이 있음.
- 학습률을 유동적으로 변경하는 방법도 메타 러닝의 방법
- 다양한 목적에 맞는 옵티마이저 변경 방법이 입다.



## Metric Learning

- 파라미터의 임베딩을 찾는다.
- 임베딩 된 벡터끼리 거리 계산을 쉽게 하기 위해서이다.
- prototypical networks  : 각각의 데이터포인트에서의 $f_{\theta}$ 의 임베딩
- Relation networks..



## Black-box model for meta-RL

- RL에도 사용할 수 있으며,
- 짧은 작업에도 효과가 있었다.
- longer-horizon은 여전히 문제



## Training Task Acquisition

- 데이터가 가지는 학습 제약조건을 이해(?)
- 더 좋은 학습 작업=> 더 많은 상황 학습 가능



## Generative Teaching Network

- 현존하는 데이터에 기반해 더 효과적인 학습을 위한 데이터셋 생성
- 제너레이터를 메타러닝 함.

