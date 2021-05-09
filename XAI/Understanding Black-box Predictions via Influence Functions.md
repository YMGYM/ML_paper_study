# Understanding Black-box Predictions via Influence Functions - Pang Wei Koh, Percy Liang

본 자료는 빅데이터 동아리 Tobigs 12기 안민준의 XAI 심화세미나 활동으로 작성되었습니다.

본 자료는 동명의 [논문](https://arxiv.org/abs/1703.04730) 의 내용을 정리하고 이해하기 위해 작성되었습니다.

출처가 적혀 있지 않은 이미지는 모두 논문의 자료입니다.

## Abstract

- 블랙박스 형태의 모델을 해석하기 위해 본 논문은 influence function을 사용했다.
- 모델의 예측을 트레이싱해서 가장 영향을 주는 포인트를 가지는 부분을 찾아낸다.
- Influence function은 선형 모델 뿐 아니라 다양한 형태의 모델에도 유효한 것을 확인했다.