# U-GAT-IT: Unsupervised generative attentional networks with Adaptive layer-instance normalization for Image-to-Image Translation
## Abstract
비지도 Image-to-Image Translation
- new attention module
  - 보조 classifier에 의해 얻은 ```Attention Map```기반으로 source domain과 target domain를 구별하는데 중요한 영역에 focus 하도록 함
  - 이전 Attention-based method은 도메인 간의 기하학적인 변화를 처리 못함
    - 우리 method는 전체적인 변화가 필요한 이미지와 큰 모양 변화에 모두 변환 가능
- new learnable normalization function in an end-to-end manner
  - AdaLIN(Adaptive Layer-Instance Normalization) 기능
    - Attention-guided model이 데이터 세트에 따라 학습된 매개변수에 의해 모양과 질감의 변화량을 유연하게 제어하도록 해줌
결과 : 고정된 네트워크 아키텍처롸 하이퍼 파라미터를 기존 최첨단 모델과 비교하여 제안된 방법의 우수성 


## Intro
### 추세
- GAN 추세 (발전)
### 한계
- 이전 방법은 domain간의 모양과 질감의 변화양에 따라 성능차이 
   - ex. Local Texture를 매핑하는 Style Transfer 작업
### 우리의 방법

### 결과
