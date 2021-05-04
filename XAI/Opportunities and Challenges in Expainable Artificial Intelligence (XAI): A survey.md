# Opportunities and Challenges in Expainable Artificial Intelligence (XAI): A survey

by Arun Das and Paul Rad

본 게시글은 동명의 논문의 내용을 정리하고, XAI를 이해하는 것을 목표로 한다.

논문의 링크는 https://arxiv.org/abs/2006.11371 이다.

본 게시글의 출처가 적혀 있지 않은 이미지는 원 논문에서 가져왔다.



## Abstract

- 인공 신경망 기술은 다양한 분야에 사용되고 있다.
- 하지만 인공 신경망의 블랙박스 특징 때문에 사용이 제한되는 분야도 발생하고 있다.
- 설명가능 인공지능(XAI) 기술은 인공지능의 결정에 대해 해석적, 직관적, 이해가능한 설명을 제공한다.
- 본 논문은 XAI를 scope, methodology, explanation level에 따라 분류하여 설명했다.
- XAI 연구분야에서 2007년 부터 2020년까지 역사적 타임라인을 보여 준다.
- 8개의 XAI알고리즘의 explanation maps를 평가하며, 한계점과 미래 발전 방향에 대해 논할 것이다.



## Introduction

- DNNs(Deep Neural Networks) 은 많은 파라미터들을 가지고 있기 때문에 점점 이해하기 어렵다.
- DNNs의 결정을 해석하는 것은 관련 지식이 필요하다.
- 이런 지식들은 AI 비전문가나, 최종사용자에게는 필요가 없는 지식이다. (정확한 결과를 저 필요로 하는 계층)



XAI를 연구하는 이유는 다음 이유들을 들 수 있다.

- 인간의 호기심
- 더 좋은 학습을 유도하기 위해서
- 결정에 대한 투명성, 신뢰성, 공정성 확보



하지만, 해석가능/설명가능한 AI에 대한 용어가 종종 포괄적이어서 오해를 일으킬 수 있다.



의사결정 트리, rule-based 모델 같은 경우는 기본적으로 해석이 가능하지만 딥러닝 기반 모델에 비해 정확성이 떨어지는 문제도 발생한다.

(Interpertablility-versus-Accuracy trade-off)

API기반의 인공지능 서비스는 인공지능 모델의 출력값만 반환하며 상대적으로 '블랙박스'의 성향이 더 강하다.



- 본 논문은 설명가능/해석가능 알고리즘을 시간 순서대로 파악할 것이다.

- 또한 알고리즘이 주로 분류되는 3가지 형태로 분류할 것이다.

- 이 알고리즘이 한계와 발전 방향을 평가할 것이다.



본 논문을 요약하면 다음과 같은 형태이다.

1. XAI를 세가지 카테고리로 분류해 명확성과 접근성을 올렸다.
2. XAI 연구의 핵심 수학적 모델을 요약하고 분류할 것이다.
3. 8개의 XAI알고리즘의 explanation maps를 생성하고 분석해 볼 것이다.



본 논문은 2007년부터 2020년까지 출판된 연구를 기반으로 했다.

Google Scholar, ACM Digital Library, IEEEXplore, ScienceDirect, Spinger, arXiv 등에서 논문을 참고하였다.



## Taxonomies and Organization

### Taxonomies

본 논문은 XAI기법을 다음과 같이 분류했다.

![survey_1](/Users/jun/My Works/paperStudy/ML_paper_study/XAI/Images/survey_1.png)



1. Scope

   - 데이터에 대한 설명 범위

   - Local : 전체 데이터 X 안의 단일 데이터 x에 대해서만 설명이 가능하도록 설계된 방법
   - Global : 모델 전체에 대해서 인사이트를 제공한다. 입력 전체의 배열에 대해 설명을 제공한다.

2. Methodology 

   - 설명가능 모델 내부에 존재하는 핵심 알고리즘적 콘셉트
   - Backpropagation-based  : 역전파 과정중에 편미분을 활용하여 설명을 얻는다.
   - Perturbation-based : 오클루전, 부분적으로 제거된 피쳐, 마스킹, 조건부 샘플링 등의 방법을 사용한다. 역전파가 필요 없다는 장점이 있다.

