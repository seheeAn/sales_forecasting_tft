# TFT를 이용한 Walmart 수요예측 
소프트웨어융합캡스톤디자인 결과물

### 과제 개요
모든 산업의 사업 기획 및 운영계획은 수요예측으로부터 출발하며, 따라서 수요예측 기법은 모든 분야에 적용가능하고 그 필용성과 범용성이 높다. 2020년 열린 M5 competition(수요예측 정확도 평가 대회) 수상자들은 과거에 비해 수요예측에서 통계적 기법, 시계열 기법 사용이 줄어들었고, ML, DL 활용이 급증했다. 이는 단순한 대회 통계를 넘어 수요예측 기법의 트렌드 흐름으로 생각할 수 있다. 따라서 본 연구에서는 최신 딥러닝 기법을 적용하여 해당 대회에서의 수요예측 성능을 향상시키는 것을 목표로했다.

### 데이터셋 및 대회설명
1941일간의 미국 3개주에 위치한 매장 10개의 실제 데이터 1941일치를 사용.  
데이터는 State > Store > Category > Department > Item의 계층구조.  
미래의 28일간의 판매량에 대한 point forecasting

### Temporal Fusion Transformer
- multi-horizon forecasting 목적으로 개발된 attention based DNN architecture
- Gating mechanism & Variable selection network등으로 각 시점마다 중요한 변수를 선별
- Direct forecasting
- Interpretability
![image](https://user-images.githubusercontent.com/49268298/207885059-e70794f3-76e4-44eb-83f6-d72a814c7d68.png)

### Training
 - CA_1 store-product 단위 판매에 대한 수요 예측 진행
- encode data = 90일 , decode data = 28일
- 1941일간의 train data중 마지막 28일을 validation으로 사용
- store, store-category data pool에서 각각 학습
- tweedie loss 사용
- store 모델에 대해 파라미터 튜닝

### Result
![image](https://user-images.githubusercontent.com/49268298/207885721-f73c475e-c677-45e4-81c4-1a4ed5b2e991.png)  
WRMSSE값을 여러 집계 level 별로 계산했을 때 개별 product 예측에서 TFT가 더 우수한 성능을 보였다.  

![image (1)](https://user-images.githubusercontent.com/49268298/207885939-9b3a86b0-1614-4d92-b2c8-a856d4642051.png)
![image (2)](https://user-images.githubusercontent.com/49268298/207886247-a5f60fc7-5fab-4a75-94fd-bc57bb8633d0.png)  
실제값과, 1위 예측값, TFT 예측값을 product, store단위로 plot한 결과는 위와같다.

-----
결론적으로 1위 기법보다 전반적으로 유사한 예측을 보였으나 store-product level에서의 성능을 향상시켰다. 향후 추가 연구를 통해 다른 매장에도 해당 예측 기법을 확장하여 적용시킬 예정이다.
