# StarGAN-v2

## 선행 공부
- StarGAN-v1 [정리](https://github.com/dnwjddl/PaperReview_v1/blob/master/4nd_paper(StarGANv1).md)

## 관련 연구
- Image-to-Image Translation Task: Pix2Pix, CycleGAN, DiscoGAN 등이 존재
### StarGANv1 정리
#### 개요
- multi-domain translation tasks의 비효율적인 문제 해결
- N(N-1)개의 Generator가 아닌 1개의 Generator 사용

#### Generator, Discriminator
- G(x,c) -> y
- D(real) -> real/fake + classification
- D(fake) -> real/fake
- G(real image, target domain label) -> fake image
- G(fake image, original domain label) -> reconstructed image
#### loss
1. GAN 에서 사용하는 adversarial loss를 적용한다. real/fake discriminator를 사용하여 G/D에 대해 : log(D(x)) + log(1-D(G(x,c))) 
2. domain을 맞추는 classification loss를 classification discriminator을 사용하여 G에 대해 : -log(D(c|G(x,c))) / D에 대해 -log(D(c`|x))
3. 기존 이미지를 얼마나 잘 복원하는지에 대한 평가를 위하여 reconstruction image loss G에 대해: ||x-G(G(x,c),c`)||_1 으로 loss를 정의한다.


## StarGAN-v2
### 개요
**좋은 Image-to-Image Translation 모델의 특성**  
- 생성하는 이미지의 다양성
- 여러 domains에 대한 scalability

![image](https://user-images.githubusercontent.com/72767245/106156876-696af180-61c5-11eb-9689-9251b221b9bd.png)

### StarGANv2
- 어떤 도메인의 하나의 이미지를 타겟 도메인의 여러 다양한 이미지로 변경
- 동시에 여러 타겟 도메인을 목표로 할 수 있게 됨
  - 기존 StarGAN v1은 데이터 분포에 대한 다양한 특성을 반영하지 못하여, Generator은 one-hot vector등의 고정된 label만을 입력으로 가질 수 있었음
  - domain에 대해 동일한 변형만 가능 (이는 각각의 domain이 미리 정해진 인수만을 받았기 때문)
    - 성별이 'domain'이라면 화장, 수염, 머리스타일등은 'style'
    - 뛰어난 Image-to-image Translation은 domain과 style을 넘나들며 이미지 생성이 가능해야 함
<br><br>

- ```a mapping network```
  - random Gaussian noise를 style code 로 변환
- ```a style encoder```
  - given reference image에서 style code를 추출
    
