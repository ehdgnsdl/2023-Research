# 주제

- 멀티모달 데이터 기반 추천 시스템 (Multi-modal Recommender System)

# Background

- 추천 시스템은 사용자의 정보를 분석하여 사용자에게 적합한 상품을 추천해주는 인공지능 기술 중 하나
- 추천 시스템 기술을 통해 사용자 편의성 증가 및 사용자의 상품의 접근성을 높여 기업의 이익 증대를 기대
- 추천 시스템은 주로 사용자의 상품에 대한 선호도 정보를 사용하지만, 데이터 수집의 어려움으로 Data Sparseness나 Cold Start 문제가 발생함. 이를 보완하고자, 최근 사용자 로그 정보 뿐만 아니라 이미지 혹은 리뷰 정보를 결합하여 Multi-modal 데이터 기반 추천 시스템 연구가 다수 진행되고 있음.
- 인하대학교 인공지능융합연구센터에서는 본 챌린지를 통해 다양한 Multi-modal 데이터를 기반으로 높은 성능의 추천 알고리즘을 개발하는 것을 목표로 함

# Summary
![StudyOverview](https://github.com/ehdgnsdl/2023-Research/assets/87434001/6fb18f91-df43-4446-b8d1-bcbb07a295e3)

Study Overview
- 서로 다른 하이퍼파라미터 BM3 모델 2개, SLMRec 모델 2개를 앙상블 하여 최종 submission 제작
- Public LB: 0.04217
- Private LB: 0.04396
- **Prize: 대학원생 트랙 부분 대상**

## (0). Competition Metric

평가 산식 : **NDCG@50(Normalized Discounted Cumulative Gain)**

![metric](https://github.com/ehdgnsdl/2023-Research/assets/87434001/7768454f-d931-488d-9f1a-422d82b61356)



## **(1). Data Description**
![Dataset](https://github.com/ehdgnsdl/2023-Research/assets/87434001/b4e43a1d-b930-483b-9476-70aab9ad1a28)
About Dataset

- train.csv
    - user_id, item_id, rating 정보가 들어가 있는 csv파일
- image.npy
    - item_id와 매핑되는 item의 이미지 feature 데이터
- text.npy
    - item_id와 매핑되는 item의 리뷰 feature 데이터
- user_label.npy / item_label.npy
    - 분석을 위한 라벨 관련 정보 (정답 라벨의 라벨 의미가 아님)

[2023 인하 인공지능 챌린지](https://dacon.io/competitions/official/236113/data)

**2023 인하인공지능 챌린지**

[2023 인하 인공지능 챌린지](https://dacon.io/competitions/official/236113/overview/description)

## **(2). Data Split Strategy(CV, Cross Validation)**

- Random Split 방식을 사용
    - 192403명의 각 유저당 하나의 item을 뽑아서 validation set으로 사용

## **(3). Method**

### **(3) - 1. BM3 Model**
![BM3](https://github.com/ehdgnsdl/2023-Research/assets/87434001/3ffe85fa-99fd-4a4a-8600-1349bb02c6e2)

BM3 Overview

- Contrastive Learning 방식
- 논문 참고: https://arxiv.org/abs/2207.05969
- 코드 참고: https://github.com/enoche/BM3

### **(3) - 2. SLMRec Model**

![SLMRec](https://github.com/ehdgnsdl/2023-Research/assets/87434001/edf218b3-1a22-4e93-97d6-ac12293d846d)

- Self-supervised Learning 방식
- 논문 참고: https://ieeexplore.ieee.org/document/9811387
- 코드 참고: https://github.com/zltao/SLMRec

## **(4). Model**

## **BM3**

hyperparameter

| Embedding | n_layers | dropout | reg_weight | cl_weight | learning_rate |
| --- | --- | --- | --- | --- | --- |
| 512 | 1 | 0.3 | 0.01 | 2.0 | 0.001 |
| 512 | 1 | 0.5 | 0.01 | 2.0 | 0.001 |

**Best public LB: 0.0395**

## SLMRec

| ecdim | layer_num | ssl_task | reg | ssl_alpha | ssl_temp | dropout | learning_rate |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 64 | 3 | FAC | 0.01 | 0.01 | 1.0 | 0.3 | 0.0001 |
| 64 | 3 | FAC | 0.0001 | 0.01 | 1.0 | 0.3 | 0.0001 |

**Best public LB: 0.0340**

## **(5). Ensemble**

- **Method:** Weighted voting
    - TOP 100의 item list를 가지고 Rank에 따라 지수승의 Weight를 부여함.
- **Rank weight:**
    
    $$
    2^{100-rank}
    $$
    

## **(6) Result**

![Result](https://github.com/ehdgnsdl/2023-Research/assets/87434001/571be5a9-7146-406a-ac90-cffbb1d850e4)

- Public LB: 0.04217
- Private LB: 0.04396
- Prize: 대학원생 트랙 부분 대상
