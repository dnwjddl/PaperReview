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
