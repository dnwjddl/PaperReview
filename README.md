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

* paper : https://openaccess.thecvf.com/content_CVPR_2020/papers/Collins_Editing_in_Style_Uncovering_the_Local_Semantics_of_GANs_CVPR_2020_paper.pdf
* video : https://www.youtube.com/watch?v=l2RATZjpzwI


## Object Detection

## Image Segmentation
