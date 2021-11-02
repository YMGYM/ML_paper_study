# Audio auto tagging
- 어떤 레이블이 사운드에 연결되는지 인식 필요
- 굳이 한개의 클래스로 연결될 필요가 없다
- Average precision 정확도를 사용 (정보 검색에서 자주 사용함)
- 피쳐들을 뽑아낼 필요성이 있음
  
# 구조
- 입력 : 오디오 샘플, 파워 스펙토그렘, 로그 스펙토그램, 멜 스펙토그램
- 아키텍쳐 : Sample Level CNN, 1D CNN, 2D CNN, CRNN
- Losses: BCEWithLogitsLoss

# 실습
- 타임 축을 맞춰 주어야 함 (자르든, 늘리든..)
- 