3. Usage

   - 특정 모델에만 적용될 수 있는지, 외부 알고리즘에도 적용될 수 있는지를 나타낸다.
   - Model-intrinsic : 솔루션이 특정 모델 구조에 종속되어 있다.
   - Post-hoc(model-agnostic) : 이미 잘 예측중인 인공지능 모델에 대입될 수 있는 방법이다. 다양한 형태의 데이터에도 적용이 가능하다.



### 평가방법의 변화

XAI알고리즘의 정량적, 정성적 평가를 위해 몇가지 평가 알고리즘을 제안했다.

투명성, 신뢰성, 편향 이해 부분에서 바람직한 제약조건을 제시했다.

이 평가방법은 아직 완벽하지는 않지만, 미래에 많은 발전가능성을 가지고 있다.



### 오픈 소스

깃허브 플랫폼의 오픈소스 패키지를 제공한다.

많은 사용자 지원과 알고리즘이 포함된 패키지들을 선택했다.



### 수식 표기

본 논문에서 제안된 모든 수식은 다음 표현 방법을 따를 것이다.

![survey_2](/Users/jun/My Works/paperStudy/ML_paper_study/XAI/Images/survey_2.png)



## Definitions and Preliminaries

본 논문에서는 XAI의 정의를 다음과 같이 설정했다.

> AI 시스템의 신뢰성과 투명성을 향상시키기 위해 설계된 일련의 기술과 알고리즘



다양한 DNNs을 설명하기 위한 접근이 많은 연구에서 제안된 바 있다.

![survey_3](/Users/jun/My Works/paperStudy/ML_paper_study/XAI/Images/survey_3.png)

논문에서 DNNs를 설명하기 위해 설명한 그림이다.

하나의 x (메타데이터가 따로 제공되지 않는다)가 딥러닝 모델 f를 통과하여 $\bar{y}$ 라는 결과를 산출한다.

전체 데이터 안의 단일 데이터가 딥러닝 모델을 통과하여 특정 클래스의 원소를 반환한다.



아래는 이 논문의 명확한 정의를 위해 용어를 정의해 둔 것이다.

 ### Interpretability

> 해석가능성(Interpretability)이란 특정 알고리즘이 어떻게 동작하는지 이해할 수 있도록 하는 충분한 표현을 제공하는 알고리즘의 기능이나 특징이다.

해석가능한 도메인은 이미지나 텍스트 등 사람이 이해할 수 있는 도메인들을 포함한다.



### Interpretation

> 해석(Interpretation)이란 복잡한 도메인의 단순화된 표현이다. 예를 들어 ML모델의 결과물이나, 사람이 이해가능/합리적인 의미있는 콘셉트이다.

단순히 rule-based 모델의 예측 결과물은  rule-set을 통해 쉽게 해석될 수 있다.

CNN 네트워크 등은 의사 결정에 영향을 미친 부분을 추론할 수 있다.

### Explanation

> 설명(Explanation) 이란 ML모델이나 외부 알고리즘에 의해 생성된 추가적인 메타 정보이다. 이는 피처 중요도나, 입력 데이터와 출력 데이터의 관련성을 묘사한다.

예를 들어 이미지에 대해서는 explanation map이 생성될 수 있는데, 입력 이미지와 같은 크기의 픽셀 맵일 것이며, 텍스트에 대해서는 word-by-word influence scores가 될 수 있다.

### White-box

> 딥러닝 모델 $f$에 대해서, 모델 파라미터 $\theta$ 와 모델 구조가 알려져 있는 경우, 이 모델을 화이트박스(White-box)라 여긴다.

화이트 박스 모델은 모델 디버깅을 용이하게 하고, 신뢰도를 향상시킨다.

하지만 모델 구조와 파라미터에 대해서 아는 것은 모델을 설명가능하게 하지는 않는다.

###  Black-box

>모델 파라미터나 네트워크 구조가 최종 사용자에게 숨겨져 있으면 이를 블랙박스(Black-box)라고 여긴다.

웹 기반 딥러닝 모엘 서비스나, 제한된 비즈니스 플랫폼에서의 API식 모델은 입력 데이터를 받아 단순히 결과물만 반환하는 블랙박스적 구성을 띄고 있다.



남은 용어들은 XAI가 왜 중요한지를 설명하며 같이 설명한다.

인공지능이 헬스케어 분야, 신용점수, 대출 승인 등에 대해서는 윤리적, 사법적, 안전성 면에서 중요하다.

XAI가 중요한 부분에서는 크게 3가지 부분으로 나눌 수 있다.



