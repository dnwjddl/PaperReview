# Spatially Attentive Output Layer for Image Classification [CVPR 2020, Kakao Brain] Ildoo Kim, Woonhyuk Baek et al. 
- 일반적인 CNN(Convolutional Neural Network)는 GAP(Global Average Pooling)에 이어 출력 로짓에 Fully connected Layer을 사용
- Spatial aggregation procedure은 공간정보가 분류에 유용할 수는 있지만 출력계층에서 위치별 정보의 활용은 본질적으로 제한된다
- 이 논문에서는 기존 CNN feature map 위에 새로운 공간 출력 계층을 제안하여 위치별 출력 정보를 명시적으로 활용한다

## Introduction

### 1
- CNN은 computer vision task에서 큰 진보를 이루어냄(Imge classification, Object Detection, Semantic Segmentation)
- 특히, 많은 논문과 researches들은 **convolutional block**과 **their connections**을 수정함
  - depthwise separable convolution(심층적으로 분리가능한 convolution)
  - deformable ConvNet(변형가능한 ConvNet)
  - ResNet
  - NASNet(특징 묘사를 발달시키기 위한)
- 하지만 (다중 스케일) 공간 특징 추출을 위한 well-developed convolutional architectures들에 반해, 특징맵에서 classification logits들을 생성하기 위한 output module 들은 개발이 되지않고 있다. (standard module: **GAP>>FC**) 
- CNNS with this feature aggregation은 localization ability을 어느 정도는 유지할 수 있음을 보여주었지만, 원칙적으로 이러한 CNN은 제한이 있다 이미지 분류를 위한 output logits의 명시적인 localization으로 부터 얻는 완전한 이득 착취에는 제한이 있다.

### 2
최근에 localized class-specific response는 image classification에서 높은 관심을 얻었다.
- three main advantages 
  - 시각적인 설명을 통해 CNN의 의사 결정을 해석하는 것을 도울 수 있다.
  - 공간 주의 메커니즘은 고려된 라벨과 의미론적으로 관련이 있는 영역에만 초점을 맞춤으로써 성능 개선을 위해 사용될 수 있다
  - 공간 변환을 기반으로 하는 보조적인 자체 조정 손실 또는 작업을 사용 할 수 있으며, 이는 향상된 일반화 능력으로 이어짐
    (it enables to make use of auxiliary self-supervised losses or tasks based on spatial transformations, which leaads to enhanced generalization ability)
  
### 3
그러나, 대부분의 이전 방법은 class activation mapping(CAM) 및 gradient-weighted class activation mapping 그라데이션 가중 클래스 활성화 매핑(Grad-CAM)과 같은 기존의 클래스 활성화 매핑 기법을 통해 공간 로짓 또는 attention map을 얻음
   
그들은 여전히 이미지 수준 예측을 위해 GAP을 활용했고, 따라서 대상 물체의 작은 부분만 찾거나 클래스에서 분리할 수 없는 영역에 참여함  
   
이 부정확한 attention mapping은 분류 정확도를 향상시키기 위한 사용을 방해하지만, 또한 공간 라벨링에 관한 자체 감동 적용은 회전 및 플립과 같은 단순한 공간 변환 또는 순진한 주의 자르기와 낙화와 같은 단순한 공간적 변환에서 주의 일관성을 유지하는 것으로 제한  


## Main Contributions
- The SAOL on top of existing CNNs is newly proposed to improve image classification performances through spatial attention mechanism on the explicit location-specific class response.
  - 기존 CNN 위에 있는 SAOL은 명시적인 위치별 클래스 응답에 대한 공간 주의 메커니즘을 통해 이미지 분류 성능을 개선하기 위해 새롭게 제안되었다.
  - SAOL에서 정규화된 공간주의 맵은 정교한 공간 로짓에 대해 가중 평균 집계를 수행하기 위해 별도로 획득되며 이를 통해 해석 가능한 주의 출력과 전방 전파에 의한 객체 위치 측정 결과를 생성할 수 있음
  - 이미지 분류 작업과 다양한 벤치마크 데이터 세트와 네트워크 아키텍처가 있는 Weakly Supervised Object Localization(WSOL) 과제 모두에서, 
  
