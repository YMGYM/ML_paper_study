# Grad-CAM: Visual Explanations from Deep Networks via Gradient-based Localization



본 파일은은 동명의 [논문](https://arxiv.org/abs/1610.02391) 의 내용을 정리하고 이해하기 위해 작성되었습니다.



##  Abstract

- 본 논문은 CNN 기반 모델의 결정을 시각적으로 설명해주는 방법을 제안했다.
- Gradient-weighted Class Activation Mapping (Grad-CAM) 은 마지막 convolutional 층의 그래디언트를 사용해 중요한 정보를 지목하는 coarse localization map을 보여준다.
- Grad-CAM은 많은 종류의 CNN 모델에 적용할 수 있다.
- 본 논문은 Grad-CAM과 고해상도 클래스 구분 시각화 툴과 결합해 시각화했다.
- 이 시각화 방법은 다음 방법을 제공한다.
  - 실패한 모델의 인사이트를 얻을 수 있다.
  - ILSVRC-15 태스크에서 기존 방법을 뛰어넘었다.
  - 적대적 perturbations에 대해 강건하다.
  - 기존 모델에 대해 더 많은 신뢰감을 제공한다.
  - 데이터셋의 편향을 파악함으로서 모델 일반화를 달성할 수 있다.





## Introduction

- CNN은 컴퓨터 비전 환경에서 놀라운 성과를 이륙했다.
- 그럼에도 불구하고, 투명성과 individually intuitive 한 components 가 해석하기 어렵게 하고 있다.
- 또한 이 모델델은 종종 설명이나 경고 없이 오답을 내기도 한다.
- 따라서 우리는 '투명한' 모델을 내야 할 필요가 있다.
  - AI가 인간보다 부족한 경우, 실패한 상황을 밝혀야 한다.
  - AI와 인간이 동등한 경우, 신뢰와 자신감을 줄 필요가 있다.
  - AI가 인간을 앞선 경우 Machine Teaching 에 집중해야 한다.
- 성능-해석가능성 trade-off에 의해 우리는 딥러닝에서 많은 해석가능성을 포기했다.
- 본 논문은 현존하는 SOTA논문을 구조를 변경하지 않고 해석가능하게 해서 전 trade-off를 해결했다.
- Zhou 등은 Class-Activation-Mapping 을 사용해서 완전연결계층이 아닌 CNN을 해석가능하게 했는데, 본 논문은 이를 일반화해서 모든 논문에 적용할 수 있게 했다.



### What makes a good visual explanation?

클래스를 구분하는 모델에서 모델은 - class discriminative 하고, high-resolution 이어야 한다.

GAM과 Grad-CAM은 분류 클래스의 영역을 하이라이팅 함으로서 구분할 수 있게 된다.



### 연구 요약

1. Grad-CAM을 제안했다.
2. Grad-CAM을 현재 가장 좋은 클래스 구분, 캡셔닝, VQA모델에 적용했다.
3. Grad-CAM 시각화가 모델 실패를 진단하는데 도움이 되는지 개념적으로 증명한다.
4. ResNet에 대해 Grad-CAM 시각화를 진행했다.
5. Grad-CAM의 뉴런 중요도와 이름, 텍스트화된 중요성을 보여준다.
6. Human studies를 진행해서 훈련되지 않은 사람을 도와줄 수도 있다.



## Related Work

본 논문은 세 가지 연구분야를 끌고 가고 있다.

### Visualizing CNNs

다양한 방법들이 중요한 픽셀을 하이라이팅함으로서 CNN예측을 시각화했다.

본 논문의 시각화 방법은 network unit을 가장 크게 activate한 것과 이미지를 합성하는 방법이다.



### Accessing Model Trust

이 방법은 모델이 평가하고, 신뢰감을 주는 데 중요한 역할을 할 것을 보인다.



### Aligning Gradient-based Importances

후속 논문등에서 Gradient-based한 뉴런 중요도를 사용한다.



### Weekly-supervised localization

CAM을 사용해 localization을 수행할 수 있다. (소수의 경우에서만 적용이 가능하다)

Grad-CAM은 fully connected layer가 있는 네트워크에도 적용이 된다. 또한 계산 비용이 저렴하다는 장점이 있다.





## Grad-CAM

- 합성곱 신경망은 주로 지역적인 정보를 담고 있다. 따라서 본 연구는 마지막 레이어에 가장 많은 정보가 담겨 있을 것이라고 생각했다.
- Grad-CAM은 마지막 합성곱 층으로 들어가는 그래디언트 정보를 사용한다.
- 본 기술은 심층 신경망의 어느 층에서도 적용될 수 있지만, 본 연구는 output 층에만 초점을 맞출 것이다.



1. 클래스 $c$에 대해서 점수 $y^c$의 그래디언트를 계산한다. 이 때, 각 convolutional layer 의 활성화 값 $A^k$ 에 대해서 구한다.
2. 이 값을 GAP를 통과시켜 $a^c_k$를 구한다.
3. $a^c_k$ 은 partial linearization 이라고 부르며, 타겟 클래스 $c$에 대한 피처 맵 $k$의 중요성을 나타낸다.
4. 이 값에 ReLU를 써서 양수만 남긴다.
