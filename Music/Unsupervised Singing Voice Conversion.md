# Unsupervised Singing Voice Conversion

## Introduction

본 논문은 한 가수의 목소리를 다른 가수의 목소리로 변환하는 Singing Voice Conversion 작업을 수행한다.

이 논문에서 unsupervised란 가사, 음표, 발음, 가수 등 '메타데이터'를 사용하지 않았다는 것을 의미한다.

## Related Works
- WaveNet부터 시작. paralled data 을 사용하지 않는 방식이 유사하다.
- VQ-VAE의 quantized latent space를 더욱 발전시켜 domain confusion loss를 사용했다.
- Singing Synthesis and Conversion처럼 일상 대화를 학습 데이터로 사용했다.
- Backtranslation방법을 이용해서 source singer 에 가까운 학습 데이터 생성
- Mixup Training: 두 개의 샘플을 합쳐서 새로운 가상 Sample을 만들었다. 