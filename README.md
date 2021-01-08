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

## Object Detection

## Image Segmentation
