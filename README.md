2022-1 DSCover 4조 사회 서비스 기획

-프로젝트 주제

전국 17개 시도별 태양광 발전량 예측

-프로젝트 배경

전세계적으로 환경과 기후 변화에 대한 관심이 많아지면서 기존의 화석연료를 신재생에너지로 대체하려고 하고 있음. 

하지만 신재생에너지는 그 특성상 발전이 일정하지 않고 기상 조건의 영향을 크게 받아 에너지 계획을 수립하기 위해서는 에너지 수급 예보가 필수적으로 요구됨.

따라서 여러 국가들과 유관 기관에서 태양광, 풍력 등의 신재생에너지 발전량을 예측하려는 시도가 활발히 진행 중에 있음.

본 프로젝트는 신재생에너지를 에너지원으로서 사용하기 위한 첫 번째 단계인 에너지 예측을 시도해보았다는 것과, 

태양광 발전량을 환경 및 경제적 지표로 환산해 배경지식이 없는 사람들이라도 태양광 발전량이 실생활에 어떤 영향을 미치는지 파악할 수 있도록 한다는 것에 의의가 있음.

-데이터 전처리 및 모델링 과정

사용한 데이터 : 한국전력거래소 지역별 시간별 태양광 발전량 + 기상청 지상(종관, ASOS) 일자료 조회 서비스 + 에어코리아 최종확정 측정자료

위 세 데이터들을 2016년~2020년의 기간으로 가공해 한 데이터프레임으로 만들었음.

그 뒤 발전량 데이터들 중 발전량이 0인 것과 정규분포표상 3sigma 밖에 위치한 데이터들을 이상치로 규정해 제거했음. 그 뒤 남은 데이터들을 모델 학습에 사용.

날짜, 지역 변수들을 Label Encoding함. Label Encoding 결과값들간 크기가 모델 학습에 영향을 줄 수 있을 것 같다는 생각에 One-Hot Encoding을 추가로 진행.

이외의 feature 변수들에 대해서는 min-max scaler를 적용했고 target 변수인 발전량에 대해서는 로그 정규화 적용.

참고) 다양한 정규화 조합들을 시도해본 끝에 가장 성능이 좋은 조합들을 선정한 것임.

모델의 성능 개선 정도를 파악하거나 GridSearchCV module로 하이퍼파라미터 조합을 탐색해 조합별 성능을 비교할 때 mae, rmse, rmsle지표들을 종합해 사용했고,

그 중 rmsle지표가 가장 이상치에 덜 민감한 것으로 알려져 있어 rmsle지표를 기준으로 모델 성능을 비교하고 하이퍼파라미터 조합을 선정함.

또한 rmsle 지표를 기준으로 모델간 결과값 앙상블인 submission ensemble 진행. 이 앙상블로 인해 성능이 소폭 향상되었음.

그 뒤 gui에 학습된 모델을 넣고 서비스를 구현했음.


발표자료 : https://drive.google.com/file/d/1sgfI5QHeHN14p4FXCe19zNI7KHhpsYjX/view?usp=sharing
