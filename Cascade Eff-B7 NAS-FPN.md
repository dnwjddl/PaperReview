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
