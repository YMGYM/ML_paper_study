# 딥러닝 기반의 음성합성

## HMM 대신 딥 러닝
- 어쿠스틱 모델만 딥러닝으로
- 전체 모델을 딥러닝으로?

## Linguistic feature
- Binary + numerical

## 음성합성 DNN
- HMM의 의사결정 트리 알고리즘들을 DNN으로 치환
- 파라미터 생성 등이 필요할지도..?

## RNN based
- Deep Bidirectional LSTM
- 좌우 음성을 모두 사용이 가능함
- 컴퓨팅 자원이 많이 필요함

## End-To-End 음성 합성
- 앞서 말한 부분들을 하나로 통합했다.
- 많은 연구가 이루어지고 있음

## Tacotron
- 처음으로 제안된 end-to-end 음성합성 모델
- 멜 스펙트럼까지 하나의 모델로 사용
- CBHG 모듈 사용
- Encoder, Attention-based decoder, post-processing
-  