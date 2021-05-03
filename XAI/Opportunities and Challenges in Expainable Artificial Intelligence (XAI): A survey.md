# Opportunities and Challenges in Expainable Artificial Intelligence (XAI): A survey

by Arun Das and Paul Rad



link : https://arxiv.org/abs/2006.11371



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



XAI를 연구하는 이유는 다음 이유들을 들 수 있어 보인다.

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

앞서 이야기했던 세 가지 분류 중 설명 범위에 대해 분류한 설명가능 모형

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
4. 학습이 완료되면 $x_*$ 는 특정 패턴의 이미지가 나타날 것이다.

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