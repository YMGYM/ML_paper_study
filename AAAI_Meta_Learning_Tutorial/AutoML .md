# AAAI 2021 Meta Learning Tutorial - AutoML

본 파일은 [링크](https://sites.google.com/mit.edu/aaai2021metalearningtutorial/home) 의 영상 내용을 정리해 둔 파일입니다.

개인 공부의 노트 필기용도로 작업했습니다.`



## Machine Learning

- 학습에는 여러 하이퍼파라미터가 필요하다.
- 메타 모델을 새로운 태스크에 적용할 때는 하이퍼파라미터를 고정하고 진행한다.



## AutoML

- 머신러닝 모델을 데이터 기반으로 효율적으로 설계하는 것
- 파이프라인 자체, 하이퍼파라미터를 최적화한다고 볼 수 있다.
- Neural Architecture Search : 신경망 구조 결정, 최적화 방법 설정...



## AutoML + Meta Learning

- 모든 모델을 테스트해보기에는 오래 걸린다.
- 편향을 사용해서 self-learning AutoML을 사용해 효율적으로 바꿀 수 있다.


### observation

- 학습된 우선 상태에 강하게 의존한다. (하이퍼파라미터 단순화)
- 대부분 성공적인 모델은 비슷한 파이프라인 구조를 가지고 있다.



## 모델을 선택하는 법

- RL기반의 검색 (엄청 오래걸림)
- Random Search  : 제약조건이 많으면 가능
- Weight Sharing : 모든 가중치가 공유.. : 작동한다!

