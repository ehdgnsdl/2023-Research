################ 최종 앙상블 Submission 파일 설명 ##################
Public LB 0.04217, Private LB 0.04396: 0807_Ensemble_BM3_SLMRec_ver2.csv
	- BM3 2개, SLMRec 2개로, 총 4개의 submission 앙상블
	- 각 모델 결과 csv 파일의 TOP 100 Rank에 대하여 2의 지수승으로 순서 weight를 줘서 앙상블 진행.
	- create_ensemble_submission폴더에 0723_Compute_CV_for_Ensemble.ipynb 파일로 실행.

* BM3 - 1 (Public LB 0.03954) 
 - BM3-inha-idx0-top100-ndcg50-0.0-Aug-06-2023-23-29-56.csv
 - all_inha.inter 사용 (전체 dataset)
 - epoch 400
 - 하이퍼파라미터 설정
"""
embedding_size: 512
feat_embed_dim: 512
train batch size: 65536
LR: 0.001

n_layers: [1]
dropout: [0.3]
reg_weight: [0.01]

cl_weight: 2.0
"""

* BM3 - 2 (Public LB 0.03827)
 - BM3-inha-Aug-04-2023-21-33-10-['n_layers', 'reg_weight', 'dropout', 'seed']-(1, 0.01, 0.3, 999)-50.csv
 - inha_by_taehoon.inter 사용
 - epoch 400
 - 하이퍼파라미터 설정
"""
embedding_size: 512
feat_embed_dim: 512
train batch size: 65536
LR: 0.001

n_layers: [1]
dropout: [0.3]
reg_weight: [0.01]

cl_weight: 2.0
"""


* SLMRec - 1 (Public LB ?)
 - SLMRec-inha-Aug-07-2023-04-19-09-['learning_rate', 'ssl_temp', 'ssl_alpha', 'reg', 'seed']-(0.0001, 1.0, 0.01, 0.01, 999)-50.csv

['learning_rate', 'ssl_temp', 'ssl_alpha', 'reg', 'seed']-(0.0001, 1.0, 0.01, 0.01, 999)



* SLMRec - 2 (Public LB ?)
 - SLMRec-inha-Aug-07-2023-02-27-12-['learning_rate', 'ssl_temp', 'ssl_alpha', 'reg', 'seed']-(0.0001, 1.0, 0.01, 0.0001, 999)-50.csv

['learning_rate', 'ssl_temp', 'ssl_alpha', 'reg', 'seed']-(0.0001, 1.0, 0.01, 0.0001, 999)


################ Submission 파일 정리 ##################
Public LB 0.04217: 0807_Ensemble_BM3_SLMRec_ver2.csv
	- BM3 2개, SLMRec 2개 submission 앙상블


Public LB 0.03827: submission_cv00363.csv
	- 단일 BM3 모델 성능

#################### BM3 모델 설명 ####################
* Public LB 0.03954 submission 파일 제작 설명
 - all_inha.inter 사용 (전체 dataset)
 - epoch 400
 - 하이퍼파라미터 설정
"""
embedding_size: 512
feat_embed_dim: 512
train batch size: 65536
LR: 0.001

n_layers: [1]
dropout: [0.3]
reg_weight: [0.01]

cl_weight: 2.0
"""

* 학습 방법
cd BM3 -> cd src -> "python main.py -m BM3 -d inha" 명령어 실행


* submission 파일 제작법
모델 학습 후 -> BM3 -> src -> recommend_topk -> Analysis_submission.ipynb 실행 
 -> 'df = pd.read_csv('BM3-inha-idx0-top50-ndcg50-0.0-Aug-06-2023-16-34-20.csv', sep='\t')'에 해당하는 파일 이름을 대입.
     단, 'BM3-inha-idx0-top50-ndcg50-0.0-Aug-06-2023-16-34-20.csv' 파일을 csv파일로 다시 저장해야함.
 -> 나머지 실행하여 제출을 위한 submission 파일 제작 완료


* submission 파일: submission_cv00363.csv

#################### SLMRec 모델 설명 ####################
* 학습 방법
cd SLMRec -> cd src -> "python main.py -m SLMRec -d inha" 명령어 실행

csv폴더에 자동적으로 top50 / top100 submission용 파일 생성

앙상블에 사용한 csv 모델 하이퍼 파라미터

['learning_rate', 'ssl_temp', 'ssl_alpha', 'reg', 'seed']-(0.0001, 1.0, 0.01, 0.01, 999)
['learning_rate', 'ssl_temp', 'ssl_alpha', 'reg', 'seed']-(0.0001, 1.0, 0.01, 0.0001, 999)






