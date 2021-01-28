# StarGAN-v1: Unified Generative Adversarial Networks for Multi-Domain Image-to-Image Translation (CVPR 2018)
- Naver에서 개발
- attributes 변화 (multi-Attributes도 변화 가능)
  - age, hair, gender, 감정
- 하나의 generaters를 가지고 학습

## StarGAN-v2
[StarGAN-v2](https://github.com/dnwjddl/PaperReview_v1/blob/master/4nd_paper(StarGANv2).md) 리뷰


## Contributes
- Unsupervised(Unpaired) : Multi Dataset
  - No pair between each domain
- Multi-Domain Image-to-Image Translation (여러개의 Attribution 바꾸기 가능)
  - Translate image into multi domains simultaneously
  
  
### » CycleGAN
- ```pix2pix```는 GAN loss를 합친 목적함수를 사용하여 성능을 높였지만, Training data가 pair로 존재해야된다는 한계점 존재
- ```CycleGAN```은 사진의 스타일을 바꾸되, 다시 원본 이미지로 복구 가능한 정도로만 바꾸는 것
  - Adversarial Loss
  - Cycle-consistency Loss
  - Full Objective
- multi-domain 불가능
- 1 대 1로 하나의 모델을 만든다 (한방향 한모델)

![image](https://user-images.githubusercontent.com/72767245/106115791-7a4f3f00-6194-11eb-8a78-ee2f5f63c19b.png)

Dy는 G을 업데이트, Dx는 F를 업데이트
![image](https://user-images.githubusercontent.com/72767245/106115651-58ee5300-6194-11eb-9915-bdc20afed69b.png)

**Loss**  
![image](https://user-images.githubusercontent.com/72767245/106149400-8e5b6680-61bd-11eb-9eed-a474b0239417.png)
