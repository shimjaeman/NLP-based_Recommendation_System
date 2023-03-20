# Modeling

<details><summary><h3>Data Preprocessing</h3></summary>

- **`DB DIAGRAM`**

  ![db diagram](https://user-images.githubusercontent.com/95950967/226321296-9b473c88-7e6c-4d4e-9ef4-28e961c84d73.png)
  
  
- **`Preprocessing`**
  * 로우 데이터에서 필요한 부분만 추출하기 위해 정규표현식을 사용하거나 nan 값을 제거하여 처리
  * AI 봇 및 사람이 직접 만든 부분은 정확도 향상을 위해 제거
  ```
  ## change pik_title
  label_pik = pd.merge(pik_label, piks, how='left', on="pik_id", suffixes=('_label', '_pik'))

  ## pik_info + cat_info
  pik_cat = pd.merge(catego, label_pik, how='inner', on="pik_id", suffixes=('_cat', '_pik'))

  ## link_info + pik_cat_info
  pik_cat_link_label = pd.merge(linkhub, pik_cat, how='inner', on='category_id', suffixes=('_link', '_catpik'))
  pik_cat_link_label.sort_values(['user_id', "pik_id", 'category_id', 'link_id'], ascending=True, inplace=True)

  ## data filtering & drop
  def dropNa_ArtificialUser(data, artificial_users, integering=True, dropna=True):
      if integering:
          data = data.astype({'pik_id': 'int', 'link_id': 'int', 'category_id': 'int'})
          data = data.loc[:, ["user_id", "pik_id", "pik_title", "category_id", "cat_title", "link_id", "link_title", "topic_label"]]

      if dropna:
          data = self_del_list(data, 'user_id', "pik_id", artificial_users)
          data = filtering_data(data,  ['link_title'])
          data = filtering_data(data,  ['pik_title'])
      return data
  ```
</details>

<details><summary><h3>Hugging Face Model</h3></summary>

- **`Purpose of Hugging Face`**
  - 데이터가 적은 문제점을 해결하기 위해서 허깅페이스의 전이 학습된 모델 사용
  
- **`Feature Extraction`**
  
  **`1. Feature Extraction Feature`**
  
   <img src="https://user-images.githubusercontent.com/95950967/226324245-1d2425f7-bf12-4116-9490-b919eff80167.png"  width="70%"  height="70%"/>
  
  - 입력된 텍스트 데이터에서 의미 있는 특징을 추출하여 임베딩 벡터로 변환
  
  - 이러한 벡터들은 pooling 기법을 통해 하나의 벡터로 만들어지며, 새롭게 들어오는 문장과의 유사도 비교
  
  - 최종적으로 각 문장과의 유사도를 비교하여 가장 유사한 문장을 추출 
  
  ***********
  **`2. Feature Extraction Coding`**
  ```
  ## Feature Extraction 
  for batch in tqdm(dataloader):
    batch = tuple(t for t in batch)
    b_input_ids, b_att_masks = batch

    ## Run the text through BERT, and collect all of the hidden states produced         
    with torch.no_grad():
            outputs = model(b_input_ids, attention_mask = b_att_masks) ##For distilbert we dont need token_type_ids
            # outputs.keys()
            embeddings = outputs.last_hidden_state # hidden_states는 각 layer의 hidden state를 모아놓은 list
            mask = b_att_masks.unsqueeze(-1).expand(embeddings.size()).float()
            masked_embeddings = embeddings * mask
            summed_emb = torch.sum(masked_embeddings, 1)
            summed_mask = torch.clamp(mask.sum(1), min=1e-9)
            mean_pooled_emb = summed_emb / summed_mask

    mean_pooled_total.append(mean_pooled_emb)
  ```
  - 하나의 주제에 해당하는 모든 URL 임베딩 값의 평균을 구하여 진행
  
  
- **`Zero-Shot Text Classification Model`**

  **`1. Zero-Shot Text Classification Feature`**

   <img src="https://user-images.githubusercontent.com/95950967/226324258-b44d1fae-5aec-4dfc-b18b-5b29e4ad9a90.png" width="75%" height="75%"/>

  - 새로운 입력값이 들어왔을 때, 주제분류 모델을 이용하여 분류 예측 결과를 산출
  - 학습 데이터에 없는 라벨에 대해서도 예측이 가능한 기계 학습 모델
  - 분류 예측 결과에 속하는 라벨을 가진 데이터만을 추출
  
    ***********
  **`2. Zero-Shot Text Classification Coding`**
  
  ```
  # title을 zero-shot-classification을 이용하여 테마 분류
  def theme_classification_piks (pipeline_name, model_name, title, labels):
      ## 16개의 라벨링 테마 분류
      candidate_labels = ["Development", "Artificial intelligence", "travel", "restaurant",  "finance",    
                       "design", "life wisdom", "social issues", "game", "sports", "cooking", 
                       "business", "marketing", "cultural life", "hobby", "education"]
      if title :
          classifier = pipeline(pipeline_name, model=model_name)
          pik_class = classifier(title, candidate_labels)

          # Scores가 높은 모델 중 top5만 뽑기
          pik_labels = []
          top5_cnt = 0
          for i, j in zip(pik_class["labels"],  pik_class["scores"]):
              # top3개만 추출
              if top5_cnt == 3:
                  break
              # 단 유사도가 0.05보다 높은 경우만
              if j > 0.05:
                  pik_labels.append(i)
                  top5_cnt += 1     
          pik_num_result = [label_dict[n] for n in pik_labels]

      return pik_num_result
  ```
  
  - 하나의 주제에 해당하는 모든 URL 임베딩 값의 평균을 구하여 진행
  
  
- **`Overall Data Flow`**
  
  ![overall data flow](https://user-images.githubusercontent.com/95950967/226324486-8464df07-2a21-45eb-8227-806c6fbe93ca.png)
  
</details>

<details><summary><h3>System Pipeline</h3></summary>

- **`개발환경`**
  - OS: window 10 / Ubuntu 22.04 LTS
  - IDE
    - Conda
    - VScode
    - spyder
  - Database
    - Nhost
    - MYSQL
  - File Server : GraphQL
  - CI/CD: Airflow, Docker, BentoML
  
- **`DataFlow`**
 
  <img src = "https://user-images.githubusercontent.com/95950967/225795060-7d5db141-7699-4f71-b083-32a20d1e993e.png" width="50%" height="50%">
  
  - 전체 파이프라인은 여러 단계를 거쳐 모델 학습과 배포를 자동화하는 것을 목표로 개발

</details>

<details><summary><h3>Model Deployment</h3></summary>

- **`Airflow Dags`**

  <img src = "https://user-images.githubusercontent.com/95950967/226339811-edeb455c-d09a-4c84-a07d-b0cc0a258a5c.png" width="80%" height="100%">
  
- **`Airflow Graph View`**

  <img src = "https://user-images.githubusercontent.com/95950967/226339817-bea90e87-dab0-471d-91cc-ffdf5f821a25.png" width="80%" height="100%">
  
- **`BentoML API`**

  <img src = "https://user-images.githubusercontent.com/95950967/226339815-7f218a28-5a24-4db0-9815-51a4ae9ff044.png" width="80%" height="100%">
  
  </details>
