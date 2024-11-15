[공부자료_코랩](https://colab.research.google.com/drive/1KKp9-Fhr-PmN_Cndebb0wSy-JgcZuPST?usp=sharing#scrollTo=nx5ViAXvwcWS)
## 저번 시간 : 데이터 관련해서 선택에 대한 부분 피트백 + 추가적으로 B-box 를 적용하는 것을 추가로 진행하면 된다는 피드백 받았음

## 요약 : 
###  1.  관련 연구 조사(객체탐지 정의, 활용, 객체탐지 모델 역사,  YOLO5)  
###  2. 슈퍼브 AI를 이용해서 바운딩박스 라벨딩 데이터 뽑기 성공 
###  3. 추가적으로 데이터 모델링 진행




-------------------




## 01.

## 객체탐지 : 한 이미지에서 객체와 그 경계 상자(bounding box)를 탐지

## Applications

### 자율 주행 자동차에서 다른 자동차와 보행자를 찾을 때
### 의료 분야에서 방사선 사진을 사용해 종양이나 위험한 조직을 찾을 때



![image](https://github.com/user-attachments/assets/1a98346f-651e-4a86-840d-66193a0008a0)

--------------------

## 객체 탐지 (Object Detection)의 역사




![image](https://github.com/user-attachments/assets/8153016c-13b2-4a34-a35d-feda414a1f9f)


# RCNN (2013)
Rich feature hierarchies for accurate object detection and semantic segmentation (https://arxiv.org/abs/1311.2524)
- 물체 검출에 사용된 기존 방식인 sliding window는 background를 검출하는 소요되는 시간이 많았는데, 이를 개선시킨 기법으로 Region Proposal 방식 제안
- 매우 높은 Detection이 가능하지만, 복잡한 아키텍처 및 학습 프로세스로 인해 Detection 시간이 매우 오래 걸림

# SPP Net (2014)
Spatial Pyramid Pooling in Deep Convolutional Networks for Visual Recognition (https://arxiv.org/abs/1406.4729)
- RCNN의 문제를 Selective search로 해결하려 했지만, bounding box의 크기가 제각각인 문제가 있어서 FC Input에 고정된 사이즈로 제공하기 위한 방법 제안
- SPP는 RCNN에서 conv layer와 fc layer 사이에 위치하여 서로 다른 feature map에 투영된 이미지를 고정된 값으로 풀링
- SPP를 이용해 RCNN에 비해 실행시간을 매우 단축시킴

# Fast RCNN (2015)
Fast R-CNN (https://arxiv.org/abs/1504.08083)
- SPP layer를 ROI pooling으로 바꿔서 7x7 layer 1개로 해결
- SVM을 softmax로 대체하여 Classification 과 Regression Loss를 함께 반영한 Multi-task Loss 사용
- ROI Pooling을 이용해 SPP보다 간단하고, RCNN에 비해 수행시간을 많이 줄임

# Faster RCNN (2015)
Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks (https://arxiv.org/abs/1506.01497)
- RPN(Region Proposal Network) + Fast RCNN 방식
- Selective Search를 대체하기 위한 Region Proposal Network 구현
- RPN도 학습시켜서 전체를 end-to-end로 학습 가능 (GPU 사용 가능)
- Region Proposal를 위해 Object가 있는지 없는지의 후보 Box인 Anchor Box 개념 사용
- Anchor Box를 도입해 Fast RCNN에 비해 정확도를 높이고 속도를 향상시킴

# SSD (2015)
SSD: Single Shot MultiBox Detector (https://arxiv.org/abs/1512.02325)
- Faster-RCNN은 region proposal과 anchor box를 이용한 검출의 2단계를 거치는 과정에서 시간이 필요해 real-time(20~30 fps)으로는 어려움
- SSD는 Feature map의 size를 조정하고, 동시에 앵커박스를 같이 적용함으로써 1 shot으로 물체 검출이 가능
- real-time으로 사용할 정도의 성능을 갖춤 (30~40 fps)
- 작은 이미지의 경우에 잘 인식하지 못하는 경우가 생겨서 data augmentation을 통해 mAP를 63에서 74로 비약적으로 높임

# RetinaNet (2017)
Focal Loss for Dense Object Detection (https://arxiv.org/abs/1708.02002)
- RetinaNet 이전에는 1-shot detection과 2-shot detection의 차이가 극명하게 나뉘어 속도를 선택하면 정확도를 trade-off할 수밖에 없는 상황
- RetinaNet은 Focal Loss 개념의 도입과 FPN 덕분에 기존 모델들보다 정확도도 높고 속도도 여타 1-shot detector와 비견되는 모델
- background object의 Loss를 줄이기 위해 (1-sig)를 제곱하여 loss를 변동시킴으로써 해결
- Focal Loss는 background object들이 학습에 영향을 주지 않게 하여 학습의 다양성을 넓힘

# Mask R-CNN (2018)
Mask R-CNN (https://arxiv.org/pdf/1703.06870.pdf)

# YOLO (2018)
YOLOv3: An Incremental Improvement (https://arxiv.org/abs/1804.02767)
- YOLO는 v1, v2, v3의 순서로 발전하였으며, v1은 정확도가 낮았고 이는 v2에서도 문제였음
- 엔지니어링적으로 보완한 v3는 v2보다 속도는 조금 떨어지지만, 정확도는 크게 향상됨
- RetinaNet과 같이 FPN 도입으로 정확도 상승
- RetinaNet 대비 4 mAP 정도 낮지만, 속도는 더 빠름

# RefineDet (2018)
Single-Shot Refinement Neural Network for Object Detection (https://arxiv.org/pdf/1711.06897.pdf)

# M2Det (2019)
M2Det: A Single-Shot Object Detector based on Multi-Level Feature Pyramid Network (https://arxiv.org/pdf/1811.04533.pdf)

# EfficientDet (2019)
EfficientDet: Scalable and Efficient Object Detection (https://arxiv.org/pdf/1911.09070v1.pdf)

# YOLOv4 (2020)
YOLOv4: Optimal Speed and Accuracy of Object Detection (https://arxiv.org/pdf/2004.10934v1.pdf)
- YOLOv3에 비해 AP, FPS가 각각 10%, 12% 증가
- 다양한 딥러닝 기법(WRC, CSP 등)을 사용해 성능 향상
- CSPNet 기반의 backbone(CSPDarkNet53)을 설계하여 사용

# YOLOv5 (2020)
- YOLOv4에 비해 낮은 용량과 빠른 속도 (성능은 비슷)
- CSPNet 기반의 backbone을 사용
- YOLOv3를 PyTorch로 구현한 Glenn Jocher가 발표

# 이후
- 다양한 YOLO 버전들이 발표됨
- Object Detection 분야에서 많은 논문이 계속 발표되고 있음

------------------------

## YOLO (You Only Look Once)

### 가장 빠른 객체 검출 알고리즘 중 하나
### 256x256 사이즈의 이미지
### 파이썬, 텐서플로 기반 프레임워크가 아닌 C++로 구현된 코드 기준 GPU 사용 시, 초당 170 프레임(170 FPS, frames per second)
###  작은 크기의 물체를 탐지하는데는 어려움

https://pjreddie.com/darknet/yolo/
https://www.youtube.com/watch?v=MPU2HistivI


앵커 박스(Anchor Box)
YOLOv2에서 도입

![image](https://github.com/user-attachments/assets/05cda267-2cbc-46fd-b734-6387a02bc18f)

![image](https://github.com/user-attachments/assets/6cecccd1-0222-4344-a512-68413ffabd25)

사전 정의된 상자(prior box)

객체에 가장 근접한 앵커 박스를 맞추고 신경망을 사용해 앵커 박스의 크기를 조정하는 과정때문에  tx,ty,tw,th 이 필요



첫 번째 값 (1): 객체의 클래스 레이블입니다. 이 값은 감지된 객체의 클래스 ID를 나타내며, YOLO 모델을 훈련할 때 설정한 클래스 레이블에 해당합니다. 예를 들어, 1이 차량을 의미하도록 설정되었다면, 해당 객체는 차량을 나타냅니다.

두 번째 값 (0.820964): 객체의 중심점의 x좌표입니다. 비율로 표현되며, 이미지의 전체 너비에 대한 상대적 위치입니다. 0은 이미지의 왼쪽 끝, 1은 오른쪽 끝을 의미합니다.

세 번째 값 (0.703546): 객체의 중심점의 y좌표입니다. 비율로 표현되며, 이미지의 전체 높이에 대한 상대적 위치입니다. 0은 이미지의 위쪽 끝, 1은 아래쪽 끝을 의미합니다.

네 번째 값 (0.141927): 객체의 너비입니다. 이미지의 전체 너비에 대한 상대적 비율로 표시됩니다.

다섯 번째 값 (0.184759): 객체의 높이입니다. 이미지의 전체 높이에 대한 상대적 비율로 표시됩니다.


-----------------

## 02. 슈퍼브 AI를 이용해서 바운딩박스 라벨딩 데이터 뽑기 성공 

![스크린샷 2024-11-15 03-04-50](https://github.com/user-attachments/assets/064972a8-1f1d-4ed4-8673-dc53feb98b92)

![스크린샷 2024-11-15 03-06-42](https://github.com/user-attachments/assets/573dfdec-882d-438e-bbd2-d06a9efeea4c)





----------------------




##0.3 추가적으로 데이터 모델링 진행


Train : 83,800장, Val : 56,300


## train

![image](https://github.com/user-attachments/assets/0a83c1fe-5e95-4345-85ec-c79d98a867fa)


![image](https://github.com/user-attachments/assets/c4197e34-4333-48e6-8432-9b10ba826b80)

바운딩 박스 손실, 객체 손실, 클래스 손실을 나타냅니다.

169: 해당 배치에서 감지된 인스턴스 수입니다.
416: 입력 이미지 크기입니다.

바운딩 박스 손실, 객체 손실, 클래스 손실

## eval

![image](https://github.com/user-attachments/assets/216dc95e-7aae-4c19-88f4-6ca93af9d1ea)


