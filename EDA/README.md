# EDA

  ### NLP 픽 제목의 워드 클라우드 부분 [ [WORDCLOUD](https://github.com/shimjaeman/NLP-based_Recommendation_System/issues/3#issue-1625549103) ]
 
   stylecloud를 사용하여 영어와 한국어 제목을 워드 클라우드로 표현하였다.
   서비스를 이용하는 사용자가 어떤 주제에 관심이 있는지 확인하였습니다.
    
  ### NLP 클러스터링  [ [Clustering](https://github.com/shimjaeman/NLP-based_Recommendation_System/issues/5) ]
    
    단어간 군집을 살펴보기 위해서 클러스터링 기법을 사용하였습니다.
    ISOMAP과 T-SNE은 차원 축소 기법 중 하나로, 고차원 데이터를 저차원으로 변환하여 단어 간의 관계를 시각화하였다. 
    그림으로는 각각의 단어가 점으로 나타내어져 있고, 비슷한 단어들끼리 가까이 위치하도록 시각화되어 있습니다. 
    또한, 비슷한 단어들끼리 묶인 군집들이 서로 다른 색으로 표시되어 있습니다.
    이러한 결과를 바탕으로, 라벨링을 하면 데이터 분류에 정확도를 높일 수 있겠다는 가설을 세우게 되었습니다.
    
  ### NLP K-means [ [K-means](https://github.com/shimjaeman/NLP-based_Recommendation_System/issues/6) ]
 
    K-means 클러스터링을 이용하여 군집화된 단어들을 묶어보았습니다. 군집화된 단어를 기준으로 주제를 분류하는데 참고하였습니다. 
    
  ### NLP Labeling [[Labeling](https://github.com/shimjaeman/NLP-based_Recommendation_System/issues/7)]
 
    클러스터링 결과를 바탕으로 픽 제목을 보고 라벨링 작업을 해주었습니다.

  ### NLP 유사도 비교 [[유사도 비교](https://github.com/shimjaeman/NLP-based_Recommendation_System/issues/8)] 
 
    라벨링 분류를 통해서 만들어진 주제들을 유사도 비교를 하였습니다. AI주제는 개발주제와 가장 유사도가 높습니다. 
