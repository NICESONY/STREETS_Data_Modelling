
**STREETS** 데이터셋은 시카고 교외 지역의 교통 흐름을 모니터링하기 위해 개발된 독창적인 카메라 네트워크 기반 데이터셋으로, 약 100대의 카메라를 통해 **400만 장 이상의 이미지**를 수집하여 교통량을 분석합니다. 교외 지역의 복잡한 교통 흐름을 이해하기 위해, 데이터셋은 웹 카메라에서 촬영된 이미지 데이터를 기반으로 교통 상태를 분석하는 것을 목표로 합니다. 다음은 STREETS 데이터셋의 주요 구성 요소와 특징을 소제목별로 더 자세히 설명한 내용입니다.

---

### 1. **데이터셋의 목표**

- **STREETS 데이터셋**은 주로 교외 지역의 교통 흐름을 분석하고자 개발되었습니다. 기존의 교통 데이터셋들은 대부분 도심 지역이나 고속도로 교통 흐름에 초점을 맞추고 있어, **교외 지역의 교통 패턴을 잘 반영하지 못하는 한계**가 있었습니다.
- 이 데이터셋은 **저비용의 비침해적**인 웹 카메라를 사용해, **실시간 교통 흐름을 모니터링**하면서 교외 지역 교통 데이터를 효율적으로 수집하고자 했습니다】.
- 주요 목표는 **지능형 교통 시스템(Intelligent Transportation Systems)** 및 **스마트 시티** 구축에 필요한 교통 데이터를 제공하고, 연구자들에게 벤치마크 데이터셋으로 활용될 수 있도록 하는 것입니다.

---

### 2. **데이터 수집 과정**

- **Lake County**, Illinois의 교외 지역에서 **2.5개월 동안** 데이터를 수집했습니다. 카메라는 주로 교차로에 설치되었으며, **100개의 카메라**에서 총 **400만 장 이상의 이미지**가 캡처되었습니다.
- 카메라는 일정한 주기로 동기화되지 않았으며, **약 10분 간격으로** 주기적으로 이미지를 촬영했습니다. 각 카메라는 교차로의 다양한 방향을 포착할 수 있도록 **회전 가능**한 구조로 설계되어, **최소 2개에서 최대 4개 방향**을 캡처했습니다.
- 수집된 이미지는 날씨 조건, 조명 상태, 차선의 시야에 따른 **다양한 환경적 조건**을 포함하여 교통 흐름을 보다 다양하게 반영하도록 설계되었습니다.

---

### 3. **카메라 네트워크의 구조와 데이터 처리**

- 각 카메라 위치는 그래프의 정점(Vertex)으로 모델링되었고, 카메라 네트워크는 **방향 그래프**로 변환되었습니다. 이를 통해 교차로에서의 **차량 흐름을 시각적으로 분석**할 수 있습니다.
- 내부 엣지(Internal Edge)와 외부 엣지(External Edge)를 정의하여, 교차로에서의 **진입 및 진출** 흐름을 정확하게 모델링했습니다. 내부 엣지는 **동일 교차로 내**에서의 차량 흐름을, 외부 엣지는 **인접 교차로 간**의 흐름을 나타냅니다.
- 카메라 뷰의 방향에 따라 **차선 정보**와 **Google Maps**를 기반으로 **거리**를 계산하여 각 엣지에 가중치를 부여했습니다.

---

### 4. **차량 감지 및 데이터 처리 알고리즘**

- 수집된 이미지에서 **차량 감지**를 위해 **Mask R-CNN** 모델이 사용되었습니다. Mask R-CNN은 차량을 세그멘테이션(segmentation)하고 **차량 수를 계산**하는 데 사용되며, 각 프레임에서 교차로의 **진입 및 진출 차량**을 정확하게 감지했습니다.
- 이미지에 나타난 차량을 정확하게 세기 위해 **약 3,000개의 라벨링된 이미지**를 사용해 Mask R-CNN을 재훈련시켰습니다. 이 과정에서 **Amazon Mechanical Turk**를 통해 작업자들이 차량을 세그멘테이션하고 검증했습니다.
- 학습에 사용된 데이터는 출퇴근 시간대(7~9시, 4~6시)의 교통량을 강조하여, **혼잡한 교통 상황**에서의 차량 감지 성능을 향상시켰습니다.

---

### 5. **교통 사건 및 비정기적 사건 기록**

- **2,566건의 비정기적 사건**(예: 차량 사고, 도로 장애물, 공사 등)이 이미지 데이터와 함께 기록되었습니다. 이 사건들은 **현지 교통 엔지니어**들이 기록했으며, 사건 발생 시간, 위치, 원인 및 **교통 흐름에 미치는 영향**에 대한 정보가 포함되어 있습니다.
- 이 데이터는 교통 사고와 같은 비정기적 사건이 교통 흐름에 어떻게 영향을 미치는지 연구할 수 있도록 지원합니다.

---

### 6. **카메라 네트워크 그래프**

- **Gurnee**와 **Buffalo Grove**라는 두 지역의 교차로에 카메라가 설치되었으며, 이 지역에 **100대의 카메라**가 배치되었습니다. 각각의 커뮤니티는 **50대의 카메라**로 나뉘었으며, 각 카메라는 **방향 그래프**로 변환되었습니다【23†source】.
- 그래프는 교통 흐름을 시각화하기 위해 **카메라 간의 연결성**을 나타내며, 차량이 진입하고 나가는 교차로의 차선 수를 기반으로 **엣지 가중치**가 부여되었습니다.

---

### 7. **벤치마크 작업 및 모델 평가**

- STREETS 데이터셋을 기반으로 한 주요 벤치마크 작업 중 하나는 **단일 단계 교통 예측(Single-step Traffic Prediction)**입니다. 이는 **카메라 네트워크 그래프**를 사용하여 특정 지점의 교통량을 예측하는 작업입니다.
- **랜덤 포레스트 회귀(Random Forest Regressor, RFR)**, **서포트 벡터 회귀(Support Vector Regressor, SVR)**, **선형 회귀(Linear Regression)**, **인공 신경망(Artificial Neural Network, ANN)** 등의 모델로 성능을 평가했습니다. 
- 각 모델은 교차로에서의 교통량을 예측하는 데 사용되었으며, 이를 통해 **공간적 데이터**와 **시간적 데이터**를 결합하여 **정확한 예측**을 목표로 했습니다.
- 예측 성능은 MAE(Mean Absolute Error)로 평가되었으며, 실험 결과는 각기 다른 날짜에 대해 비교되었습니다.

---

### 8. **결론 및 향후 연구 방향**

- STREETS는 교외 교통 흐름 분석에서 새로운 표준을 제공하며, 연구자들이 교통 예측, 차량 감지, 비정기적 사건 분석 등 다양한 작업을 수행할 수 있는 벤치마크 데이터셋입니다.
- **미래 연구 방향**으로는 **교통 밀도 예측**, **비정기적 사건의 영향 분석**, **차량 세기** 및 **웹 카메라 기반 장면 분석** 등의 작업을 제안합니다.
- 또한, 교외 지역의 교통 흐름과 다양한 조건을 반영한 더 나은 지능형 교통 시스템 연구가 가능합니다.

---

이렇게 STREETS 데이터셋은 교외 지역의 교통 데이터를 효율적으로 수집하고 분석할 수 있도록 설계된 고유한 데이터셋입니다. 이를 통해 연구자들이 교통 흐름과 관련된 다양한 문제를 탐구할 수 있는 기반을 제공합니다.
