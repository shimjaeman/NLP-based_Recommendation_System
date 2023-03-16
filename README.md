# ASAC 기업프로젝트

## 🗸 NLP 기반 링크 추천 시스템 개발 (23.02.15 ~ 23.03.09)

### 0. 개요 
**NLP 기반 링크 추천 시스템**은 기존의 서비스를 이용하는 사용자가 

저장한 데이터 중에서 유사도가 가장 높은 객체를 추천해주는 시스템이다.

### 1. 참여 인원 및 역할 
|                이름                           |                  역할                  |
| :--------------------------------------------:| :------------------------------------: |
|  [손용원](https://github.com/ywonson)         |          Full Stack Developer          |
|  [심재만](https://github.com/shimjaeman)      |        Machine Learning Engineer       |
|  [손태산](https://github.com/steadyfox2)      |      Project Manager, Data Analyst     |

### 2. Tech Stack
<div align=left> 
 <img src="https://img.shields.io/badge/python-3776AB?style=for-the-badge&logo=python&logoColor=white"> 
 <img src="https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white">
 <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white">
 <img src="https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=Next.js&logoColor=white">
 <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=PyTorch&logoColor=white"><br/>
 <img src="https://img.shields.io/badge/Slack-000000?style=for-the-badge&logo=Slack&logoColor=white">
 <img src="https://img.shields.io/badge/Airflow-017CEE?style=for-the-badge&logo=Airflow&logoColor=white"> 
 <img src="https://img.shields.io/badge/BentoML-FF61F6?style=for-the-badge&logo=BentoML&logoColor=white">
 <img src="https://img.shields.io/badge/Hugging_Face-ECD53F?style=for-the-badge&logo=HuggingFace&logoColor=white">

## 🗸 프로젝트 진행

### 0. 문제 정의 및 목표
  - 문제 정의 : 기존 추천 시스템은 데이터가 부족하여 사용자가 원하는 정보를 적절히 추천해주지 못함 

  - 목표 : 문제를 해결하기 위해, 전이학습 모델을 활용하여 사용자가 원하는 추천 정보를 제공하는 것
 
### 1. 데이터셋
  1. Piks_Data : 사용자가 만든 주제와 관련된 데이터
  
  2. Category_Data : 각 주제를 카테고리로 나누고, 해당 카테고리 안에 링크를 담을 수 있도록 생성된 데이터
  
  3. Links_Data : 주제와 카테고리에 맞게 URL 주소 및 해당 URL의 이름을 저장한 데이터
 
  4. Data Train Structure [ [Data Structure](https://github.com/shimjaeman/NLP-based_Recommendation_System/issues/4) ]

### 2. 프로젝트 파일 구조
```
.
├─dags
│  ├─bentoml
│  │  └─link_rec_bento
│  │      └─__pycache__
│  ├─data
│  ├─functions
│  │  └─__pycache__
│  └─__pycache__
├─logs
│  ├─dag_id=link_rec_airflow
│  │  └─run_id=manual__2023-03-08T07_22_16.398594+00_00
│  │      ├─task_id=calculate_emb_vector
│  │      ├─task_id=clear_bento
│  │      ├─task_id=create_bento
│  │      ├─task_id=linktitle_data_to_torch
│  │      ├─task_id=make_bento_model
│  │      ├─task_id=piktitle_data_to_torch
│  │      ├─task_id=raw_data_preprocess
│  │      ├─task_id=save_processed_data
│  │      └─task_id=serve_bentoml
│  ├─dag_processor_manager
│  └─scheduler
│      └─2023-03-08
│          ├─bentoml
│          │  └─link_rec_bento
│          ├─data
│          └─functions
└─server
    └─db

```

### 3. 구현

### 4. Conclusion

### 5. 참고논문 및 사이트
  * [Docker](https://docker-curriculum.com/)
  
  * [Airflow](https://www.bucketplace.com/post/2021-04-13-%EB%B2%84%ED%82%B7%ED%94%8C%EB%A0%88%EC%9D%B4%EC%8A%A4-airflow-%EB%8F%84%EC%9E%85%EA%B8%B0/)
  
  * [BentoML](https://docs.bentoml.org/en/latest/)
  
  * [Hugging Face](https://huggingface.co/docs/transformers/main_classes/pipelines)
  
  * [Zero-shot Text Classification](https://arxiv.org/abs/2210.17541)
  
  * [Few-shot Text Classification](https://arxiv.org/abs/2103.07552)
 
  * [Feature Extraction](https://huggingface.co/tasks/feature-extraction)
