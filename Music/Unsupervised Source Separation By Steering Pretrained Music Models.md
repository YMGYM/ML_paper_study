# Unsupervised Source Separation By Steering Pretrained Music Models

[원본 논문 보기](https://arxiv.org/pdf/2110.13071.pdf)

작성자 : [15기 안민준](https://github.com/YMGYM)

본 리뷰는 투빅스 15&16기 음성 세미나에서 동명의 논문의 내용을 정리하고 공유하기 위해 만들었습니다.

출처가 적혀 있지 않은 이미지는 모두 본 논문에 수록된 이미지입니다.

## Abstract
본 논문은 기존에 음악 생성과 태깅 모델을 그대로 사용하여 Source Seperation 모델을 얻습니다.

음악 생성 모델은 OpenAI의 JUKEBOX 모델을 사용했으며, 태깅 모델은 4 종류를 묶어서 사용했습니다.

이 논문을 통해 소스 분리 작업에서 음악 생성 & 태깅 모델의 가능성을 기대할 수 있겠습니다.

## Introduction

### 데이터셋 부족과 모델 전이(?)
- MIR 영역에서는 데이터셋의 부족으로 인해 어려움을 겪는 중이고 특히 Source Seperation(소스 분리) 모델은 well-labeled 된 데이터가 없다고 합니다.
- 기존 소스 분리 모델은 분리할 수 있는 소스의 종류의 한계가 있습니다. (Voice, Bass, Drums, "기타" - MUSDB18)
- 최근 연구들은 음악 생성 모델 등을 MIR 쪽에 적용하려는 시도를 하고 있습니다.

### 본 논문에서는
- 본 논문에서는 사전 학습된 모델이 musical source seperation 작업에 적용되는지 보일 예정입니다.
- 태깅 모델의 추론 결과를 JUKEBOX가 생성하는 방법으로 사용했습니다.
- Gradient Ascent(경사 상승법) 을 JUKEBOX의 임베딩 공간에 적용하고 디코딩된 오디오를 입력값의 마스크로 사용했습니다. (후에 자세히 설명합니다)
  
## Prior work

### 기존 방법론
- 기존 연구들은 '이미 존재하는 데이터셋에서 성능을 최대화하는 것'에 초점을 맞추어 진행했습니다.
- 가장 유명한 데이터셋인 MUSDB18은 악기 소스가 제한되어 있고, 데이터셋 크기도 너무 작아서(150개) 증강이 어렵습니다.
- 딥러닝의 발전으로 Non-negative Matrix Facotization(NMF)와 같은 비지도 방법론이 도입되었으나, 일부 휴리스틱한 알고리즘이 도입되어야 합니다.
- 반복, 화성, 타악(박자)와 같은 음악적 특징을 사용하는 시도도 있었으나, 음원의 종류에 따라 안되는 경우가 많았습니다.

### 최근 방법론
![MixIT](https://images.deepai.org/converted-papers/2006.12701/x2.png)

MixIT방법론 (https://deepai.org/publication/unsupervised-sound-separation-using-mixtures-of-mixtures)

- [Mixture Invariant Training (MixIT)](https://deepai.org/publication/unsupervised-sound-separation-using-mixtures-of-mixtures) 사용
  - Mixtures of mixtures (MoMs)를 생성하고 이를 overseparating 하는 방법(?)
  - 악기 소스가 독립적이지 않기 때문에 음악 영역에는 적합하지 않습니다.
- [VAE를 사용한 연구](https://www.music.mcgill.ca/~julian/wp-content/uploads/2021/06/2021_eusipco_vae_bss_neri.pdf)도 있으나, 학습이 어느정도 필요합니다.
- 본 논문에서 제안하는 방법은 **학습이 전혀 필요하지 않은** 방법이라고 강조합니다.
  
  
## Background
### OpenAi's Jukebox

### Automatic Music Tagging

## Proposed System

## Experimental Validation