# Understanding Black-box Predictions via Influence Functions - Pang Wei Koh, Percy Liang

본 자료는 빅데이터 동아리 Tobigs 12기 안민준의 XAI 심화세미나 활동으로 작성되었습니다.

본 자료는 동명의 [논문](https://arxiv.org/abs/1703.04730) 의 내용을 정리하고 이해하기 위해 작성되었습니다.

출처가 적혀 있지 않은 이미지는 모두 논문의 자료입니다.

## Abstract

- 블랙박스 형태의 모델을 해석하기 위해 본 논문은 influence function을 사용했다.
- 모델의 예측을 트레이싱해서 가장 영향을 주는 포인트를 가지는 부분을 찾아낸다.
- Influence function은 선형 모델 뿐 아니라 다양한 형태의 모델에도 유효한 것을 확인했다.



## Introduction

- 머신 러닝 시스템에서 왜 모델이 이런 결정을 내렸는지가 중요한 결정이었다.

- 모델을 이해하는 것은 성능을 향상하고, 새로운 연구 분야가 나오고, end-user에게 모델이 예측하는 데 영향을 준 부분을 표시할 수 있다.

- 하지만 최근 좋은 성능을 보이는 모델은 복잡하고, 블랙 박스 모델이기 때문에 설명이 어렵다.

- 이 논문에서는 모델의 예측값을 추적해서 학습 알고리즘을 통해 학습 데이터로 넘어가는 방법에 의문점을 제시했다.

- 그 대체제로 influence functions을 제시했다.

- 이는 학습 포인트를 미세하게 변경했을 때 모델 파라미터가 어떻게 변하는지를 보여준다.

- 그럼에도 불구하고 influence function은 많이 사용되지 않았다. 그 이유로는 모델의 복잡한 이계미분이나 convexity를 필요로 하기 때문이다.

- 본 논문은 이를 second-order optimization techniques를 사용해 해결했다.

- 또한 influence function은 다양한 태스크에도 적용될 수 있음을 보였다.

  

## Approach

### 2.1 Upweighting a training point

- 본 논문은 트레이닝 포인트 $z$의 변화를 $ \theta_{-z} - \hat{\theta} $으로 표기한다.
- -모델은 복잡한 계산을 통해(미분..) 이를 $ \frac{1}{n}I_{up, params}(x) $ 로 근사했다.
- z의 upweighting이 $\hat\theta$ 에 미치는 영향력을 측정하기 위해선 chain rule을 사용해 closed-form 표현으로 변환할 수 있다.



### 2.2 Perturbing a training input

- $z$ 가 $z_\delta$ 로 변화할 때, $\theta_{z\delta -z}$ 를 empirical risk minimizer로 정의한다.
- 2.1에서 측정한 식을 사용하면  $\theta_{z\delta -z} = \frac{1}{n}(I_{up, params}(z\theta) - I_{up, params}(z))$ 로 근사가 가능하다.
- 이는 $\theta_{z\delta -z} - \hat\theta \approx -\frac{1}{n}H^{-1}_{\hat\theta}[\nabla_x\nabla_\theta L(z, \hat\theta)]\delta $ 로 다시 근사가 가능하다.

### 2.3 Relation to Euclidean distance

- 테스트 포인트와 가장 관련 깊은 트레이닝 포인트를 찾기 위해 nearest neighbors를 사용하는것이 가장 흔하다.
- 로지스틱 회귀 모델에 대해서 $I_{up, loss}(z, z_{test})$를 계산했다.
- 그 결과 두 가지를 발견했는데, $\sigma(-y\theta^Tx) $ 가 더 중요한 부분에 대해 손실을 크게 준다는 사실과, $\nabla_\theta L(z, \hat\theta)$가 더 적게 변화하는 쪽을 가리킨다는 것이다. (결과값을 크게 변화시키지 않기 때문이다)



## Efficiently calculating influence

-  $I_{up, loss}(z, z_{test})$ 를 계산하는 데에는 두 가지 문제점이 있다.
  1. empirical risk의 헤이시안의 역행렬을 계산해야 하는데 $O(np^2 + p^3)$ 이라는 매우 큰 연산량이 들어간다.
  2.  $I_{up, loss}(z, z_{test})$ 를 모든 $z_i$ 에 대해서 계산해야한다.
- 이 문제를 해결하기 위해 논문에서는 Hessian-vector-products (HVP) 를 추정해서 대입한다.
- $s_{test} = H^{-1}_{\hat\theta}\nabla_\theta L(z_{test},\hat\theta) $ 으로 놓고, $I_{up, loss}(z, z_{test}) = -s_{test} \cdot \nabla_{\theta} L(z, \hat\theta)$ 를 계산한다.
- 이 방법의 계산복잡도는 $O(p)$ 이다.
- 이 문제를 해결하기 위해서 `Conjugate gradient(CG)` 방법과, `Stocastic estimation` 방법을 사용했다.



## Validation and extensions

- influence functions을 불러오는 것은 점근적 접근이며 다음 두 가지 가정을 필요로 한다.
  - $\hat\theta$ 는 empirical risk를 최소화한다.
  - empirical risk 는 이계미분이 가능하며 엄격하게 convex하다.
- MNIST 데이터에 대해 적용해 본 결과 큰 차이가 없이 적용되었다.
- 본 논문의 식이 convex하지 않은 곳에도 적용되는 것을 보였다(?)
- 또한 손실 함수가 미분 불가능해도 적용이 가능하다.



## Use Cases of influence 

- 주어진 예측에 대해 '책임이 있는' 학습 지점을 말하는 것은 모델이 학습 데이터의 어느 지점에 의존하고 해석되는지를 알 수 있게 한다.

### Understanding model behavior

- Inception 모델과 RBF SVM모델로 인식해본 결과, SVM은 픽셀 간 거리가 비슷하면 Loss가 적게 나오고, Inception 모델은 객체의 특징이 비슷한 경우 적게 나오는 것을 확인할 수 있었다.
- 반면 SVM은 강아지 클래스의 이미지들이 물고기라고 인식하는 데 방해가 된 반면 Inception은 요인이 섞여 있는 것을 확인할 수 있었다.



### Adversarial training examples

- $I_{up, loss}(z, z_{test})$ 을 사용하면 적대적 이미지를 만들 수 있다. (가장 Loss가 증가하는 방향을 알려 주기 때문)
- 학습 데이터에 $I_{up, loss}(z, z_{test})$ 값을 $\alpha$ 만큼 곱해서 더해주는 것 만으로 적대적 이미지를 만들 수 있다.
- 이 방법으로 학습 모델을 교란시킬 수 있었다.
- 본 모델은 이를 통해 세 가지 점을 발견했다
  - 입력 픽셀값이 매우 조금 변하더라도 output값은 매우 크게 변화했다.
  - 적은 변화량을 가지는 방향으로 모델을 교란하면 모델이 과적합을 일으킬 수 있다.
  - 모호하게 레이블링 된 이미지가 공격에 취약하다.
- $I_{pert, loss}(z, z_{test})$ 를 사용해 모델 개발자에게 얼마나 모델이 취약한지 정량적으로 나타낼 수 있을 것이다.



### debugging domain mismatch

- domain mismatch (학습 데이터와 평가 데이터의 분포가 맞지 않는 것)을 구분할 수 있다.
- Influence function 에러에 가장 영향을 주는 학습 예시를 보여 준다.
- 의료 데이터로 확인해  본 결과, 치우치지 않은 데이터에 큰 주목을 하는 것을 확인할 수 있었다.



### Fixing mislabeled examples

- influence function은 인간 전문가가 정말로 중요한 데이터에만 집중할 수 있게 도와준다.
- 가장 모델에 영향을 춘 트레이닝 포인트를 마킹하는 아이디어
- 각 데이터에 대해 $I_{up, loss}(z_i, z_i) $ 를 구하고, 오류가 있어 보이는 경우 제거하고 진행했다.
- 데이터 정제를 할 수록 모델의 정확도가 향상되는 것을 확인했다.



## Discussion

- influence function은 기본적인 아이디어임에도 불구하고, 다양한 부분에서 사용될 수 있다.
- influence function은 upweight point 를 극미량 변경했을 때 결과값의 변화를 주목했다.
- 모델을 크게 변화시키지 않으면서 전반적인 글로벌 영역에 대한 질문의 답을 구할 수 있다.
- 연구진들은 본 방법이 툴킷 개발, 이해, 진단 등 다양한 분야에 적용될 수 있기를 기대한다.



