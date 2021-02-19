# DE:TR: End-to-End Object Detection with Transformers

## Object Detection
Direct set prediction problem (개별적인 인스턴스를 예측해야되는 문제)
- predict a set of bounding boxes
- category labels for each objects of interest

✔ **set**: 순서에 상관하지 않으며, 중복되지 않음

### 기존 Object Detection
- 1) 앵커 박스 구조를 이용한 관심 영역 추출
- 2) 예측한 bounding box에 대한 Non-Maximum Supression(NMS)

### 이 논문에서의 장점
- 1) 모델의 간소화(CNN -> Transformer)
- 2) 휴리스틱한 부분의 제거
- 3) End-to-End 방식

### 이 논문의 제안 방법
- 1) 이분 매칭 손실함수
- 2) Transformer

### 성능
- COCO Datset으로 Faster RCNN과 겨룰 수 있을 만큼의 성능이 나옴
- panoptic segmentation도 활용 가능하다. (class 별로 나누는 것이 아닌 인스턴스 별로 segmentation)

### DETR의 한계점
- 1) 학습시키는 시간이 오래 걸린다.
- 2) 작은 객체에서 낮은 성능을 가짐
