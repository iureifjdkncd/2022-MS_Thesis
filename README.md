## 석사학위논문 정리 

### 디렉토리 구조
- `1.) CNN-LSTM_36개월-확률분포추정.ipynb`: 확률분포추정 예시
- `2.) CNN-LSTM_36개월-예측.ipynb` : 예측모델링 예시1
- `3.) CNN-LSTM_12개월_예측.ipynb` : 예측모델링 예시2
---

### 문제 정의

- 1.) 월별 물동량 데이터를 활용한 Multi-Horizon & Uncertainty Forecasting 구
---

### 주요 전처리 
  - 1.) 2000.01 ~ 2022.06 다변량 데이터 수집

    <img width="386" height="193" alt="화면 캡처 2025-08-04 170710" src="https://github.com/user-attachments/assets/faebcd49-60b7-4557-ba69-6c5b5fcc032c" />


  - 2.) Train / Test & 데이터 정규화, Multi-Horizon 정의

    <img width="188" height="56" alt="train_test" src="https://github.com/user-attachments/assets/205662af-7aa7-477a-9633-219dd4bc9c13" />

    <img width="388" height="144" alt="화면 캡처 2025-08-04 170550" src="https://github.com/user-attachments/assets/39bf463c-f461-4ed5-9422-c19bcd9b9b0f" />

    <img width="272" height="247" alt="화면 캡처 2025-08-04 171406" src="https://github.com/user-attachments/assets/c268851e-68d6-4924-9de4-9922b168050d" />

    <img width="365" height="356" alt="화면 캡처 2025-08-04 171704" src="https://github.com/user-attachments/assets/83f9cca3-8d8c-4cc1-bd93-4c267a14b40e" />


---
### 핵심 프로세스 1 예시 (Uncertainty Quantification)

  - 1.) Monte Carlo Dropout 기반 Encoder-Decoder 확률분포 추정 예시

       → 실제 물동량 분포 기준 MCD=0.8 & N=30 Uncertainty Distribution 적합도 확인 

    <img width="269" height="136" alt="화면 캡처 2025-08-04 172701" src="https://github.com/user-attachments/assets/55920270-6a6b-4eb7-8329-5cf3704554d3" />

       → CNN-LSTM Best Layer 구조로 확인 

  - 2.) Monte Carlo Dropout 기반 Encoder-Decoder 예측 예시  

       → Gaussian & Quantile Uncertainty (MCD N=30 & mean/median)

       → Mean/Median은 점추정값으로 정의

    <img width="420" height="120" alt="다운로드" src="https://github.com/user-attachments/assets/191c3938-7078-4b2f-99f0-3c35b174cb5a" />


    <img width="448" height="130" alt="화면 캡처 2025-08-04 172213" src="https://github.com/user-attachments/assets/4d2d8457-a104-41fb-80a8-bb5d8dd7bec1" />

    <img width="449" height="120" alt="화면 캡처 2025-08-04 172234" src="https://github.com/user-attachments/assets/603db172-1aa0-4024-bf50-37484e88f25b" />

   - 3.) 전체 Horizon 종합 평균 성능 평가

       → Gaussian & Quantile Uncertainty Estimation 중 최종 택1

       → CRPS기반 Best Model구조 확인 (CNN-LSTM)

     <img width="395" height="226" alt="화면 캡처 2025-08-04 173230" src="https://github.com/user-attachments/assets/73f88644-00b3-4f4b-aa77-d38cf16f6307" />


       → Best Model & 통계기반 Multi Horizon, One-Step Ahead DL 비교

       <img width="404" height="225" alt="화면 캡처 2025-08-04 173607" src="https://github.com/user-attachments/assets/e49ed487-45e1-457a-8366-5ad09be690e7" />
--- 

### 핵심 프로세스 2 예시 (Prior Individual Forecasts from Uncertainty Quantification)

  - 1.) Scenario Forecast 기준 설정 

       → 각 예측Horizon마다 MCD CNN-LSTM Encoder-Decoder의 평균값 정의 (Trend 가정)

       → 기존 물동량의 고유 순환성 (Seasonality) 추출 

       → Horizon마다 Mean(Trend) x Seasonality값을 기준으로 선정 

     <img width="407" height="99" alt="화면 캡처 2025-08-04 174016" src="https://github.com/user-attachments/assets/dae23746-94db-44e3-a34d-f06d964d1499" />

      

  - 2.) Scenario Forecast 후보 출력

       → Horizon 기준과 MCD 확률적 추정값들 비교 (Euclidean,JS Dist, DTW)

       → 최근접 5개값 집합 개별 Horizion마다 출력 

       → 기존 물동량 대비 최근접 MCD개별 추정값들이 적어도 1개 이상 집합 존재여부 확인

    <img width="399" height="327" alt="화면 캡처 2025-08-04 174730" src="https://github.com/user-attachments/assets/5f7bdc43-7110-4de1-98e1-ec5e9d81a458" />

    <img width="322" height="385" alt="화면 캡처 2025-08-04 174859" src="https://github.com/user-attachments/assets/32caae4e-8c94-4eca-94f3-f8d4b972f47a" />

### 향후 예측 예시 



  

---
