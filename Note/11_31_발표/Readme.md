## incidence.csv 파일 분석

-----------------

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


### -----------------------------------------------------------------------------