### Transparent

> 딥러닝 모델의 표현이 사람이 알아듣기 충분한 경우, 모델을 투명하다(Transparent)고 여긴다.



**1) XAI는 투명성을 증가시킨다.**

XAI는 결과물을 사람이 인식할 수 있게 해석하므로 투명성과 공정성이 증가한다.

투명성은 결과물의 질이나, 외부 공격을 차단할 수 있다는 점에서 중요하다.



논문은 특히 외부 공격에 대해서 다음 모습을 보였다.

![survey_4](/Users/jun/My Works/paperStudy/ML_paper_study/XAI/Images/survey_4.png)

논문에서는 적대적 공격의 예시로 다음 사진을 보여 주고 있다. 원본 이미지의 약간의 적대적 노이즈를 더해주니 긴팔원숭이로 이해하는 문제를 보였다.

![survey_5](/Users/jun/My Works/paperStudy/ML_paper_study/XAI/Images/survey_5.png)

다른 예시로 이미지를 분류할 때 워터마크에 집중하여 분류하는 모습을 보인다.

텍스트를 제거하니 다른 이미지로 인식되는 모습을 보인다.



우리가 자동화된 알고리즘에 의존할 수록 AI알고리즘이 공격을 방어하고 투명한 결과를 제공하는 것은 매우 중요해져야 할 것이다.



### Trustbility

> 딥러닝 모델의 신뢰가능성(Trustbility)은 최종 사용자인 인간으로서, 현실 환경에서에서 모델의 의도한 동작에 대해서 측정된 확신의 정도이다.



**2) XAI는 모델의 신뢰성을 높인다.**

인간은 사회적 동물로서 우리의 결정은 특정 상황에 대한 지식과 사실에 의해 내려진다.

즉 아무 설명이 없는 최적의 결정보다 덜 합리적인 결정에 대해 과학적 설명/논증이 있는 것이 더 낫다.

따라서 '특정 결정이 왜 내려졌는가' 는 최종 사용자가 신뢰감을 가지는 데 매우 중요한 요소가 될 것이다.

Fundamental explanations 는 이해관계자나 정부 대리인들에게 신뢰를 주고, socio-economic 환경에서 AI를 연결할 수 있게 했다.



### Bias

> 딥 러닝 알고리즘의 편향(Bias)은 편향된 가중치, 편견, 선호, 인간의 데이터 수집이나 학습 알고리즘 부족에 의해 유발된 학습된 모델의 경향성이다.



**3) XAI는 모델의 편향을 이해하고 공정성을 증가시킨다.**

XAI 기술을 통해 모델의 행동을 이해하는 것은 모델의 편향과 왜도에 대한 이해를 증가시킬 수 있다.

입력 공간(input space)에 대한 이해는 편향이 줄어든 모델이나, 더 빠른 모델에 대한 연구가 가능하게 할 것이다.





XAI 기법은 많은 이점을 가져다 준다. 하지만 설명을 위해 적합한 방법을 선택하는 것은 많은 주의와 노력이 필요하다.

본 논문은 다양한 기법을 제시해 볼 것이다.

## Scope of Explanation

앞서 이야기했던 세 가지 분류 중 설명 범위에 대해 분류한 설명가능 모형이다.

### Local Explanations

- 의사가 분류 모형의 결과를 가지고 진단을 내린다고 상상해 보자.
- 의사는 인공지능의 예측에 대해 깊은 예측과 '왜 그렇게 생각했는지' 강건한 예측이 필요하다.
- 이와 같은 유형의 문제를 Locally explainable한 방법이라고 설명한다.



로컬 설명은 모형 f와 단일 데이터 x를 통해 설명 내용인 g를 만드는 것이다.

논문에서는 그림으로 다음과 같이 설명한다.

![survey_6](/Users/jun/My Works/paperStudy/ML_paper_study/XAI/Images/survey_6.png)



- 초기 연구는 히트맵, rule-based한 방법, 베이지안, 피처 중요도, 등을 사용했었다.
- 이 결과들은 항상 양의 real-valued metrics/vectors였다는 문제점이 있었다.
- 최근 연구는 attribution maps나 그래프 기반, 게임이론 기반 등을 사용해 양수와 음수의 결과를 모두 사용한다.
- 양의 분포값은 특정 피처가 결과가 나오는데 긍정적 영향을 미친 것이고, 음의 분포값은 결과의 부정적인 영향을 미치는 것이다.



