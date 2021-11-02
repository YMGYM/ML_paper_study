# 음성 합성
- 텍스트를 읽어서 음성으로 변환해주는 것
- 정보량이 적은 곳에서 많은 곳으로 변환
- Intelligibility : 합성된 음성이 또박또박 발음되는지
- Naturalness : 얼마나 자연스러운지

# SPSS
- 통계적 접근
- text-processing - 피처 추출 - 웨이브폼 변환
- 어쿠스틱 모델에 따라 HMM, 뉴럴넷으로 나뉘어짐
- 에러 축적 한계 존재

# End-To-End
- 에러 축적 방지를 위해 처음부터 끝까지 한 번에 진행함

# Unit-Selection Based
- 딥러닝 이전의 방법
- 작은 speech unit을 쪼개고 이를 합쳐서 잇는 방법으로 구현함
- Unit (syllable, Diphones)로 나눔
- 최단거리 찾기 알고리즘(그래프) 방법으로 연결? - Viterbi 알고리즘, 빔서치 알고리즘을 사용
- 타겟 코스트, 연결 코스트 두개로 나눠서 사용
- 인터풀레이션 사용

# HMM (Hidden Markov Model)
- 확률 모델(생성 확률)
- HMM의 가정
  - 현재 상태는 바로 직전 상태에만 영향
  - 현재의 관측은 이전 state에 영향을 받지 않는다
- 사용 확률
  - state transition probability
  - output probability
  - initial state probability

## 구성
- Speech DB
- 파라미터 추출, 레이블링
- HMM 트레이닝
- Tree-based Clustering : 결정트리
- Acustic Models
- Text analysis : 텍스트 피쳐 추출
- Model Construction : 텍스트가 어떤 음성에 매치되는지
- Feature parameter generation
- Vocoder : 웨이브 생성

## 학습
- 앞 자음, 상황 맥락에 따른 피치 차이 등 많은 차이가 있음
- 피처 추출 : Source-Filter 모델링, 피치 정보 (F0), 강세 정보 (C0), Duration Data (미리 가공) - 수동 레이블링해서 넣어 줌 (시간을)
- 텍스트 분석 : 읽을 수 있는 문장을 컴퓨터 형태로 변환; 음소로 어떻게 바꿀 것인가
- HMM : acoustic Model을 학습 Baum-Welch 알고리즘(평균, 분산 추출)
- DT clustering : 주어진 음이 비음, 유음 경음 등등.. 으로 트리 분석(?) - 세세한 발음을 신경쓰지 않고 대표 발음으로 하는 편
- 파라미터 생성 : 텍스트 피쳐를 주어졌을 때 HMM state sequence 를 만듬 (DT를 통해 구한 상태를 연결함) , 필터를 통해 스무딩 과정-> DT에서 상태를 어떻게 추출하는지 모름..
  - 스무딩; parameter generation method - 피처가 나올 가능성을 최대화시키는 방식으로 구함
  - (?) 옆과 자연스럽게 이어짐 : 조건부확률이 가장 높다는 뜻?