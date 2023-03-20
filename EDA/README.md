# EDA

<details><summary><h3>WordCloud</h3></summary>

- **`Korean Wordcloud`**
  - 
  <img src = "https://user-images.githubusercontent.com/114843451/226329148-b8bf129f-6ed1-43f7-b16d-7e9251c7d742.png" width="35%" height="30%">


- **`English Wordcloud`** 
  - 
  <img src = "https://user-images.githubusercontent.com/114843451/226329013-287ec90c-48dc-4c62-80ef-31d3fffd1653.png" width="35%" height="30%">
  
   stylecloud를 사용하여 영어와 한국어 제목을 워드 클라우드로 표현하였다.
   
   서비스를 이용하는 사용자가 어떤 주제에 관심이 있는지 확인하였습니다.

</details>

<details><summary><h3>NLP_Clustering</h3></summary>

- **`ISOMAP Clustering `**
  -
  <img src = "https://user-images.githubusercontent.com/114843451/226330924-b655081b-25cf-4f0f-9e67-cf3127d85c63.png" width="35%" height="30%">
  
- **`TSNE Clustering `**
  -
  <img src = "https://user-images.githubusercontent.com/114843451/226331410-4ab6cfcf-da6a-4354-b7af-9887cc7709bd.png" width="35%" height="30%">

단어간 군집을 살펴보기 위해서 클러스터링 기법을 사용하였습니다. 

ISOMAP과 T-SNE은 차원 축소 기법 중 하나로, 고차원 데이터를 저차원으로 변환하여 단어 간의 관계를 시각화하였다. 

그림으로는 각각의 단어가 점으로 나타내어져 있고, 비슷한 단어들끼리 가까이 위치하도록 시각화되어 있습니다. 

또한, 비슷한 단어들끼리 묶인 군집들이 서로 다른 색으로 표시되어 있습니다. 

이러한 결과를 바탕으로, 라벨링을 하면 데이터 분류에 정확도를 높일 수 있겠다는 가설을 세우게 되었습니다.

</details>

<details><summary><h3>K_means_Clustering</h3></summary>

- **`K_means_Clustering `**
  -
  <img src = "https://user-images.githubusercontent.com/114843451/226333929-9196f43b-2587-46c6-9ff3-e37ac9d01e35.png" width="35%" height="30%">
  
  가설을 기준으로 주제를 분류하기 위해서, K-means 클러스터링을 활용하여, 군집화 된 단어를 가지고 주제를 정하였습니다.
  
  Cluster 2를 보면 ai, ai technology, ai server, 등 ai 관련된 단어들이 나오는 것을 확인할 수 있었고,
  
  다른 cluster도 확인을 해보니 비슷한 단어들끼리 군집화 되는 것을 확인할 수 있었습니다.
  
  이러한 결과를 바탕으로  개발, AI, 여행 등 17가지 주제로 나누었습니다.

</details>


</details>

<details><summary><h3>NLP_Labeling</h3></summary>

- **`NLP_Labeling `**
  -
  <img src = "https://user-images.githubusercontent.com/114843451/226334503-9715afbb-9258-450b-98ca-0688083c88b7.png" width="35%" height="30%">
  
   클러스터링 결과를 바탕으로 픽 제목을 보고 라벨링 작업을 해주었습니다.

</details>

<details><summary><h3>NLP_Similarity</h3></summary>

- **`NLP_Labeling `**
  -
  <img src = "https://user-images.githubusercontent.com/114843451/226334764-e7cb8eb8-54a3-493f-8e18-9687bcb0b24c.png" width="35%" height="30%">
  
   라벨링 분류를 통해서 만들어진 주제들을 유사도 비교를 하였습니다. 
   
   AI주제는 개발주제와 가장 유사도가 높습니다. 

</details>