#### Activation Maximization

참고 : https://m.blog.naver.com/vyoyo/221552750022

- CNN에서 Layer-wise 한 피처의 중요도를 파악하는 방법이다.
- 특정 채널의 activation을 최대화 하는 패턴x가 있다면, 그 x가 채널이 학습한 피처의 패턴이라고 볼 수 있다는 아이디어



![survey_7](/Users/jun/My Works/paperStudy/ML_paper_study/XAI/Images/survey_7.png)

출처 : [HOW CONVOLUTIONAL NEURAL NETWORKS SEE THE WORLD — A SURVEY OF CONVOLUTIONAL NEURAL NETWORK VISUALIZATION METHODS (Zhuwei Qin, 2018)](https://arxiv.org/pdf/1804.11191.pdf)



1. 랜덤한 픽셀로 구성된 이미지 $x_0$ 을 구한다.
2. 이미지를 파라미터가 고정된 학습 모델에 넣고 그래디언트를 구한다.
3. 정해진 학습률만큼 activation값이 최대화하는 방향으로 움직인다.
4. 학습이 완료되면 $x^*$ 는 특정 패턴의 이미지가 나타날 것이다.

학습이 완료되면 다음 결과를 보인다.

![Some convnet filters](https://blog.keras.io/img/conv5_2_stitched_filters_8x3.png)

출처 : [How convolutional neural networks see the world](https://blog.keras.io/how-convolutional-neural-networks-see-the-world.html)



#### Saliency Map Visualization

참고 자료 : https://yeoulcoding.tistory.com/76

- 샐리언시 맵은 사람이 물체를 보는 것은 관심 영역을 따라 시선을 집중하는 데서 아이디어를 얻었다.
- 샐려언시 맵은 출력 카테고리에 대한 모델의 그래디언트를 계산한다.

- 그래디언트를 시각화하면 픽셀에 대한 중요도를 볼 수 있을 것이라는 데서 출발한다. (양의 그래디언트를 가지면 출력 결과에 더 큰 영향을 줄 것이라는 가정)

- 저자는 1) 클래스 모델 시각화, 2) image-specific 시각화의 두 가지 시각화 방법을 제안했다.
- 1) 클래스 모델 시각화는 차후에 설명한다. (글로벌 설명이기 때문)



![image](https://blog.kakaocdn.net/dn/c2kTzL/btqCKA4EceF/WS9aUqI0zy5RUlJ2zjUmMk/img.png)



샐리언시 맵의 추출은 다음 과정을 통해 이루어진다.

1. 명확하게 라벨링된 이미지와 잘 훈련된 모델을 준비한다.
2. 이미지를 모델에 넣어 출력 벡터를 구한다.
3. 구한 벡터를 input 이미지에 대해 편미분하여 기울기를 구한다.
4. 3)의 결과의 3개의 값(R, G, B) 중 최댓값을 취한 뒤에 절댓값을 취한다.
5. 결과 반환



#### Layer-wise Relevance BackPropagation (LRP)

참고 : https://angeloyeo.github.io/2019/08/17/Layerwise_Relevance_Propagation.html

- LRP 기술은 DNN의 출력값을 분해(Decompose)하여 각각의 피처에 대한 타당성 점수(relevance scores)를 구한다
- CNN (타당성이 레이어간 전파된다) 과 RNN(타당성이 은닉 상태와, 메모리 셀에 전파된다) 모두 적용될 수 있다.



