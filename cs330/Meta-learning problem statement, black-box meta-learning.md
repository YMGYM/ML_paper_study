# Meta-learning problem statement, black-box meta-learning

본 파일은 동명의 [CS330](https://cs330.stanford.edu/) 의 2주차 강의의 필기 내용입니다.

출처가 적혀 있지 않은 이미지는 모두 강의 PPT에서 발췌하였습니다.



## 정리

이 강의는 메타 러닝의 기본적인 내용을 전반적으로 정리하는 강의입니다.



## 용어 정리

본격적인 메타 러닝 내용에 들어가기 전에 기본적인 용어와 수식을 정리해 보도록 하겠습니다.



### Single-task Learning

먼저 우리가 지금 까지 알고 있는 일반적인 학습 방법인 Single-Task Learning (단일 태스크 학습) 입니다.

![single-task](/Users/jun/My Works/paperStudy/ML_paper_study/cs330/images/single-task.png)

 

Single-Task Learning 은 주어진 데이터 분포 $D$ 가 존재할 때, 이 분포에서 손실 함수 $L$을 최소화 할 수 있는 파라미터 값 $\theta$ 를 찾는 것입니다.

 이때 손실 함수는 우리가 알고 있는 함수 (크로스 엔토로피 등등) 을 포함합니다.



### Task

Single-Task, Multi-Task 등등 태스크 라는 말을 많이 사용했는데 Task란 구체적으로 무엇일까요?

본 강의에서 Task는 다음과 같이 정의되어 있습니다.

![task](/Users/jun/My Works/paperStudy/ML_paper_study/cs330/images/task.png)

Task $T$ 는 입력 값 $X$ 에 대해서 입력값의 분포, 입력에 대한 출력값의 분포, 손실 함수 등을 사용하는 과정으로 생각할 수 있습니다.



## Task의 예시

태스크가 정확히 무엇인지 잘 와닿지 않을 수도 있을 것이라고 생각합니다. 조금 더 자세히 알아봅시다.



Task의 예시로는 다음과 같습니다.

multi-task classification의 예시로는 다국어 손글씨 탐지, 개인에게 특화된 스팸메일 탐지가 있다.

이 경우 손실함수는 모든 Task에 대해서 같습니다.

Multi-label learning의 경우 유명인 인식하기, 장면 인식 등이 있으며 이 경우 Task에 따라 손실 함수가 다르게 적용된다.



그럼 언제 손실함수가 다를까요?

- 분포가 달라서 하나의 손실을 적용하기 어려운 경우
- 하나의 Task를 다른 것 보다 더 중요하게 생각할 때



![task-flow](/Users/jun/My Works/paperStudy/ML_paper_study/cs330/images/task-flow.png)



이 관점에서 바라볼 경우, 하나의 신경망의 Task를 관리하는 task descriptor $z_i$ 로 계산합니다. task descriptor의 상태에 따라 신경망이 다르게 작동하는 것이죠.

Task descriptor의 경우는

- task번호의 원-핫 인코딩이거나
- task의 메타 데이터이거나
- formal specifications



task가 여러 가지가 있는 경우는, 목적함수는 Task들의 손실 함수의 합이 됩니다.



이 경우 두 가지 문제가 발생하는데

- Z의 조건을 어떻게 설정?
- 목적 함수를 어떻게 최적화 할까

에 대한 문제가 발생합니다.





## 태스크의 관리

태스크가 다른 태스크와 어떻게 해야 최소한으로 겹칠까요



네트워크를 분할할 수 있을 것입니다.

![task-conditioning](/Users/jun/My Works/paperStudy/ML_paper_study/cs330/images/task-conditioning.png)



이 경우 각각의 네트워크는 파라미터를 공유하지 않은 채 여러 태스크로 관리되게 됩니다.





또는

![task-conditioning2](/Users/jun/My Works/paperStudy/ML_paper_study/cs330/images/task-conditioning2.png)

각각의 태스크의 입력, 활성화  값을 연결하여 하나의 네트워크처럼 학습 시킬 수도 있습니다.



이 조건에서 바라본 Multi-Task 문제의 목적 함수는 다음 식으로 나타낼 수 있을 것입니다.

![multi-task](/Users/jun/My Works/paperStudy/ML_paper_study/cs330/images/multi-task.png)



각각의 $\theta$는 태스크별로 쪼개져 $\theta^1 ... \theta^i$ 가 되며 $\theta^{sh}$의 경우는 태스크 끼리 공유하는 공유 파라미터 입니다.



이 시각으로 보았을 때 우리는 $z_i$를 설정하는 것은 태스크 간 파라미터 공유를 어떻게 할 것인지를 결정하는 문제가 됩니다.



## 조금 더 구체적인 관리



### 덧셈

조금 더 구체적으로 관리 방법을 알아 봅시다.

먼저 입력 값에 각 태스크 구분자를 연결 하거나, 더해 주는 방법이 있을 수 있습니다.

![conditioning-choice1](/Users/jun/My Works/paperStudy/ML_paper_study/cs330/images/conditioning-choice1.png)



이 둘은 두 개의 기법처럼 보이지만 사실 같은 방법입니다. linear한 층을 통과하는 과정에서 어짜피 하나로 합쳐지기 때문입니다.



### 멀티헤드 구조

![conditioning-choice2](/Users/jun/My Works/paperStudy/ML_paper_study/cs330/images/conditioning-choice2.png)

태스크가 각각 어떻게 공유되는지 아이디어가 없는 경우 다음과 같은 방법을 사용할 수 있고 합니다.

모델을 쪼개서 다양한 Head로 만듭니다.





### 곱셈적(Multiplicative) 구조

![conditioning-choice3](/Users/jun/My Works/paperStudy/ML_paper_study/cs330/images/conditioning-choice3.png)

가장 흔한 방법 중 하나입니다. 덧셈적 구조에서 덧셈을 곱셈으로만 바꾼 구조입니다.

곱셈적 구조가 왜 좋을까요?

- 덧셈적 구조보다 더 표현적임
- multiplicative gating을 얻기 때문 (각각의 특징을 모듈화하여 나눠서 계산할 수 있다고 함, 필요로 할 때만 사용할 수도 있음)



### 기타

![conditioning-choice4](/Users/jun/My Works/paperStudy/ML_paper_study/cs330/images/conditioning-choice4.png)

 이 외에도 수많은 복잡한 알고리즘이 있지만, 시간 문제상 다루지 않았습니다.





### 선택법

그럼 이 구조들 중 어떤 구조를 선택하는게 좋을까요?

이 선택은 다음 특징을 가집니다

- 문제에 의해
- 문제에 대해서 가진 직관과 배경지식
- 개인의 능력입니다.



## 목적 함수 최적화



### 기본적 버전

- 태스크의 미니배치
- 미니배치 포인트를 샘플링
- 미니배치 별 손실값 감
- 역전파
- 구해진 그래디언트를 optimizer와 함께 학습



이 과정은 데이터 양에 관계 없이 동등하게 샘플링된다는 특징이 있습니다.

따라서 데이터의 양이 다른 경우 공정하게 샘플링될 수 있도록 조정해야 합니다.



## 문제점

위 구조를 적용하는 데 적용될 두 있는 두 가지 문제점을 설명합니다.



### Negative transfer

학습이 네트워크와 무관하게 이루어져 단일 모델이 성능이 더 좋은 경우를 이야기합니다.

하나의 태스크의 데이터가 다른 태스크에 영향을 주는 상황입니다.

CIFAR-100 데이터셋의 데이터로 확인해 본 결과 단일 모델이 성능이 가장 좋았습니다..



![negative-transfer](/Users/jun/My Works/paperStudy/ML_paper_study/cs330/images/negative-transfer.png)

### 왜?

- 최적화 문제. (Cross-task interference)
  - 태스크가 다른 비율로 학습되었을 수 있음



이 문제를 해결하려면 태스크 간 공유되는 것을 줄여야 합니다.



## Overfitting

앞 문제와 반대되는 내용으로 오버피팅을 들 수 있습니다.

더 많이 공유하는 것으로 해결할 수 있다.



---

## Meta-Learning Basics



메타 러닝 알고리즘은 크게 기계적 관점, 확률적 관점 두 가지로 나뉜다.

기계적 알고리즘

- 어떻게 알고리즘이 실행되는지 알기 쉽다.
- 데이터셋을 기반으로 새로운 데이터를 예측한다.
- 메타 러닝 알고리즘을 적용하기 쉽다.

확률적 알고리즘

- 알고리즘이 무엇을 하고 있는지 알기 어렵다.
- prior information을 추출해 효율적인 학습을 위해 조율한다.
- 적은 양의 데이터에 적용 가능



## 확률적 알고리즘

베이지안 관점을 메타러닝의 베이지안 관점으로 재정의가 필요하다.

지도학습 영역에서 설명하겠다.

![mata-learning1](/Users/jun/My Works/paperStudy/ML_paper_study/cs330/images/mata-learning1.png)



문제점

- 데이터가 작으면 오버피팅 위험 이를 막기 위해 $logp(\phi)$ 가 regularizer 로 작용한다.
- 하지만 오버피팅을 막는 등의 목적에는 적합하지 않아 보인다.



베이지안을 메타 러닝 관점에서 접근해 보자

새로운 데이터를 어떻게 반영할지 -> 메타-트레인 데이터를 만들었습니다. 

 



 

![mata-learning2](/Users/jun/My Works/paperStudy/ML_paper_study/cs330/images/mata-learning2.png)

위 이미지에서 사진을 분류하는 인공지능을 만들 때, 하나의 클래스당 5개 이미지가 있는 데이터로 확인하면 기존 방식으로 모델을 학습하면 분명 오버피팅이 발생할 것입니다.



 만약 과거의 경험 $D_{meta-train}$을 계속 가지고 있지 않고 싶다면.. (태스크를 통해 능력만 배움)

메타-파라미터를 학습시켜야 할 것입니다.

메타 파라미터는 $\theta : p(\theta|D_{meta-train})$로 정의되며, 주어진 태스크를 빠르게 해결하기 위해 $D_{meta-train}$에서 배워야 할 것이라는 뜻이 됩니다.



이 경우 Output의 분포는 다음 수식으로 나타낼 수 있습니다.

![meta-learning3](/Users/jun/My Works/paperStudy/ML_paper_study/cs330/images/meta-learning3.png)

따라서 주어진 모델은 오른쪽 하단의 수식으로 분리될 수 있습니다.

두 개의 항 중 왼쪽 항은 태크스 단일에서 학습되어야 할 파라미터이며, 오른쪽 항은 메타 러닝 과정에서 공통적으로 학습되는 파라미터입니다.



## 메타러닝 학습 과정

![learning_cycle](/Users/jun/My Works/paperStudy/ML_paper_study/cs330/images/learning_cycle.png)



주어진 데이터셋 $D$에 대해서 메타 러닝 파라미터 $\theta\star$ 를 학습합니다. 이 과정을 메타 트레이닝이라고 부릅니다.

이렇게 학습된 메타 러닝 파라미터 상에서 테스트용 입력에서 출력이 나올 확률을 최대화 하는 $\phi\star$를 찾는 과정을 '메타 테스팅' 이라고 부릅니다.



메타 테스팅 시에는 특정 태스크의 데이터 모두를 입력으로 사용할 수 있지만, 메타 트레이닝 시에는 목표태스크의 테스트 데이터를 어떻게 구성해야 할 지에 대해 고민을 하게 됩니다.



![learning_data](/Users/jun/My Works/paperStudy/ML_paper_study/cs330/images/learning_data.png)

메타 트레인에 사용되는 데이터셋 $D_{meta-train}$의 경우는 $D^{tr}_i$ 와, $D^{ts}_i$ 로 구성됩니다. 전자는 $i$ 번째 태스크의 학습용 데이터, 후자는 테스트 데이터입니다.

즉 메타 학습은 $ \phi\star = f_{\theta\star}(D^{tr})$ 을 $D^{ts}_i$ 에 적합하게 만드는 과정이라고 볼 수 있습니다.



## 다른 적용 예시

이 구조는 Auto-ML이나 Architecture search에도 적용됩니다.

Auto-ML의 경우에서 $\theta$는 하이퍼 파라미터이고, 이를 통해 네트워크 가중치를 빠르게 학습시키는 것이므로 $\phi$ 는 네트워크 가중치입니다.

아키텍처 검색의 경우는 $\theta$ 는 네트워크 구조입니다. 적절한 $\theta$를 통해 빠르게 학습되는 네트워크 가중치를 찾는 것이므로 $\phi$는 네트워크 가중치입니다.

이 부분에 대한 연구도 매우 활발하게 이루어지고 있지만, 수업의 과정 이외 범위이기 때문에 다루지 않습니다.
