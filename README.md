# PaperReview_v1 
computer vision paper review

## Image Classification
### An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale (ICLR 2021 : Open review)
- NLP분야에서 핫한 모델인 Transformer를 vision task에 적용한 논문
- Transformer을 거의 그대로 image classification task에 이용한 것으로, ImangeNet/ImageNet-ReaL/CIFAR-100/VTAB SoTA모델과 거의 비슷한 정도 혹은 그 이상을 성능을 달성

https://arxiv.org/pdf/2010.11929.pdf

### Spatially Attentive Output Layer for Image Classification(Accepted at CVPR 2020, Kakao Brain)
- 일반적인 CNN(Convolutional Neural Network)는 GAP(Gloval Average Pooling)에 이어 출력 로짓에 Fully Connected layer 사용한다.
- 이 논문에서 새롭게 제시되는 spatial aggregation procedure 는 출력 계층에서 위치별 정보의 활용을 제한한다.
- 이 논문은 위치별 출력 정보를 명시적으로 활용하기 위해 기존 컨볼루션 피쳐맵 위에 새로운 spatial output layer 를 제안한다.

https://arxiv.org/pdf/2004.07570.pdf

## GAN(Generative Adversarial Network)
### U-GAT-IT: Unsupervised Generative Attentional Networks with Adaptive Layer-Instance Normalization for Image-to-Image Translation(ICLR 2020)
- Unsupervised Image-to-Image Translation
- 두 도메인간의 변환을 할때, 가장 차이가 나는 영역에 집중해서 변환을 하도록 Attention module 결합
- 변환을 할때, 데이터셋에 따라서 얼만큼 변환할지 네트워크가 스스로 학습하는 AdaLIN(Adaptive Layer-Instance Normalization)이라는 normalization 기법 제안

https://arxiv.org/pdf/1907.10830.pdf

### StarGAN v2: Diverse Image Synthesis for Multiple Domains (CVPR 2020)
- 기존 StarGAN 모델은 하나의 모델로 다양의 도메인의 이미지를 생성할 수 있는 모델
- 어떤 도메인의 하나의 이미지를 타겟 도메인의 여러 다양한 이미지들로 변경했다는 점과 동시에 여러 타겟 도메인을 목표로 할 수 있게 되었다는 점이 v2.에서 업데이트 됨


https://arxiv.org/abs/1912.01865


### Editing in Style: Uncovering the Local Semantics of GANs (CVPR 2020)
이미지를 생성 할 때 객체의 특정 부분(Localizaed smentic part)을 수정할 수 있도록 함.

* paper : https://arxiv.org/abs/2004.14367  
https://openaccess.thecvf.com/content_CVPR_2020/papers/Collins_Editing_in_Style_Uncovering_the_Local_Semantics_of_GANs_CVPR_2020_paper.pdf
* video : https://www.youtube.com/watch?v=l2RATZjpzwI


## Object Detection
### DE:TR: End-to-End Object Detection with Transformers[Facebook AI][ECCV 2020]
https://arxiv.org/abs/2005.12872   
- Object Detection을 direct set prediction의 문제로 바라보는 새로운 방법을 제시
- NMS나 앵커 생성하는 과정을 효과적으로 제거하여 End-to-end 기반의 Object Detection 방법 제시(Transformer 사용)

### EfficientDet: Scalable and Efficient Object Detection [Google Brain][CVPR 2020]
https://arxiv.org/abs/1911.09070v4   
- 기존 EfficientNet의 저자들이 속한 Google Brain팀에서 쓴 논문으로 EfficientNet은 Image Classification문제를 타겟으로 논문을 작성하였다면, Efficient Det은 - - Object Detection 문제를 타겟으로 논문을 작성하였습니다.
- BiFPN과 Model Scaling을 적용하여 COCO dataset에서 가장 높은 정확도를 달성하였고, 기존 연구들 대비 매우 적은 연산량(FLOPS)으로 비슷한 정확도를 달성하였다.

### SNIPER: Efficient Multi-scale Training
[paper](https://arxiv.org/pdf/1805.09300v3.pdf)


# PaperReview_v2
### Generative Pretraining from Pixels
[paper](https://cdn.openai.com/papers/Generative_Pretraining_from_Pixels_V2.pdf)
- 기존 NLP에서 성능이 좋았던 GPT를 pixel prediction에 도입
- 자연어처리에서 문장을 하나의 sequenxe로 input을 주듯 본 논문에서는 이미지를 픽셀을 flatten하여 하나의 sequence로 만든 후 transformer에 input으로 넣는 구조를 사용
- SoTA까진 아님

### NMT by Jointly Learning To Align And Translate
[paper](https://arxiv.org/abs/1409.0473)
- Attention을 처음으로 제안한 논문
- 어떤 word에 집중할지 알려주는 것이 alignment(=attention) 임

### Simple Copy-Paste is a Strong Data Augmentation Method for Instance Segmentation
[paper](https://arxiv.org/pdf/2012.07177v1.pdf)
- 두 의 이미지에서 한 장을 source, 나머지 한 장을 target으로 하여 source 이미지 내 객체들의 부분집합을 선택해 target 이미지에 붙여 넣음으로써 어렵고, 새롭고 이미지 데이터셋을 만들 수 있음
- 코드 이식성이 좋아서 쉽게 다른 모델을 사용할 때 data augmentation 적용할 수 있으며 여러 실험을 진행해 본 결과 object detection, instance segmentation, semantic segmentation, self-supervised learning 성능에 우수

# Human Mesh
## 3D human mesh recovery
- SMPL: A Skinned Multi-Person Linear Model, ACM Trans. Graphics (Proc. SIGGRAPH Asia), 2015
- Keep it {SMPL}: Automatic Estimation of {3D} Human Pose and Shape from a Single Image, ECCV 2016
- End-to-end Recovery of Human Shape and Pose, CVPR 2018
- VIBE: Video Inference for Human Body Pose and Shape Estimation, CVPR 2020
- End-to-End Human Pose and Mesh Reconstruction with Transformers, CVPR 2021

## Models and Light-weight models
- Mask R-CNN, ICCV 2017
- Focal Loss for Dense Object Detection, ICCV 2017 (RetinaNet)
- YOLACT: Real-time Instance Segmentation, ICCV2019
- MobileNets: Efficient Convolutional Neural Networks for Mobile Vision Applications, arXiv 2017
- CONVOLUTIONAL NEURAL NETWORKS WITH LOWRANK REGULARIZATION, ICLR2016
