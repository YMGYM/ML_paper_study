# Source-Filter Model
- 성대에서 나온 공기에 필터를 위해서 소리를 만든다.

# Glottal Waveform Model
- Source 
- 성대는 천천히 열리고 빨리 닫히기 때문에 독특한 모양이 생김
- 수학적인 모델링이 가능하다.

# Vocal tract
- filter 역할
- 튜브 모양으로 전달
- formant : resonance frequency

# Filter 추정
## Linear Prediction
- Autoregressive
- LPC : LP를 통해 추정된 값을 Quantization
- Error minimization, Autocorrelation 방법으로 최적화
- 적당한 수의 LPC를 구해야 함(하모닉스 모델링 때문)

## Cepstrum Analysis
- Homomorphic system - 컨볼루션을 더하기로 바꿔주는 시스템
- 셉스트럼 : 푸리에 -> 로그 -> 역푸리에
- 왜 로그 -> Envelope: 천천히 변하는 성분 , 하모닉스 : 빠르게 변하는 성분 -> 로그를 통해서 분리하고,,
- 역 푸리에 변환을 하면 인벨롭: 저주파, 하모닉스: 고주파

## MFCC
- pre-emphasis : 노이즈에 강인한
- Mel-filterbank
  
## Mel generalized Ceptrum
- 곱해지는 범위에 따라 LPC인지, 스펙트럼인지..

# Speech Production
- 소스와 필터 두 정보가 모두 필요
- 소스 : Excitation
- 필터 : LPC, Cepstrum 분석을 통해서 구함