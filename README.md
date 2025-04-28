# K-AI_Contest

이 프로젝트는 2023 제 3회 K-인공지능 제조데이터 분석 경진대회에서 183팀 중 장려상(4등)을 수상한 데이터 분석 프로젝트입니다.
프로젝트의 목적은 인공지능 중소벤처 제조플랫폼(KAMP) 내 등재된 제조AI데이터셋을 활용하여 중소 제조기업이 직면할 수 있는 문제를 해결하거나 개선할 수 있는 우수한 인공지능 분석 모델을 개발하는 것입니다.

공모전 url : https://www.kamp-ai.kr/contestAssignInfo?CPT_SEQ=20


데이터셋 : 열처리 품질보증 제조AI데이터셋
https://www.kamp-ai.kr/aidataDetail?AI_SEARCH=%EC%97%B4%EC%B2%98%EB%A6%AC+%ED%92%88%EC%A7%88%EB%B3%B4%EC%A6%9D&page=1&DATASET_SEQ=60&DISPLAY_MODE_SEL=CARD&EQUIP_SEL=&GUBUN_SEL=&FILE_TYPE_SEL=&WDATE_SEL=

본 프로젝트에서는 아래 사항들을 기반으로 모델링을 진행하였습니다.
- 배정번호 별로 불량률에 따라 불량 공정, 정상 공정으로 정의 후 라벨링 진행, 60초 단위의 time series로 데이터셋 구성
- 불량 레이블 1,569개, 정상 레이블 34,943개로 불균형한 데이터셋으로 인한 과적합을 방지하기 위한 다운 샘플링
- LSTM, GRU, TCN, Transformer을 기반으로 학습
- 가장 성능이 좋은 모델을 기반으로 shapley value를 계산해 불량에 기여하는 변수를 파악


# code 폴더
- 모델 별 / 정상 공정 데이터 개수 별 모델링 코드(jupyter)
- ex) 3000_TCN의 경우 3000개로 다운샘플링된 정상 데이터과 기존 불량 데이터를 포함한 데이터셋을 이용하여 TCN 모델을 학습한 코드
- EDA.ipynb에 간단한 데이터 시각화 및 데이터 파악 코드 포함
  
# code 설명
  - Utils & preprocess : 각 공정 별로 60초 단위의 window 추출, scaling, Dataloader, test와 plot 함수 정의
  - Model : 모델 구조 정의
  - trainer : train, validation 코드 정의
  - Main : 데이터 전처리 실행 후 모델링, 성능 확인
  - Explain (4000_GRU 만 해당) : 각 예측값에 대해 변수 기여도 확인 코드

# model_weight
- code에 있는 모델들에 대하여 각각 validation loss가 가장 작을 때의 best_weight 저장된 폴더

# 모델링 결과
- 정상 데이터 4000개로 다운샘플링한 데이터셋을 사용하여 GRU를 학습한 경우 가장 좋은 성능을 보임
- 해당 모델에 대해 shaley value 적용하여 예측에 영향을 준 변수들의 기여도를 확인할 수 있음
![K-AI 성능](./K-AI%20성능.JPG)
- 자세한 전처리 과정과 실험 세팅은 첨부된 보고서 p.17 ~ p.21에 서술
