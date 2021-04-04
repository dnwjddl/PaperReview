# Grasp Type Revisited: A Modern Perspective on A Classical Feature for Vision (CVPR 2015)

unconstrained scenesd에서 grasp type를 인식하는 것은 large variation in appearance, occulsions, geometric disortions 때문에 Challenging

- Classify functional Hand Grasp types
  - 이를 활용한 Two Application
    - inference of human action intention
    - fine level manipulation action segmentation

grasp type은 Human action에 대한 세밀한 정보를 포함  
인간의 행동을 보다 상세하게 이해하기 위해서는 recognition of grasp type이 essential함  
grasp type은 인간의 행동의 의도를 추론하는 강력한 신호(ex. 칼을 쥐는 모양)  
Humanoid robot과 같이 intelligent agent로 작업을 수행하려면 물체를 잡는 방법에 대한 지식이 필요  


**The Goal: To provide intelligent systems with the capability to recognize the human grasp type from unconstrained static of dynamic scenes.**

### Our System
- 사람의 손 주위에 제약 없는 image patch를 적용
- 어떤 범주의 grasp type을 사용하는지 출력

### Rest of the paper
- capability: very useful for predicting ```human action intention```
- helps to further understand human action by introducing ```a finer layer``` of granularity(세밀함)

### Classification(7가지)
![image](https://user-images.githubusercontent.com/72767245/113512305-ff910e80-959e-11eb-93c8-d849a446fba8.png)

- ```PoC```: Power Cylindrical (원통형)
- ```PoS```: Power Spherical (구형)
- ```PoH```: Power Hook (손잡위 잡기)
- ```PrP```: Precision Pinch (정밀한 꼬집음)
- ```PrT```: Precision Tripod (삼각대: 와인잔)
- ```PrL```: Precision Lumbrical (전화기)
- ```RoE```: Rest or Extension (손바닥 펴있음)


## CNN for Grasp Type Recognition
- 각 계층의 ```Response maps```은 여러 filters와 융합되고 Pooling 작업에 의해 추가로 downsampling
- Pooling Operation은 최대, 최소 및 평균 샘플링과 같은 downsampling를 통해 더 작은 영역의 값을 aggregate함
- Loss Function: ```Softmax loss function```을 채택

![image](https://user-images.githubusercontent.com/72767245/113512592-5814db80-95a0-11eb-86e0-c742a9b97ba6.png)
(n번째 Training example의 k번째 ground truth output -> tnk, k번째 output layer unit in response to the n번째 input training sample -> ynk)  
N은 Training sample들의 갯수, C = 7 (Class가 7개)

- CNN은 SGD based, Two main operation: Forward and Back Propagation  
- learning rate는 dynamically lowered as training progresses.

### Model of CNN
- five layer [input layer + regression output을 위한 one-fully connected perception layer 포함)
- **First convolutional layer** : 32 filter, 5x5 with max pooling
- **Second Convolutional layer** : 32 filter, 5x5 with average pooling
- **Third Convolutional layer** : 64 filter, 5x5 with average pooling
  - convolutional layer convolves its input with a bank of filters, then applies point-wise non linearity and max or average pooling operation
- **Final Fully-connected perception layer**: 7regression outputs(linear filters to its input, then applies point-wise noe linearity.) : Fully-connected perception layer은 입력에 linearfilter을 적용한 다음 point-wise non-linearity을 적용한다.


### Test
- 훈련된 CNN 모델에 각 target hand patch를 전달하고 7x1 크기의 출력을 얻음
- action intention and segmentation experiments에서 우리는 both hands 에 대한 classification을 왼손과 오른손의 Classification으로 얻는다.
- Fully automatic fine level manipulation segmentation approach을 사용하려면 video의 input hand patches를 localize한 다음 CNN을 사용하여 grasp type을 인식해야됨
- Hand detection method을 사용해서 First frame에서 손을 감지한 다음, 평균 이동 알고리즘 기반 추적 방법을 양손에 적용하여 각 손 주변의 이미지 패치를 지속적으로 추출


- Grasp type을 훈련시키기 위해 이미지 patch의 크기는 64x64 pixel로 조정
- 
