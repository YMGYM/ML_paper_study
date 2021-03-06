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
- Seq2Se1처럼 이전 결과가 다음 입력값

### LSA (Local Sensitive Attention)
- 하이브리드 접근
- 텍스트의 내용 뿐 아니라 이전 시간 입력도 포함(위치 정보)
- 오류가 발생 가능한 부분 있음 (정적인 필터)

### Dynamic Convolutional Filter(DCA)
- **모노토닉한 어텐션 (왜?)**
- Static filter 문제를 해결하기 위해 다이나믹한 필터 제안
- 다중 화자로 구성되면 아예 안되는 경우가 있음

## Tacotron2
- Stop Token 사용 (기존에는 최대 길이) - 원하는 대로 사용
- Wavenet Vocoder 사용 - 기존보다 성능 향상
  
## Transformer TTS
- 학습이 빠름 (효율이 높음)
- 기타 트랜스포머의 장점 활용은 잘 모르겠음
- 