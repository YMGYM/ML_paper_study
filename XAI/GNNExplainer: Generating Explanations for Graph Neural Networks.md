# GNNExplainer: Generating Explanations for Graph Neural Networks
본 게시글은 동명의 [논문](https://arxiv.org/abs/1903.03894)을 정리하여 내용을 이해하기 위해 작성되었습니다.



## Abstract

- GNN은 그래프 분야의 머신 러닝에서 강력한 도구이다.
- GNN 내부의 그래프 구조와 피처들은 모델을 복잡하게 하고 설명하기 어렵게 만든다.
- 본 논문은 GNNExplainer 를 제시한다. 이는 model-agnostic 한 GNN 설명 도구이다.
- GNNExplainer 는 그래프를 각각의 subGraph로 나누고, 중요한 역할을 하는 노드집합을 찾는다.
- 또한 모든 클래스에 대해서 일관적이고 정확한 설명을 할 수 있게 된다.
- GNNExplainer을 가능한 서브그래프 구조의 예측과 분배를 최대화하는 최적화 과정으로 정의했다.
- GNNExplainer는 중요한 기능을 확인하거나, 관련있는 요소를 시각화하거나, 오류에 대한 해석을 가능하게 하는 등 많은 장점이 있다.



## Introduction

- 그래프는 실제 세상의 정보를 표현하는 데 장점이 있으며, 이를 표현하기 위해 GNN이 등장했다.
- 그럼에도 불구하고 GNN은 투명성이 부족하다.
- GNN을 이해하는 능력은 다음 면에서 중요하다.
  - 모델의 신뢰성을 높인다.
  - 공평성, 프라이버시, 안전 부분에서 투명한 결정을 가능하게 한다.
  - 배포 전에 모델에 대한 전반적인 경향성을 확인할 수 있다.
- GNN을 설명하려는 시도는 locally하게 시도하는 방법, 모델의 경향성을 분석하는 방법 두 가지로 이루어졌다.
- 하지만 이 방법들은 GNN의 핵심이 되는 연관된 정보를 구체화하지 못해서 실패하고 말았다.



- 본 논문은 GNNExplainer를 제안한다. GNNExplainer는 그래프와 예측을 입력으로 받아서 부분그래프의 요소와, 가장 예측에 중요했던 부분그래프를 보여 준다.
- 이 방법은 model-agnostic 하며, 예측, 분류 등 어떠한 도메인에도 적용이 가능하다.
- 본 논문은 GNNExplainer를 평가해 봤는데, 실제 GNN 예측에도 일관적이고 정확한 예측을 주는 것으로 나타났다.
- 또한 GNN이 영향을 주는 특징과 레이블을 확인하는 작업을 통해 중요한 인사이트를 줄 수 있다는 것도 보였다.



## Related work

- 그래프 모델이 아닌 것을 설명하려는 시도는 proxy 모델을 제시하려는 시도다.
- 다른 방법은 중요해 보이는 면을 확인하는 시도다.
- 이 두가지 계열은 그래프의 이산적인 입력에는 잘 적용되지 못하는 모습을 보였다.
- 이 외에도 모델을 블랙박스로 취급하고 연관된 정보를 뽑아내려는 시도 또한 있었다.
- 최근 연구는 GNN에 어텐션을 적용하여 해석가능성을 높였다.
- 하지만 이 방법은 예측에 대해서는 비슷한 값을 보여, 어떤 노드가 예측에 영향을 주었는지 알기 어렵다.





## Formulating explanations for graph neural networks

- 엣지 $E$, 그래프 $G$ $V$ 를 d차원의 피처로 정의한다.
- $f$는 노드에 대해 클래스를 매핑하는 함수,
- $\Phi$ 는 그래프 모델을 의미한다.

### Background on graph neural networks

- GNN 모델의 업데이트는 세 가지 계산을 포함한다.
  - 모든 node쌍에 대해서 neural messages를 계산한다. (MSG())
  - 각각의 노드 $v$에 대해서 GNN은 인접한 모든 이웃 노드 $N_{v_{i}}$ 에 대해서 메세지를 종합해 $M_i$ 를 만든다. (AGG)
  - 종합한 메시지를 모아 다음 시점 예측을 한다. (UPDATE)



### GNNExplainer : Problem formulation

- 본 논문의 핵심 인사이트는 노드 $v$의 계산을 통해 임베딩 $z$를 도출하는 과정을 관찰하는 것이었다.
- GNN을 설명하기 위해선 그래프 구조 $G_c (v)$ 와 노드 특징 $X_c (v)$ 만 관찰하면 된다.





## GNNExplainer


### Single-instance explanations

- GNNExplainer 는 주어진 서브그래프와 피처 상에서 예측을 해 보고 mutual information(MI) 가 가장 높게 나타나는 지점을 구한다.

- 이는 conditional entropy $H(Y|G = G_s , X = X_s)$를 최소화하는 것과 같다.
- Gradient based 방법을 통해 최적화시켰다.



### joint learning of graph structural and node feature information

- 어떤 노드가 중요한지 알기 위해 GNNExplainer 는 피처 선택기 $F$를 학습시킨다.
- $F$ 는 $X$에 대해 마스킹 효과를 가진다. 
- 중요하지 않은 피처라면 제로 그래디언트를 가질 것
- 이 방법은 중요하지만 그래디언트가 0인 변수도 소멸시킬 수 있기에 marginalization을 수행했다.
- 이 방법을 통해 그래프에서 끊어진 곳 등을 찾을 수 있들 것이다.(비중이 제로이기 때문)



### Multi-instance explanations through graph prototypes

- 클래스 전체에 대해 영향을 주는 부분그래프를 확인해 볼 수 있을까?

- GNNExplainer 는 그래프 정렬과 프로토타입에 기반해서 이를 수행했다.

- 레퍼런스 노드 하나를 선정하고 그 노드를 중심으로 그래프를 정렬한다.

- 또는 프로토타입 그래프 $A$를 두고 adjacency matrices를 정렬해 합쳤다.




### GNNExplainer model extentions

- GNNExplainer 는 모델의 수정 없이 예측과 그래프 분류를 제공한다.
- GNNExplainer는 현재 그래프 기반 모델에 대부분 적용이 가능하다.
- 이 때 시간복잡도는 노드 $v$ 에 대한 계산 그래프 $G_c$ 의 크기에 따라결정된다.
- 주로 이 그래프는 상대적으로 크지 않기 때문에, GNNExplainer가 효과적으로 설명을 만들어 낼 수 있다.



## Experiments

- 본 논문의 정량적, 정성적 분석은 GNNExplainer 가 그래프 구조나, 노트 피쳐 면에서 효과적이고 정확한 설명 도구임을 보여 준다.

- Synthetic dataset : 4개의 분류 데이터셋을 사용했다.
- Real-world dataset : 2개의 그래프 분류 데이터셋을 사용했다.
- Alternative baseline approaches : 그래디언트 기반의 'GRAD' 방법과, 어텐션 기반의 ATT방법을 사용했다.
- Setup and implementation details : 학습에 사용된 하이퍼파라미터 수치와, Grad/GNNExplainer를 먼저 학습시키다는 설명 등이 적혀 있다.
- 본 논문은 다섯 가지 질문에 답한다.
  - GNNExplainer가 분명한 설명을 제공하는가?
  - 기존 설명 방법과 비교해서 효과적인가
  - GNNExplainer가 다양한 그래프 기반 예측 태스크에서 효과적인가
  - 다른 GNN 네트워크에서 예측한 것을 설명할 수 있을까?



### Quantitative analyses

본 논문은 explanation problem 을 이진 분류 문제로 공식화하고, 좋은 설명성을 가지는 모델은 높은 점수를 가질 것이다.

GNNExplainer는 다른 방법보다 평균적으로 17.1% 으로 높은 성과를 보였으며, Tree-Grid 모델에 비해 43.0% 높은 정확도를 가진다.



### Qualitive anaylses

Topology-based 예측에서 GNNExplainer는 정확하게 network motif를 확인하는 모습을 보였다.

Reddit 데이터셋에 대해서 다른 데이터셋에 비해 비교적 잘 관계를 파악하는 모습을 보였다.

ATT는 메시지에 대한 중요도를 계산할 수 있었지만, single-instance explanations은 하지 못했다.

모델이 설명가능한지가 중요한 요소이기 때문에, 모델은 쉽게 이해가능한 설명을 내놓을 수 있어야 한다.

GNNExplainer는 적은 수의 feature 개수로부터도 구조적 정보들 고려한다. 반면 gradient-based방법은 노이즈에 취약한 모습도 보였다.





## Conclusion

- 본 논믄은 GNN 환경에서 하나의 조정 없이 예측에 대한 설명을 제공하는 GNNExplainer를 제시했다.
- GNNExplainer는 재귀적인 방법을 통해서 중요한 그래프 경로와, 관계가 높은 노드를 하이라이팅 할 수 있다.
- 본 논문의 연구는 합리적인 구조로 접근하며, 직관적인 인터페이스를 제공한다는 점에서 독창적이라고 볼 수 있다.

