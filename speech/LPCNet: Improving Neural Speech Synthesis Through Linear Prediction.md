# LPCNet: Improving Neural Speech Synthesis Through Linear Prediction

[원본 논문 보기](https://arxiv.org/pdf/1810.11846.pdf)

# Abstract
- 본 논문은 Linear Prediction과 RNN을 결합하여 기존 시스템보다 더 효율적인 모델을 만들어 냄
- 모바일 기기에 적용하는 것을 목적으로 함
  
# introduction
- speech synthesis 를 end-user devices 에서 사용할 수 있게 함
- neural synthesis network를 사용하지 않은 model을 제안.
  
# waveRNN
- 이전 신호와 파라미터를 사용해 현재 시간의 output Sample을 생성
- 8bits 샘플을 두개 예측 -> 시간 복잡도 감소
- 
# LPCNet
- 저주파에 신호가 집중되는 것을 막기 위해 first-order pre-emphasis filter를 적용
- 자귀회귀 모델을 통해 vocal tract response를 생성
- all-pole 모델 -> correlation으로 계산 가능 = 행렬곱으로 계산 가능
- 
# Evaluation