![img](https://raw.githubusercontent.com/angeloyeo/angeloyeo.github.io/master/pics/2019-08-17_LRP/pic7.png)

출처 : [**Layer-wise Relevance Propagation** - 공돌이의 수학정리노트](https://angeloyeo.github.io/2019/08/17/Layerwise_Relevance_Propagation.html)



- 각 층에서 역순으로 출발하여 각 층의 타당성 점수를 전파한다.

- 하나의 뉴런의 출력은 그 노드에 대한 타당성 점수의 합으로 나타내어진다.

$ f(x) = \Sigma_jR_{i\leftarrow j}$

- 타당성 점수의 전파는 다음 그림과 같다.

  ![img](https://2.bp.blogspot.com/-nwa2Y3ZW2Cw/XV-UOUCTuxI/AAAAAAAAsXc/zRTQgHVb39w_JMBRv_xqM3nSbez3BkwyQCK4BGAYYCw/s640/LRP.PNG)

출처 : [딥러닝 안에서 일어나는 과정을 해석하는 설명가능 인공지능 기술](https://itkmj.blogspot.com/2019/08/blog-post.html)

- 한 계층의 타당성 점수의 합은 보존 공식에 의해 이전 계층의 모든 타당성 점수의 합으로 나타내어진다.
- 이렇게 얻은 마지막 계층의 타당성 점수를 시각화하면 중요도를 시각적으로 표현할 수 였을 것이다.



최근 연구는 LRP 방법이 모델의 정확도 손실 없이 연산량이나 저장 비용 등을 절감하는 network pruning으로도 사용될 수 있음을 밝혀 냈다.



#### Local Interpretable Model-Agnostic Explanations (LIME)

참고 : https://yjjo.tistory.com/3



LIME은 '중요한 부분일 수록 변형되었을 때 예측값이 크게 변한다'는 생각에서 출발해 입력을 변형시키면서 예측값을 크게 변화시키는 것을 찾는 방법이다.



- LIME은 연속적인 '슈퍼픽셀'을 통해 중요성을 찾으려 하는 방법이다.
- 0 (목표값이 없다) 또는 1(목표값이 있다) 을 예측하는 방법으로 문제를 단순화 한다.
- 위 데이터는 이미지에 대해서는 다음과 같이 나타낼 수 있다. 출처 : [Interpretable Machine Learning for Image Classification with LIME](https://towardsdatascience.com/interpretable-machine-learning-for-image-classification-with-lime-ea947e82ca13)
- ![img](https://miro.medium.com/max/3634/1*wHLeYXmhK7h34yKb4Iq56A.png)
- 이를 데이터 1개에 대해 나눠서 진행한다.

- $\xi(x) = argmin_{g \in G}\mathcal{L}(f,g,\pi_x) + \Omega(g) $ 식으로 최적화 문제를 나타낼 수 있다.
- LIME는 이를 최소화하는 방향으로 학습을 진행한다.
- $\mathcal{L}(f,g,\pi_x)$ 는 $f(x)$ 와 $g(x)$ 의 차이로 생각될 수 있다. (예측 값이 작을수록 중요한 데이터가 포함되어 예측 오차가 작아진다.)

<img src="https://miro.medium.com/max/2524/1*K4HCitQxRrjcFekIsSZDSg.png" alt="img" style="zoom:67%;" />

출처 : [Interpretable Machine Learning for Image Classification with LIME](https://towardsdatascience.com/interpretable-machine-learning-for-image-classification-with-lime-ea947e82ca13)



LIME 분석을 텍스트 데이터에 대해 출력하면 다음과 같은 결과물이 나타난다.

![20 newsgroups 데이터셋 중 한 예측에 대한 설명.](https://d3ansictanv2wj.cloudfront.net/figure5-cd7d3c5128549df1e957bf8f9f93bb2b.jpg)

출처 : [머신러닝 모델의 블랙박스 속을 들여다보기 : LIME](https://dreamgonfly.github.io/blog/lime/)



최근에는 LIME을 발전시키는 많은 후속연구들이 존재한다. 본 논문은 그 사례를 몇 가지 들고 있다.

- [**Sound-LIME(SLIME)**](https://www.semanticscholar.org/paper/Local-Interpretable-Model-Agnostic-Explanations-for-Mishra-Sturm/8b0a16b2475798ed1b5f5cffed62a47e1ef30c7d) : LIME을 활용해 목소리 탐지 시스템을 설명하고자 했다.

  <img src="/Users/jun/My Works/paperStudy/ML_paper_study/XAI/Images/survey_8.png" alt="survey_8" style="zoom:50%;" />

- [**KL-LIME**](https://arxiv.org/abs/1810.02678) : 베이지안 모델을 설명하기 위한 LIME 모델, KL-divergence (두 확률분포 간 차이)를 최소화하는 모형을 발견했다.

- [**DLIME**](https://arxiv.org/abs/1906.10263) : 무작위 변형이 아닌 계층적 클러스터링이나 KNN기법을 사용한 방법. 더 안정적으로 분석이 가능해졌다.

- [**Quadratic-LIME(QLIME)** ](https://scholar.smu.edu/cgi/viewcontent.cgi?article=1138&context=datasciencereview): 선형 모델이 아닌 모델에도 LIME을 적용했다.

- [**Modified Perturbed Sampling operation for LIME(MPS-LIME)**](https://arxiv.org/abs/2002.07434) : 슈퍼픽셀 선택 방법을 변경한다. (그래프적 방법 도입)

  <img src="/Users/jun/My Works/paperStudy/ML_paper_study/XAI/Images/survey_9.png" alt="survey_9" style="zoom:50%;" />



#### SHapley Addictive exPlanations (SHAP)

참고 : https://datanetworkanalysis.github.io/2019/12/23/shap1, https://eair.tistory.com/30

- SHAP는 input $x$이 예측값에 미친 피처별 기여도를 설명한다.
- 섀플리값은 '연합 게임이론'에서 플레이어의 기여도에 따라 보상을 배분하는 방법에 대한 식이다.
- 이 때 피처는 테이블 형태에서는 각각의 행이 될 수 있고, 이미지에서는 슈퍼픽셀로 생각할 수 있다.
- $g(z′)=ϕ_0+∑_{j=1}^{M}ϕ_jz′_j$ 의 식으로 계산한다.
- $z$는 특성 벡터로서 특정 피처가 있으면 1, 없으면 0으로 계산. $\phi$는 섀플리 값 (기여도)를 의미한다.
- $g(z')$는 존재하는 피처들의 섀플리 값의 합으로 설명된다.



기본적인 SHAP 방법은 이후 다양한 방법으로 적용되었다.

**KernelSHAP**

- LIME 모형에 SHAP커널을 사용하여 값을 추정하는 방법이다
- 대량의 데이터에서 필요한 계산량을 감소시켰다.
- 모든 머신러닝 알고리즘에 적용될 수 있다. (피처를 랜덤 샘플링해서 제거하는 방식 사용)

**LinearSHAP **

- 최대 연합의 크기 $M$이 작은 경우에서 효율적이다.

**DeapSHAP**

- DeepLIFT 방법을 적용했다.

- DeepLIFT는 역전파 시 기울기 변화량을 사용해서 영향력을 계산하는 방법이다.

  <img src="/Users/jun/My Works/paperStudy/ML_paper_study/XAI/Images/survey_10.png" alt="survey_10" style="zoom:50%;" />

  출처 : [Learning Important Features Through Propagating Activation Differences](https://docs.google.com/file/d/0B15F_QN41VQXSXRFMzgtS01UOU0/edit?filetype=mspresentation)(논문 발표)



SHAP 방법은 의료 분야에서 의사결정을 설명하기 위해 사용된다.

본 논문은 의료 분야에서 SHAP의 적용에 대해서 설명했다.

- [**extendedSHAP**](https://arxiv.org/abs/1903.02407) : 이상 탐지를 위해 사용되던 오토인코더를 설명한다. 오토인코더가 재구성(reconstruction)할 때의 오차를 사용해 확인한다.

- [**Baseline Shapley(BShap)**](https://arxiv.org/abs/1908.08474) : 특정 피처가 상대적으로 덜 중요할 때 비직관적인 설명을 내는 문제를 해결했다.

- [**KernelSHAP 의 확장**](https://arxiv.org/abs/1903.10464) : 상관관계가 있는 피처들을 해석하기 위해 개발되었다.

- [**TreeExplainer**](https://arxiv.org/abs/1905.04610) : SHAP을 트리 모델에 대해 확장했다. 트리 모델의 로컬 설명이 다항시간 안에 계산될 수 있음을 밝혔다.

- [**LSTM에 대해 확장**](https://www.sciencedirect.com/science/article/abs/pii/S1574954119303498) : DeepSHAP 알고리즘을 사용해 LSTM에 확장했다.

  

### Global Explanations

![](/Users/jun/My Works/paperStudy/ML_paper_study/XAI/Images/survey_11.png)

- 글로벌하게 설명하는 방법은 딥려닝 모델을 더 해석하기 쉬운 선형 모델로 추론한다.
- Rule-based나 트리 모형, 선형 모델은 그 자체로 글로벌하게 해석가능한 모델이다.
- 일반적으로 글로벌하게 설명가능한 모형은 입력들의 대해 블랙박스 모형의 전반적인 경향을 보여준다.



#### Global Surrogate Models

- Global Surrogate Model은 비선형적 모델을 선형 모델이나 트리 모델로 근사시키는 방법이다.
- 본 모델을 설명하기에는 너무 복잡하기 때문에 훨씬 단순한 모형으로 표현하고자 하는 것이다.
- "어떻게 내 AI 모델이 일반화될 수 있는지", "어떻게 내 AI모델의 변형이 작동하는지"에 대한 질문에 대답한다
- Surrogate Model의 대표적인 예시는 feature-rich layer embeddings이다.

- SHAP, LIME등을 대리자로 사용해서 예측할 수 있다.



사용 예시는 다음과 같이 나타난다.

출처 : https://christophm.github.io/interpretable-ml-book/global.html

1. 데이터셋 $X$ 를 선정한다.
2. 블랙박스 모델 $f$에 $X$를 넣어 예측값을 생성한다.
3. 해석가능한 모델의 타입을 설명한다.(선형 모델, 의사결정트리...) 이를 대리 모델로 선정한다
4. $X$ 와 $f(X)$(예측값)에 대해 대리 모델을 학습시킨다.
5. 대리 모델을 해석한다.



#### Class Model Visualization

참고 : https://glassboxmedicine.com/2019/07/13/class-model-visualization-for-cnns/

- Activation Maximization을 Class Model을 사용하여 글로벌하게 확장한 방법이다.
- 이미지 클래스를 분류하는 모델$f$ 는 $c$ 클래스 이미지 $I$에 대해 예측값을 반환한다.
- 이 클래스 이미지의 확률 $S_c(I)$ 를 최대화하는 방향으로 학습된다. 
- 즉, $I' = argmax S_c(I) - \lambda ||I||^2_2$ 으로 표현된다.
- L2 Norm부분은 이미지가 너무 극단적인 값으로 뛰는 것을 막아준다.

- 이렇게 생성된 이미지는 블랙박스 모델이 특정 클래스에 대해 무엇을 학습했는지를 나타낼 수 있다.

- 이렇게 생성한 이미지를 'Deep Dream' 이라고 부르기도 한다.

  

<img src="https://www.researchgate.net/profile/Talley-Lambert/publication/312620507/figure/fig3/AS:453895710351363@1485228578818/Class-Model-Visualization-We-estimated-class-models-from-either-the-healthy-top-row-or.png" alt="Class Model Visualization. We estimated class models from either the healthy (top row) or sick (bottom row) classes. Initializing the model image I to a zero image (left panels) produced structures weakly reminiscent of nucleoli for the healthy class (upper left panel) and more disorganized images for the sick class (lower left panel). Initializing I to an image from the opposing class (right panels) added nucleoli to sick cells and removed vacuoles (upper right panel) but again produced more chaotic alterations when modeling the sick class (lower right panel). We interpret these changes cautiously, as some aspects of these alterations may be due to regularization.  " style="zoom:50%;" />

출처 : [DeadNet: Identifying Phototoxicity from Label-free Microscopy Images of Cells using Deep ConvNets](https://www.researchgate.net/figure/Class-Model-Visualization-We-estimated-class-models-from-either-the-healthy-top-row-or_fig3_312620507)



#### LIME Algorithm for Global Explanations

참고 : https://yjjo.tistory.com/3

- 서브모듈러 선택 알고리즘(SP-LIME으로 불린다) 을 사용해 전역 중요도를 생성한다.
- 동작원리가 surrogate model과 비슷하다고 볼 수 있다.



**방법**

1. 블랙박스 모델 $f$와 데이터 $X$을 정의해 LIME을 수행한다.
2. B는 우리가 선택한 데이터의 집합(Budget)이다.
3. $f$를 최대한 많이 설명하는 가장 적은 데이터 입력을 수행하는 경우를 $B$ 에서 찾는다.
4. 이때 탐욕 알고리즘 (전체를 모두 수행하는 방법) 이 사용된다.



#### Concept Activation Vectors (CAVs)

- 신경망의 내부 상태를 인간이 이해할 수 있는 도메인으로 변환한다.
- 해석가능한 글로벌 모델을 $g$라 할 때, $g : E_m \rightarrow E_h$ 로 표현가능하다
- $E_m$은 블랙박스 모델 $f$ 의 벡터 표현, $E_h$는 인간이 이해할 수 있는 벡터 공간이다.



![img](https://communedeart.files.wordpress.com/2019/09/image-11.png?w=942)

출처 : https://communedeart.wordpress.com/2019/09/16/tcav%EB%A5%BC-%EB%B0%9B%EC%95%84%EB%93%A4%EC%9D%B4%EA%B8%B0-%EC%9C%84%ED%95%9C-%EB%85%B8%EB%A0%A5/



- 얼룩말에서 긍정적(positive) concept인 $P_c$ (줄무늬 등)과 부정적(Negative) concept인 $N$ 으로 분리했다.
- 특정 데이터 $x$ 가 $P_c$ 와 $N$ 을 구분할 수 있는 이진 분류 모델을 학습시킨다.



**Testing with CAVs**

- 그래디언트 기반 방법처럼 방향도함수(directional derivatives)를 사용하는 방법이다.
- 특정 입력에 대한 $f$의 예측값의 민감도를 평가한다.
- TCAV 점수는 입력값 변화에 따른 특정 레이어 출력($h(j,k)$)의 변화량이다.



![survey_12](/Users/jun/My Works/paperStudy/ML_paper_study/XAI/Images/survey_12.png)

- TCAV는 입력 콘셉트가 적절하게 선택되지 못하면 좋은 결과를 얻지 못한다는 단점이 있다.
- 서로 관련성이 높은 콘셉트도 성능을 감소시킬 수 있다.



CAV 방법은 이후에 많은 발전이 있었다.

- [**Automatic Concept-based Explanations (ACE) **](https://arxiv.org/abs/1902.03129): 다중 해상도(multi-resolution) 세그먼테이션을 수행할 수 있게 했다.

![survey_13](/Users/jun/My Works/paperStudy/ML_paper_study/XAI/Images/survey_13.png)

- [**Casual Concept Effect(CaCE)**](https://arxiv.org/abs/1907.07165) : 딥러닝 모델에 대한 high-level concepts의 있고 없음에 따른 인과관계에 집중한다.
- [**ConceptSHAP**](https://arxiv.org/abs/1910.07969) : 각각 발견된 콘셉트의 중요성과 완전성(completeness) 점수를 계산한다. 특정 지역에 대해 콘셉트를 유지하는 클러스터링을 수행한다.



#### Spectral Relevance Analysis(SpRAy)

- SpRAy는 LAP설명법을 기반으로 한 로컬 인스턴스의 최상단 부분을 설명한다

- LRP 모델에서 자주 나오는 특징을 분석하여 머신 러닝 모델의 정상/비정상을 파악한다.

  <img src="/Users/jun/My Works/paperStudy/ML_paper_study/XAI/Images/survey_14.png" alt="survey_14" style="zoom:67%;" />

- LRP를 통과한 결과값에 대해 Specral Cluster Analysis(SC) 와 EigenMapAnalysis를 수행한다.
- 이렇게 하면 importrance cluster가 반환되는데, 이걸 t-SNE 등으로 시각화할 수 있다.

![survey_15](/Users/jun/My Works/paperStudy/ML_paper_study/XAI/Images/survey_15.png)



#### Global Attribution Mapping

- GAM은 각각의 피처들의 conjoined rankings를 랭크 벡터 $\sigma$ 로 나타낸다.

- 로컬 분석을 먼저 한 뒤에, pair-wise rank distance matrix/cluster을 찾는다.

  <img src="/Users/jun/My Works/paperStudy/ML_paper_study/XAI/Images/survey_16.png" alt="survey_16" style="zoom: 50%;" />

출처 : Global Explanations of Neural Networks



#### Neural Additive Model (NAMs)

<img src="https://paperswithcode.com/media/methods/nam_xnCYK9q.jpeg" alt="img" style="zoom:50%;" />

- 하나의 피처에 주목하는 하나의 인공 신경망을 만들어서 합치는 방법으로 모델을 설명한다.

- generalized additive models (GAM)을 구성하여 분석한다

  $g(E[y]) = \beta + f_1(x_1) + f_2(x_2) + ... + f_K(x_K) $

- 논문의 저자는 ReLU를 개선한 exp-centered (ExU) $ h(x) = f(e^w * (x-b))$ 을 도입했다.

- 또한 가중치 초기화로 $ N(x, 0.5)$ with $x \in (3, 4) $ 를 사용했다.

- 음수 값은 클래스 예측 확률을 낮추고, 양수 값은 클래스 예측 확률을 증가시킨다.

- NAM을 사용하면 출력값과 상관 없이 각각의 피처에 대한 정확한 설명이 가능하다는 장점이 있다.

  