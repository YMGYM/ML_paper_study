# MuseGAN: Multi-Track Sequential Generative Adversarial Networks for Symbolic Music Generation and Accompaniment

# Abstract
- 음악은 다른 도메인과 달리 시간적 예술, 다양한 악기 트랙, 코드/아르페지오/다성의 멜로디 등으로 구성된다.
- 본 논문은 GAN 형태의 3가지 모델을 제안한다
- 본 모델은 수 백개의 Rock 음악으로 학습시켰다
- 본 모델은 사람 개입 없이 기초부터 음악을 생성하는 것을 보여줬다.
  
# Introduction
- GAN은 이미지와 텍스트 등 영역에서 놀라운 진보를 일으켰다.
- Symbolic Music을 생성하려는 비슷한 시도가 있었지만 다음 장애에 부딛혔다.

## 음악의 어려운 점
- 음악은 시간의 예술이다.
  - 음악은 시간에 따른 계층적인 구조를 보인다.
  - 음악의 리듬, 강도 등에 따른 흐름에 큰 주목을 보인다.
- 음악은 다양한 악기 트랙으로 구성된다.
  - 이 트랙들은 종종 다른 트랙과 관련 있으며, 시간에 따라 종속적으로 연결된다.
- 음악의 음들은 코드, 아르페지오, 멜로디로 그룹화된다.
  
## 논문의 목표
- 기존 논문들은 음악을 단순화해서 생성하는 구조
  - 싱글 트랙 단선율의 음악,
  - 단선율의 멜로디를 합쳐 다선율을 만드는 음악
- 본 논문은 이런 단순화를 최대한 줄이는 방향으로 감
  - 멀티트랙 음악
  - 화성/리듬적 구조를 유지함
  - 다른 트랙과의 종속성 (화음 등)
  - 시간적 구조

## 제안내용
- 두 가지 시나리오
  - 사람의 초안을 따라 음악 생성
  - 사람 없이 음악 생성
- 트랙 간 관계를 위한 세 가지 방법
- 노트의 그루핑을 위해 마디를 한 단위로 보았고, 음들을 CNN을 사용해서 탐색
- intra-track, inter-track 한 측정 방법 두 가지 제시

# Generative Adversarial Networks
- GAN 에 대한 설명
- 생성자와 구분자로 이루어지며 G와 D의 minmax loss 를 사용함
- 최근엔 gradient panalty 를 포함한 목적 함수를 사용하기도 함 (WGAN-GP)

# Proposed Model
- 마디를 기준으로 삼음

## Data Representation
- 멀티 트랙 피아노롤 데이터를 사용했다.
- R: 시간, S : 음의 깊이, M: 트랙 수
  
## Modeling the Multi-track Interdependency
- Jammimg model : 다중 트랙별로 생성자를 따로 두는 구조
- Composer model : 하나의 생성자가 멀티 트랙을 만들어 냄. -> 하나의 구분자
- Hybrid model : 다중 트랙 생성자, 단일 구분자. inter-track, intra-track 의 정보 벡터를 따로 두고 구성

## Modeling the temporal Structure
- 기존 모델은 독립된 마디 단위의 음악만 생성하는 구조임.
- Phrase 단위의 음악을 생성할 필요가 있음
- Generation from Scratch : 시간 구조를 만들어내는 생성자를 따로 두고, 구조를 먼저 만든 뒤 구조용 latent vector을 주어짐
- Track-conditional Generation : 시간적 구조를 사람이 준다고 가정하고 남는 부분을 만드는 모델
- 