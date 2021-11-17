# 강의 내용
## 음성에서 다루는 Task
- 음성 인식 : 음성을 하나의 인터페이스로 사용하기 위한 필수적 기능
- 음성 합성 : 텍스트를 음성 신호로 변환
- 화자 인식 : 입력된 음성 신호가 어디서 왔는지
- 음성 향상


## 디지털 신호처리
- 아날로그 신호를 기계가 다룰 수 있는 디지털 신호로 바꿔주는 작업
  
## Vocoder
- 멜 스펙트로그램은 Phase 를 포함하지 않으므로
- 이를 생성해야함


##  Deep Generative Model
- 자가회귀 모델
- GAN
- VAE
- Normalizing Flow : 함수를 역변환하여 음성을 복원시키는 모델로 이해

- Log likelihood를 줄이기 위해 KL-Divergence를 손실 함수로 표현
- 위 식에서 KL-Divergence 를 최소화 시킬 수 있도록 학습시킨다. (음수로 바꿔서 학습 = negative log likelihood)


## Autoregressive Model
- 과거 상태를 기반으로 하여 미래를 예측하는 모델

## 그래프 모델
- 고차원 데이터일수록 학습 파라미터가 매우 커지는 문제점이 있음, 모델마다 독립적으로 훈련해야 함

## RNN-Based approach
  
## PixelCNN
- Autoregressive 모델을 어떻게 하면 CNN으로 모사할 수 있을까..
- Blind spot 이 발생하는 문제가 생길 수 있다.

## WaveNet
- 왼쪽에 패딩, 오른쪽으로만 stride : 시간 축을 표현하는 데 좋다. (casual)
- receptive field 를 효율적으로 넓힘 (Dilated)

## Flow-based Model
- 자코비안 행렬식을 활용해서 역함수를 구할 수 있다.
- Z0을 가우시안에서 추출하여 역변환하는 방법으로 빠르게 샘플링 할 수 있다.
- z변수들의 sequence : Flow
- 두 가지 조건 필요
  - invertable
  - Jacobian Determinant 계산이 쉬워야 한다.
- 두 가지 조건을 만족시키기 위해서 Affine Coupling layer 생성함

## Glow
- 깊은 flow 네트워크
- Actnorm 도입 : 정규화를 그대로 수행할 때 발생하는 비효율성 해결

## WaveNet Vocoder
- WaveNet이 Vocoder가 될 수 있도록 수정함
- Mel-spectogram을 upsample
- 훨씬 긴 길이의 음성 신호 합성이 장점
- 샘플링 속도가 느린게 단점

## FlowWaveNet
- Wavenet보다 부족하지만 속도가 매우 빠르다

## WaveGlow
- 마찬가지로 엄청 빠름
- FlowGlow와 차이점 : 채널 섞는 방법이 다르다. 배치정규화 사용 안함.

## Parallel Wavenet
- 지식 전도 - 부모의 지식을 가져오는 작은 모델을 만드는 방법
- 파라미터 수가 줄어들어 샘플링 속도가 빨라짐
