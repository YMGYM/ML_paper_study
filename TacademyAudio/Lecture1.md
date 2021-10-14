# 오디오 신호처리 기초

## 왜 사운드?
- 음성 분류 (아리야)
- 음성 인식 (발화 인식)
- 음성 합성 (결과값)


## 컴퓨터가 소리를 이해하는 과정
- 양자화와 부호화
- Sampling rate : 1초에 몇개의 신호를 저장?
- 양자화 : float64, int 등으로 나누는 느낌으로 설명 가능
- Sampling rate가 높다고 꼭 좋은 것은 아니다.

## 소리에서 얻을 수 있는 물리량
- 표기
  - Amplitude : 진폭
  - Frequency: 주파수
  - Phase: 위상
- 물리 음향
  - Intensity : 진폭의 세기
  - Frequency: 떨림의 빠르기
  - Tone-Color : 파동의 모양
- 심리 음향 (사용자가 느끼는 것)
  - Loudness : 소리 크기
  - Pitch : 음정
  - Timbre: 음색

## 진동수
- 단위는 Hertz (1초에 진동한 횟수)
- 정현파 : 일종의 복소주기함수, 복합파 : 정현파의 합

## 푸리에 변환
- 입력 신호를 다양한 주파수를 갖는 주기함수들의 합으로 분해하여 표현하는 것
- 오일러 공식 : 지수함수 -> 주기함수
- 복소수의 절대값 : 주파수의 강도
- 복소수가 가지는 phase : 주파수의 위상


## 인간의 청각 경로
- 인간은 낮은 주파수를 더 크게 느껴진다.
- 인접한 주파수를 크게 구분할 수 없다
- 멜 필터뱅크 : 특수한 함수를 적용하여 특정 주파수를 집중적으로 추출하겠다.
- 멜 스펙토그램


## MFCC
- Mel에 log 적용 -> inverse FFT (Frequency 축을 압축했다고 볼 수 있다)
- waveform 에 가까운 모양이 된다.
- Mel 필터 뱅크가 서로 겹쳐있음 -> DCT가 잡아주는 효과가 있음
- capital cofficients ? :
  - Spectral Envalope : 주파수 영역에서 어떤 부분이 활성화가 되어 있는지 볼 수 있는 영역
  - ISFFT(Spectral Envalope) -> 스펙트럼 영역에서 spectral Envalope를 푸리에 역변환한 것과 같다.

## Data Argumentation
- Waveform Augmentation
  - pitch shift
  - value_aug
  - add noise : 생각보다 잘 안됨..
  - hpss
  - shift : 주파수를 roll(앞을 뒤로 보냄)
  - stretch : 주파수를 늘리기
  - change_speed : 속도 조절 (time-strech로 씀)
- Spectogram Augmentation
  - 주로 마스킹을 사용함
  - torch_audio transform 을 쓰는 것이 편함
- Data Split

## Data Loader
- 
