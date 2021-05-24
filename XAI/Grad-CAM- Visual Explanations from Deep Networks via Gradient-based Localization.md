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

4. 이 값에 ReLU를 써서 양수만 남긴다.(음수 값에는 관심을 가지지 않습니다.)

   

### Grad-CAM generalizes CAM

- 이 장에서는 Grad-CAM의 수식적 표현을 사용해 CAM을 일반화할 수 있음을 보였다.
- 이렇게 일반화를 수행하면 CNN 기반 모델의 시각적 표현을 가능하게 한다.



### Guided Grad-CAM

- Grad-CAM이 클래스 결정적이고 관련있는 이미지 지역을 특정할 수 있지만, 특정 픽셀에 대한 디테일을 표시하는 능력이 떨어진다.
- Guided Backpropagation은 음수값이 제거된 이미지 그래디언트를 시각화한다.
- 본 논문은 Guided Backpropagation과 Grad-CAM시각화를 원소별 곱을 통해 시각화했다.
- 이를 통해 클래스 별 특징 (예를 들어, 호랑이에서 줄무늬와 같은 특징)을 잘 추출해 낼 수 있었다.
- Deconvolution 을 원소별 곱하는 것도 비슷한 성능이 있었지만, 조금 노이즈가 있는 모습이 보였다.



### Counterfactual Explanations

- Grad-CAM을 살짝 수정하므로서 네트워크의 예측을 수정하게 만드는 지역을 하이라이팅 할 수 있다.
- 이 지역들을 제거하면 모델의 예측이 더 강건해졌다. 이를 counterfactual explantions 라고 부르기로 했다.
- 특정 클래스의 그래디언트에 음수 값을 곱해서 가중합을 구하는 방법을 사용했다.
- 강아지 클래스의 counterfactual explantions는 고양이에 가 있는 형태이다.



## Evaluating Localization Ability of Grad-CAM

### Weakly-supervised Localization

- 이미지 분류 문제 (ImageNet)에서 접근했다.
- Grad-CAM영역을 이진화 하는 방법으로 바운딩 박스를 그릴 수 있다.
- 학습할 때 정답을 주지 않는 방법이므로 준지도학습 문제로 볼 수 있다.
- CAM이나 c-MWP보다 일부에서 좋은 성능을 보였다. (항상 우수했던 것은 아니다.)



### Weakly-supervised Segmentation

- Kolesnikov 의 준지도 segmentation방법을 사용했다.
  - Localization 시드를 생성한다.
  - 시드를 적합한 사이즈로 확대한다.
  - 부정확한 경계를 처리한다.



### Pointing Game

- Zhang의 Pointing Game 실험은 목표를 locating하는 방법의 차이를 평가한다.
- 히트맵이 주어진 label에 얼마나 걸쳤는지를 판단해서 Hit 와 miss를 판단한다.
- Precision 뿐 아니라 Recall까지 계산해서 파악했다.
- 정답에 없는 카테고리를 성공적으로 reject했으면 hit로 판단했다.



## Evaluating Visualizations

- 해석가능성과 신뢰도 tradeoff를 연구했다.
- Grad-CAM이 기존 기술보다 더 class discriminative한지..



### Evaluating Class Discrimination

- Grad-CAM이 클래스 간 구분을 잘 하는지 측정하기 위해 PASCAL VOC 2007 데이터를 사용했다.
- 43명의 AMT에게 주어진 두개의 카테고리가 이미지에 잘 나타나는지를 묻는 방법으로 측정했다
- Guided Grad-CAM이 가장 좋은 성과를 보였다.



### Evaluating Trust

- 두개의 예측값을 보고 어떤 것이 더 신뢰할 수 있는지 측정했다.
- 54의 AMT가 5점 척도로 평가를 진행했다.
- Guided Grad-CAM이 1.27점으로 신뢰도가 있음을 확인했다.



### Faithfulness vs Interpretability

- 일반적으로 더 정확한 모델은 덜 해석가능하다.
- 본 논문은 Grad-CAM이 얼마나 신뢰가능한지 측정했다.
- locally accurate 하면, 더 신뢰도가 있는 것으로 생각하고 측정했다.
- occlusion 방법을 사용했는데, 마스킹이 더 높은 intensity 를 주었다.
- 이로서 Grad-CAM 이 더 신뢰도가 있음을 확인할 수 있었다.



## Diagnosing image classification CNNs with Grad-CAM

- Grad-CAM을 모델의 예측 실패를 분석하는데 사용했다.
- 적대적 노이즈의 영향을 보거나, 편향을 분석하고 제거하였다.



### Analyzing failure modes for VGG-16

- 잘못 예측된 경우의 Grad-CAM을 찍어 본 결과, 합리적인 설명가능성을 얻을 수 있었다.
- Guided Grad-CAM의 고해상도 특징 때문에 이익을 볼 수 있었다.



### Effect of adversarial noise on VGG-16

- Geedfellow 는 적대적 공격의 영향을 받을 수 있음을 보여 주었다.
- 적대적 공격으로 인해 잘못 예측된 결과는 배경에 하이라이팅 된 것을 확인할 수 있었다.



### Identifying bias in dataset

- 학습된 모델은 세상의 편견, 고정관념을 일반화할 수 없다.
- 의사 - 간호사 구분 모델을 만들어 학습시켰다
- 편향된 모델을 간호사와 의사의 차이를 얼굴, 헤어스타일을 통해 구분하려 했지만, 편향되지 않은 모델은 도구를 통해 구분하려 했다.



## Textual Explanations with Grad-CAM

- 뉴런에 설명 이름을 붙이고 이미지 활성도에 따라 뉴런의 결과를 출력했다.
- 상위에 표시된 이름에 맞게 히트맵이 잘 분포되었다.



## Grad-CAM for Image Captioning and VQA

- Grad-CAM을 이미지 캡셔닝과 질의응답에 적용했다.
- 두 작업 모두에서 해석가능한 시각적 표현을 제공할 수 있었다.



### Image Captioning

- 이미지 설명이 나타내는 부분에 잘 하이라이팅 된 모습을 보였다.
- Grad-CAM은 DenseCap모델이 설명하는 캡션을 잘 localize 할 수 있었다.



### Visual Question Answering

- 정답 클래스를 뽑고 Grad-CAM 시각화의 점수를 계산했다.
- 놀랍게도 직관적이고, 정보를 잘 전달했다.



## Conclusion

- Grad-CAM이라는 클래스를 구분하고, 지역구분을 할수있는 테크닉을 소개했다.
- 이는 고 해상도와, 클래스를 구분하는 설명 두 가지를 모두 얻을 수 있었다.
- 본 연구는 해석가능성과 신뢰성 영역에서 기존 방법보다 뛰어난 성과를 얻었다.
- Grad-CAM의 다양한 적용가능성을 실험했다.
- 앞으로 강화학습, 자연어 처리, 영상 처리 등에서도 다음과 같은 설명이 포함될 것이다.

