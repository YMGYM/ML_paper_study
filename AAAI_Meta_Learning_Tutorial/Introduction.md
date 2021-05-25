# AAAI 2021 Meta Learning Tutorial - Introduction

본 파일은 [링크](https://sites.google.com/mit.edu/aaai2021metalearningtutorial/home) 의 영상 내용을 정리해 둔 파일입니다.

개인 공부의 노트 필기용도로 작업했습니다.



## Introduction

### 기계와 인간

- 기계는 specialist이다.
- 기계는 특정 작업에서 인간을 훨씬 능가할 수 있다(AlphaX 와 같은 경우..)
- 최근 GPT-3 와 같은 모델이 많은 파라미터를 자랑하지만, 인간보다 한참 적은 파라미터를 가진다.



### DARPA Programs

- D3M -> AutoML
- LwLL -> few shot learning 
- .. 등등 많은 일들이 있었다.



### 학습 알고리즘

- 우리는 input $x$ 를 함수 $f$에 넣고 output $y$ 를 얻는다.

- Supervised Learning에서는 예측값 ($y$) 를 테스트 데이터와 비교한다

- Transfer Learning에서는 작은 데이터를 가진 경우, base predictor를 만들어 다른 데이터로 학습하고 본래 (작았던) 데이터를 이에 맞춰 피팅하는 구조. => 스노우보드를 잘 타는 인간이 서핑이나, 스케이트보드를 잘 타는 것과 비슷하다.
- Meta Learning에서는 더 좁은 접근을 한다. Task(data split)에 대해서 트레이닝을 한다. 따라서 output도 Task (학습 알고리즘) 이다.



### Machine Learning System

- 예측기 (Predictor)는 머신러닝 시스템의 큰 부분을 차지한다.
- 머신 러닝 파이프라인 설명.
- 메타 러닝은 데이터 뿐 아니라, 솔루션에 집중한다.



### AutoML

- input이 데이터셋이 아니라, 데이터셋이 분류, 회귀 등 다양한 task에 해당하는 데이터가 들어간다.



### Learning to Learn

- 기존 머신러닝은 파라미터 M만 배운다면,
- LtL 방법은 M과 파라미터도 배운다.



### Learning Task

- 역전파 알고리즘과 같이

- 학습 알고리즘이 역으로 task를 수행하도록 역 화살표를 가한다.

- 이를 통해 작업의 일반화를 수행한다.

- 이 외에도 게임 이론을 적용해, 보상을 최대화하는 것을 적용할 수 있다.

  