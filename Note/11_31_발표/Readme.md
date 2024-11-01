## incidence.csv 파일 분석

-----------------

# 요약

## 중간고사 피드백 -> 수정 
## 앞으로 프로젝트에 대한 고찰 -> 앞으로의 데이터 조사 준비
----------



### 1. reponsestart 가 무슨 열인지 문서 보고 이해하기 --> 헤딩 정보는 없음 PAPER 
### 2. 이벤트 타입의 정의를 찾아두자 ex) accident stall ->> 정보 없음

                 기존의 EDA는 모든 이벤트를 COUNT 하고, 박스플롯으로 시각화 하지 않으므로써 
![image](https://github.com/user-attachments/assets/1bb2c7bb-0aef-4e3c-bb37-e00057ab5246)
                          X축 시간 Y축 EVENT 발생 수




### 3. 1시간 단위로 박스 plot 으로 그리기 = 타입 별로 ex) accident ->> ok

![image](https://github.com/user-attachments/assets/b6905d02-7f38-44a4-8428-5adb2bb8ebb4)

### 요약
- **사고 발생이 가장 많고 변동이 큰 시간대**: 오전 7시, 오후 3시, 오후 5시, 오후 6시.
- **사고 발생이 적은 시간대**: 새벽(0시~5시) 및 늦은 저녁(21시 이후).
- **출퇴근 시간대**에 사고 발생 건수가 많아지고, 사고 발생의 변동성도 커지는 경향이 있습니다. 


### 4. x축 요일 y축 사고별 숫자 --> ok


![image](https://github.com/user-attachments/assets/cad674d7-3b93-4364-acd8-a5b066e67b21)

### 요약
- **사고 발생이 많응 요일은**: 화, 수, 목 금 순으로 높은 것을 확인 



### 5. 화, 수, 목 만 각각의 타입에대해서 1시간단위로 박스 plot — ok

![image](https://github.com/user-attachments/assets/d8214cd7-cdf0-4dd8-84d2-6d09346bc211)

![image](https://github.com/user-attachments/assets/2339a252-4a15-4cd7-b793-8dfb465a67e0)

![image](https://github.com/user-attachments/assets/eb63f188-9074-4d2a-8ce7-f98048a5df28)


-----------------------------------------------------------------------------------------



# 앞으로의 방향성 및 질문


### 1. STREET DATA 사고 데이터를 훈련하는 것이 의미가 더 있는지 교통 데이터에 초점을 두는 것이 맞는지??
### 2. 모델 최적화?? -> 모델의 파라미터를 줄이고 또는 작은 모델을 사용하여도 모델의 성능이 높은 것을 찾는것
### 3. 차량 수를 COUNT 한다는게 STREET DATA에서도 가능한지??(검지기 설치가 가능한지?

       사고 데이터 + 차량의 이동 + 클러스터링 후 지역간 연관성 분석을 통한 사고 발생시 교통 신호 체계 변화라는 과제
----------------------------------------------------------------------------

그렇다면 2가지로 task 나누어서 진행

### 1.task 사고인지, 예측 모델 + 경량화

### 2 - 1. task N-curve를 활용하여 구간 내 교통상태, 신호주기, 대기열 및 대기시간을 산정
### 2 - 2. 차량 객체의 궤적(Trajectory)를 생산하여 차량 간 거리, 순간 감가속 측정 → 차간거리와 감가속 상태를 이용하여 사고 위험 지표인 TTC(Time-to-collision)을 측정

### -------------------------- 사고 데이터 찾기 -------------------------------------


## [사고데이터 관련 논문, Big Data and Deep Learning in Smart Cities: A Comprehensive Dataset for AI-Driven Traffic Accident Detection and Computer Vision Systems](https://arxiv.org/html/2401.03587v1)

## [git.io, CADP: A Novel Dataset for CCTV Traffic Camera based Accident Analysis(https://ankitshah009.github.io/accident_forecasting_traffic_camera)


## [CADP: A Novel Dataset for CCTV Traffic Camera based Accident Analysis](https://arxiv.org/pdf/1809.05782)

## [dataset](https://drive.google.com/drive/u/0/folders/1Y1h7apbfYd7nNWuKZVPj7lov5YONC1aJ)

## [github](https://github.com/ankitshah009/CarCrash_forecasting_and_detection)


## -------------------------------------- 차량이동 데이터(조건 cctv, or 영상)---------------------------


## [UA-DETRAC_dataset, 고정형 CCTV 카메라로 중국 내 다양한 도심 지역에서 촬영된 차량 영상 데이터셋입니다](https://www.kaggle.com/datasets/dtrnngc/ua-detrac-dataset/data) but 현재로써는 


## -----------------------------------------------추가 질문----------------------------------------------------------------

## 1. 교통학회 학술 논문집 -> 추천하시는 논문 있으신지 여쭤보기 -> 이런 구성, 이런 흐름, 해당 분야 도메인 지식을 알고 싶고
## 2. 관련 논문 follow up 하다 보면 dataset찾기도 용이할 것으로 예상
## 3. 슈퍼브 AI 사용법 배우기(이미지 넣고 -> 해당 이미지 훈련 - > 이후 라벨링 된 데이터 DATA(IMAGE, LABEL) Loval 뽑아서 modeling 작업

