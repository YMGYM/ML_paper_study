# Attention is not Explanation



## Abstract

- Attention 메커니즘은 NLP 모델에서 광범위하게 적용되었다.
- Attention은 투명성있는 메커니즘을 제공하지만 input과 output의 관련성이 있으면 설명하기 어려워지는 문제점이 있다.
- 본 논문의 방법은 어떤 Attention 가중치가 예측에대해 의미있는 설명을 제공하는지 나타낸다.
- 우리의 발견은 일반적인 Attention modules가 의미있는 설명을 제공하지 못함을 나타낸다.



## Introduction and Motivation

- Attention 방법은 입력 유닛에 대해 가중치 맥락 백터를 반환하는 알고리즘으로 NLP분야에서 거의 광범위하게 사용되고 있다.
- Attention은 종종 모델이 어떤 가중치를 부여하는지 확인하므로서 인사이트를 제공한다고 알려져 있다.
- 모델 출력값에 영향을 주는 요인이 높은 어텐션 가중치를 가진다는 가정이 명확하게 계산되지 않았고, 문제가 많다는 사실을 증명했다.
- 본 논문은 어텐션 가중치, 입력, 출력 간 관계를 실험을 통해 확인하며 두 가정을 실시한다.
  - 어텐션 가중치는 다른 피처 중요도 기법과 상응해야 한다.
  - 대체된 Attention의 가중치 번화는 출력값의 결과 변화 방향과 상응해야 한다.

### Research questions and contributions

본 논문은 어텐션이 제공하는 모델의 투명성을 다음 조건을 확인하며 탐색했다.

1. 어텐션 가중치는 피처 중요도의 특징에 상응한다.
2. alternative 어텐션 가중치가 적절하게 다른 예측을 산출할 것인가?



## Preliminaries and Assumptions

- $x$은 모델 입력값, 임베딩 매트릭스 $E$, 인코더 Enc라 한다. 이때 인코더를 통과하여 다온 히든 값을 $h$라 한다.
- 유사도 함수 $\phi$ 는 $h$를 쿼리 $Q \in R^m$ 에 매핑한다. 이를 통과한 값을 softmax하여 $\hat\alpha$ 를 구한다.
- Dense층 Dec을 지나면서 예측값 $\hat y$ 를 산출한다.



## Datasets and Tasks

- binary text classification에서,  다음 데이터를 사용했다.

  - 'Stanford Sentiment Treebank'

  - IDMB

  - Twitter Adverse Drug Reaction dataset

  - 20 Newsgroups

  - AG News Corpus

  - MIMIC ICD9

    

- Question Answering 부분에선 다음 데이터를 사용했다.

  - CNN Neews Articles
  - bAbl



- Natural Language Inference (NLI)
  - the SNLY



## Experiments

실험은 다음 두 가지 질문에 초점을 맞춰서 진행됐다.

1. 학습된 어텐션 가중치가 다른 방법의 피처 중요도에 동의할 수 있을까?
2. 다른 피처에 대해서 어텐딩 하면 예측값이 달라질까?



- 1번 기준을 충죄시키는 것은 다른 방법에 의해 어탠션이 대체될 수 있음을 이야기한다. (값이 같아야한다.)
- 이를 측정하기 위해 랜덤하게 값을 왜곡하고, 결과값을 모니터링했다.
- 다름의 정도를 측정하기 위해 Total Variation Distance(TVD) 와 Jensen-Shannon Divergence(JSD) 방법을 사용했다.



### Correlation Between Attention and Feature Importance Measures

- 어탠션 가중치와 상응하는 피처 중요도 점수를 비교하고자 했다.
- 어탠션과 비교할 값으로 (1) 그래디언트 기반으로 한 방법과, (2) leaving features에 의해 도출된 모델 결과값
- 실험을 통해 확인해 보니 어텐션 가중치는 임베딩의 feature importance score와 상응하지 않는다는 사실을 알았다.



### Counterfactual Attention Weights

- 어텐션 가중치를 변경했을때 어떨까?하는 가정에서 출발했다.
- 다른 입력 피쳐값을 강조했다.
- 1. 원본 어텐션 가중치 $\hat \alpha$ 를 강화했다. 2. adversarial attention distribution을 생성했다.(결과값을 바꾸지 않으면서 어텐션 가중치가 $\hat\alpha$ 에서 가장 달라지는 값)
- 가중치를 변경했을 때 예측 값이 많이 바뀌어야 하지만, 약하게만 나타났다.



## Discussion and Conclusions

- 본 논문은 내재적인 피처 중요도 측정값과 학습된 어텐션 가중치 간 상관관계를 보여줬다.
- 또한 비현실적 어텐션 왜곡도 실시해 보았다.
- Attention 은 NLP에서 큰 발전을 이륙했지만, 해석가능성은 애매하다.
- RNN 인코더에 한해서는 인풋과 결과값의 차이가 애매하다.
- 본 논문은 대체한 방법이 gound truth 가 돼야 한다고 말하지는 않는다.