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
  
  
## » CycleGAN
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

### CycleGAN의 Loss
![image](https://user-images.githubusercontent.com/72767245/106149400-8e5b6680-61bd-11eb-9eed-a474b0239417.png)

## » CycleGAN과 StarGAN 차이

![image](https://user-images.githubusercontent.com/72767245/106150084-5143a400-61be-11eb-916b-429b6f6dd68b.png)

#### ```CycleGAN``` 
- Attributes가 n개면 n(n-1)개의 모델 생성  
#### ```StarGAN```
- 하나의 큰 Generator
- 모든 데이터의 정보를 이용하여 Train 가능
- 단점: image의 사이즈가 다 같아야된다 (CycleGAN은 Generator가 다 달라서 flexibility하다)

## StarGAN 
![image](https://user-images.githubusercontent.com/72767245/106150816-0f672d80-61bf-11eb-9e9c-7a84720c0fa3.png)

- x: input image
- y: output image
- c: target label
<br><br>
- Generator: G(x,c) -> y
- Discriminator: D:x -> {D_src(x), D_cls(x)}
  - real/fake, Attributions

### StarGAN의 loss
- Adversarial Loss (이미지가 진짜인지 translate 된건지)  
  - WGAN의 손실함수를 사용
- Domain classification Loss
  - (Discriminator Train) 이미지에 대해 도메인을 잘 classification 해냈는지
  - (Generator Train) 생성된 이미지에 대해 도메인을 잘 classification 해냈는지 
- Reconstruction Loss(cycle-consistency loss)
  - 도메인을 변형한 이미지를 다시 원본 이미지의 도메인을 갖도록 생성한 이미지가 원본 이미지와 얼마나 차이가 나는지

![image](https://user-images.githubusercontent.com/72767245/106155193-bea60380-61c3-11eb-815c-4fe66108be44.png)

- x: 원본 이미지
- c: 바꾸자 하는 도메인 (목적 도메인을 one-hot vector로 사용)
- c': 변환하기 전 원래 이미지의 도메인

<br>

**Objective Function**  

<br>

![image](https://user-images.githubusercontent.com/72767245/106151439-b3e96f80-61bf-11eb-9849-19c06afedb11.png)

## 두가지 Contribution
### Multi Attribution
### Multi Dataset
- Celeb: blond 등의 사람 얼굴 내 특징
- RaFD: Feelings
**Problems: Multi datasets have different labels & Each image only has partial information of the labels**  
#### Use Mask vector(m)
![image](https://user-images.githubusercontent.com/72767245/106152316-a5e81e80-61c0-11eb-9dfc-ce3316b26b9c.png)
- m: one-hot vector with n dimensions
- Ci: one-hot vector for categorical attributes
- 이 이미지가 어떤 Attributes을 가지고 있는지 network에 전달

![image](https://user-images.githubusercontent.com/72767245/106152647-09724c00-61c1-11eb-8ab0-932a28e65525.png)

![image](https://user-images.githubusercontent.com/72767245/106153024-72f25a80-61c1-11eb-9ca5-f733d61091e8.png)

## Experiments - Baselines(Benchmark)
- DIAT
- Cycle-GAN
- IcGAN
  - G:{z,c} -> x
    - z: random vector
    - c: conditional
  - E_z:x -> c,z
    - E: Encoder
    
## Experiments - Datasets
- CelebA
  - 202,599 face images
  - 40 binary attributes
  - Among 40, select 7 domains: 
    - Hair color: black, blond, brown
    - Gender: male, female
    - Age: young, old
- RaFD
  - 4824 images
  - 8 facial expressions(Angry, Contemptuous, Disgusted, Fearful, Happy, Neutral, Sad, Surprised)
  
## Experiments - Quantitative Results(Using AMT)
![image](https://user-images.githubusercontent.com/72767245/106154022-818d4180-61c2-11eb-849a-654cfd61b0ac.png)
- 각각의 Attributes에 월등한 성능을 보임
- Attribution을 합쳤을 때도 좋은 성능을 보임 

## Experiments - Quantiative Results(Classification)
- Domain을 Translate 하고 (Discriminator나 어떤 다른 classification 모델)이 이 image가 어떤 attribution을 갖는지를 classification하고 그 에러가 어떤건지 

![image](https://user-images.githubusercontent.com/72767245/106154278-c4e7b000-61c2-11eb-8202-1ea3c0410c97.png)

## Experiments - Joint Training

![image](https://user-images.githubusercontent.com/72767245/106154511-05dfc480-61c3-11eb-8063-5e028bc087fd.png)

- SNG: Only Trained on RaFD
- JNT: Trained on both RaFD and CelebA

## Limitations
- Use the same size of the images for translation (flexibility가 떨어짐, image를 crop해서 사용해야 함)
- Claimed Multiple datasets but provide the results on two datasets (두가지 이미지만 사용)
