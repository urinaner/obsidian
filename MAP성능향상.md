AI모델 선정과정

![[스크린샷 2023-11-08 오후 3.34.25.png]]
**Object Detection Milestones**  

여기서 1-Stage Detector 방식의 모델은 Classification(분류)와 Localization(바운딩 박스를 통해 물체의 위치정보 표시)을 동시에 수행하는 것으로 알려져 있다.

한편, 2-Stage Detector 방식의 모델은 Classification과 Localization을 순차적으로 수행한다.

즉, 다음과 같았다.

- 1-Stage Detector : 속도 빠름, 정확도 낮음
- 2-Stage Detector : 속도 느림, 정확도 높음

따라서, 실시간 CCTV 영상처리에 어떤 모델을 사용하는 것이 더 적합한지를 생각해봐야 했다.

> Q. 실시간 CCTV 영상에서는 어떤 모델을 사용하는 것이 더 적합할까??

Real Time으로 작동하는 모델이 필요했기 때문에, 정확도를 다소 희생해서라도 빠른 속도의 1-Stage 모델을 사용해야 했다.
#### [ Yolo 모델 선택]

1-Stage 방법의 대표적인 모델로는 YOLO, RetinaNet, SSD 등이 있다.

RetinaNet은 mAP 성능은 매우 좋지만, 추론시간이 매우 긴 것으로 알려져 있다. SSD와 YOLO의 mAP 값은 비슷하지만, 속도 측면에서는 YOLO가 3배 정도 더 빠른 것을 확인할 수 있었다.

따라서 One-Stage Detection 모델 중, YOLO 모델을 사용하여 객체탐지 및 카운팅 모델을 구축하기로 하였다.
YOLO v5


정확한 교통혼잡분석을 위해 각 객체의 accuracy가 0.7이상인 것만 추출

### [YOLOv5를 이용한 객체탐지 및 카운팅 구현]

#### [a. YOLOv5 모델을 사용한 차량 객체 탐지 - 라온피플 데이터 활용]

도로교차로교통 외부데이터(AI Hub 드론)를 사용하여 Yolo에 대한 Custom 학습을 진행하였다. 학습하기 이전의 모델은 여러 차량(Car)이 나열된 모습을 책상(desk)으로 인식하는 오류가 있었다. 외부데이터로 학습한 모델은 그러한 면이 제거되어 성능이 향상됨을 확인할 수 있었다.

이는 추후, COCO 데이터셋을 기반으로 재학습하여 최종적으로 Real Time Object Detection 성능향상을 이룰 수 있었다.
![[스크린샷 2023-11-08 오후 4.04.19.png]]
#### [b. COCO Dataset 활용]

COCO Dataset을 활용하여 재학습된 모델은 다음 그림과 같이 오토바이, 트럭, 버스에 대해서도 잘 인식하게 되었다. 또한 추가적인 기능으로, 화면 왼쪽 하단을 통해 현재 화면 속에 있는 차량을 Counting할 수 있도록 구현하였다.

[C. Background Subtraction Algorithm 이용]
Z.Zivkovic의 2004년 논문(Improved adaptive Gausian mixture model for background subtraction)과 2006년 논문(Efficient Adaptive Density Estimation per Image Pixel for the Task of Background Subtraction) 참고
![[스크린샷 2023-11-08 오후 3.51.28.png]]
OpenCV를 이용하여 배경을 제거한 후, 특정 accuracy값 조건을 만족하는 경우 카운팅을 실시

Tracking Detection을 사용하여 차량을 추적하고 바운딩 박스를 유지해나가는 방식으로, 차량이 정차 시 겹치게 되는 부분에 대해서도 해결


RESTAPI 시각적으로 재설계중

플로우
데이터-> Background Subtraction Algorithm -> YOLO v5 -> accuracy >=0.7 추출 -> 전처리 후 json형식 재설계 ->전송![[스크린샷 2023-11-08 오후 4.04.19.png]]
https://koreascience.kr/article/JAKO201909358629535.pdf


