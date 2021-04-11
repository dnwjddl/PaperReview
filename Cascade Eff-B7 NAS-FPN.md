# Simple Copy-Paste is a Strong Data Augmentation Method for Instance Segmentation
(Google Research, Brain Team, UC Berkeley)  

- 두 장의 이미지에서 한장의 source, 나머지 한장을 target으로 하여 source 이미지 내 객체들의 부분 집합을 선택해 target 이미지에 붙여 넣음으로써 어렵고 새로운 이미지 데이터셋을 만들 수 있음
- **Data Augmentation** 적용할 수 있으며 Object Detection, Instance Segmentation, Semantic Segmentation, self-supervised learning 성능또한 우수

**데이터가 적은 상황에서 데이터 효율성을 끌어 올릴 수 있음**

![image](https://user-images.githubusercontent.com/72767245/114272302-9e5eb480-9a50-11eb-9985-4e66181fcb4a.png)  

## Simple Copy-Paste
- Segmentation에서는 객체의 위치를 나타내는 annotation 정보가 픽셀 단위로 저장되어 있기 때문에 object 위치가 바뀌는 변환이 적용되면 annotation도 함께 변환해주어야 함
- 이 Segmentation에서 연구되는 Augmentation 방식 중 하나가 ```Copy-Paste```
- Copy-Paste Augmentation: 특정 객체의 위치 정보를 통해 잘라내거나 복사하고, 다른 이미지 위에 붙여넣는 방법
  - 1. Instance들을 복사해올 여러 Source image들과 복사해온 instance를 붙여넣을 한 장의 target image를 선택하는 방법
  - 2. 선택한 source image들 내에서 복사할 instance들을 선택하는 방법
  - 3. 선택한 target image 안에서 instance들을 붙여 넣을 위치를 선택하는 방법



이 중 3번째 요소에 대한 선택이 조금 까다로운데, 기존의 여러 Copy-Paste 방식을 보면 Instance를 붙여넣을 이미지의 시각적 context를 고려하여 최대한 자연스러운 이미지가 완성되도록 하는 연구, 하지만 이 논문에서는 이러한 고려들을 전부 배제하고 Random으로 선택하고 붙여넣는 방식을 선택했는데, 아이러니하게도 더 좋은 성능을 보임  
하지만, 이것을 위한 조건으로 다른 여러 setting들을 고정시켜서 강력한 baseline을 만들었는데, 고정요소들로부터 backbone architecture, extent of scale jittering, training schedule, image size등이 있다. 대표적인 setting들과 추가적인 실험들을 보자  

#### Baseline across Multi Settings
- Backbone Architeture

EfficientNet-B7 Backbone과 NAS-FPN architeture를 사용해서 COCO test-dev 데이터셋에 대해서 57.3 Box AP, 49.1 MAsk AP의 성능을 달성

- Large Scale Jittering


- Object Detection

기본 연구는 instance segmentation을 위해 진행 -> Instance를 복사하면서 해당 객체의 bounding box 정보고 함께 복사하면서 Object Deteciton에도 큰 성능향상
