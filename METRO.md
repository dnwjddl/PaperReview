# End-to-End Human Pose and Mesh Reconstruction with Transformers

## Abstract

- **```METRO(Mesh TRansfOrmer)```** 이라는 새로운 방법 제시(single image로 3D human pose&mesh vertices 재구성)
- **transformer encoder**를 이용해 vertex-vertex 와 vertex-joint **iteraction**를 jointly model함

**OUTPUT** : 3D joint coordinates와 mesh vertices 를 동시에 뽑아냄

- 차별점
  - 기존 모델: pose와 shape parameter를 regress함
  - 기존 모델(SMPL): parametric mesh models에 의존
  - ```METRO```: 파라미터에 의존하지 않음 -> 덕분에 hands와 같은 다른 object로도 확장이 용이

- 장점
  - transformer self-attention mechanism이 mesh topology 필요성을 줄이고 두 vertices 사이에서 freely attend 하게 함
    - 저렇게 함으로써, mesh vertices 와 joints 사이의 **non-local relationships**을 학습하는 것이 가능해짐
- proposed **masked vertex modeling**를 통해 **robust**하고 **partial occlusion**같은 challenging situation를 다루는데 효과적임


```parametric mesh model > masked vertex modeling```

- Human3.6M과 3DPW 데이터셋에서 human mesh reconstruction에 대한 SOTA 결과를 냄
- 3D human reconstruction에서 현재 SOTA인 FreiHAND 데이터셋을 능가하는 범용성을 보임

## Introduction

### CONTRIBUTION [4가지]
- NEW transformer-based method(METRO)
  - 3D human pose and mesh reconstruction from a single image
  - single image로부터 3D human pose and mesh를 reconstruction을 하는 새로운 transformer-based method 도입
- the Masked Vertex Modeling objective
  - better reconstruction을 위해 vertex-vertex 와 vertex-joint interaction을 모델링하기 위해 multi-layer transformer encoder을 포함한 Masked Vertex Modeling objective 디자인함 
- METRO : human mesh (Human3.6M과 challenging 3DPW 데이터셋에서 SOTA)
- METRO : hands (FreiHAND 리더보드에서 1위) - Generalization
  - 다른 타입의 3D mesh를 예측할 수 있음


- VR, 스포츠 모션 분석, 신경퇴행성 진단 분석 등에서 3D human pose/mesh reconstruction의 관심이 높아짐
- 그러나 complex articulated motion과 occlusion으로 인해 challenging 함
- 이 분야의 work는 두가지
  - SMPL과 같은 **parametric model**를 이용
    - shape와 pose coefficients를 예측하도록 학습되는데 environment variations에 robust 함
    - But, parametric model를 construct하는 exemplars에 pose와 shape space가 제한됨
      - 이것을 극복하기 위한 두번째 방법이 고안


## Related Works
### Human Mesh Reconstruction(HMR)
- 3D human body shape를 reconstruct하는 Task

### Attentions and Transformers


## Method
### 1. Convolutional Neural Networks
- feature extraction을 위하여 사용
- ImageNet 분류 문제로 사전 학습되어 있음
- 마지막 Hidden layer에서 feature vectore를 추출(2048d)
- 추출된 feature vector X를 Transformer에 input으로 사용해 regress
- Transformer은 HRNETs와 같이 large-scale pre-trained CNN으로 이득을 얻음
- 본 실험에서 우리는 input feature를 분석해, high resolution image features가 유용하다는 것을 발견

### 2. Multi-Layer Transformer Encoder with Progressive Dimensionality Reduction
