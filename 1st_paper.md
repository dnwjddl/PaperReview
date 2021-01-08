## Base Knowledge
### NLP에서의 Transformer
```RNN 계열```(무조건 가까운 단어가 연관성 높게) **Long-Term Dependency 문제 발생**  
```LSTM``` 게이트 추가하여 멀리있는 단어에도 영향력이 가해짐 (이후 ```GRU```등장)
  - 거리에 대한 한계가 여전히 존재
  - 순차적으로 연산해야한다는 점이 병렬처리에 어려움이 있어 연산량이 너무 많아 학습속도가 느림
```Attention``` 인코더-디코더 구조로 이루어져있으며, 이 구조에서 인코더는 입력 시퀀스 하나를 벡터 표현으로 압축, 디코더는 이 벡터표현으로 출력 시퀀스 만듦
  - 인코더가 입력 시퀀스를 하나의 벡터로 압축하는 과정에서 입력 시퀀스의 정보가 일부 손실 된다는 단점


![image](https://user-images.githubusercontent.com/72767245/104017985-6dc27100-51fc-11eb-934c-2227741cede7.png)

```Transformer``` Attention으로 인코더와 디코더로 구현한 것  
인코더에서 입력 시퀀스를 입력 받고, 디코더에서 출력 시퀀스를 출력하는 인코더-디코더 구조로 되어있음
  - 이전과 다른점은 **인코더와 디코더라는 단위가 N개 존재** 할 수 있다는 것(논문에서는 6개 쌓았다고 함)
  
![image](https://user-images.githubusercontent.com/72767245/104017993-73b85200-51fc-11eb-96f8-f9e64c5898ab.png)

- ```Encoder```구조는 하나의 인코더가 Self-Attention 및 Feed Forward인 두 개의 sub-layer로 이루어져 있다.(가중치 공유하지 않음)
- ```self-attention layer```: 하나의 특정한 단어를 인코딩 하기 위해 입력 내의 모든 다른 단어들과의 관계를 살펴보게 된다.
- ```feed-forward layer```: 똑같은 feed-forward 신경망이 각 위치의 단어마다 독립적으로 적용하여 출력을 만듦
- ```Decoder```: 두 층 사이에 ```Encoder-Decoder Attention```이 포함되어 있는데 이는 Decoder가 입력 문장 중에서 각 time step에서 가장 관련 있는 부분에 집중 할 수 있도록 해줌

![image](https://user-images.githubusercontent.com/72767245/104018398-0bb63b80-51fd-11eb-9766-5d0bee99bc0d.png)

# An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale
## Abstract
-```Transformer```
  - standard architecture for NLP
- Convoluional Networks
  - attention is applied keeping their overall structure
  - 컴퓨터 비전에서는 attention 개념은 CNN 구조에 주로 적용되어 전체 구조를 유지하되 CNN 특성 요소를 대체하는데 사용
-  **Transformer in Computer Vision**
  - a pure transformer can perform very well on ```image classification tasks when applied directly to sequences of image patches
  - achieved SoTA with small computational costs when pre-trained on large dataset
 
## Introduction
 
### NLP
Large Text Corpus에서 pre-train 후 task specific dataset에 대해 fine-tuning을 수행하는 것(BERT)
- Transformer의 계산 효율성 및 확장성으로 100B이상의 파라미터를 사용하여 큰 모델을 학습

### Computer Vision
여전히 CNN 많이 사용
  - self-attention과 결합하려고 시도(https://arxiv.org/abs/1906.01787, https://arxiv.org/abs/2005.12872)
  - CNN을 아예 대체(https://arxiv.org/abs/1906.05909, https://arxiv.org/abs/2003.07853)
이론적으로는 효율적이지만 specialized attention pattern을 사용하기 때문에 최신 하드웨어 가속기에서는 아직 효과적으로 사용하기 어려움  
large-scale image recognition task에서 ResNet-like architecture는 여전히 SoTA

### IN THIS PAPER
NLP의 Transformer 모델 수정을 최소화, 표준 Transformer를 이미지에 직접 적용해보는 실험을 시도
 - image를 patch로 분할 (image patch는 NLP에서 token(word)와 동일한 방식)
 - patch의 linear embedding sequence를 Transformer에 대한 입력으로 feed
 - supervised learning 이미지 분류에 대한 모델을 학습
 
#### mid sized Dataset
mid sized Dataset(ImageNet)에서 학습할때 비슷한 크기의 ResNet보다 몇퍼센트 낮은 정확도를 달성  
Transformer는 translation equivariance 및 locality와 같은 CNN 고유의 inductive bias를 고려할 수 없기 때문에 불충분한 양의 data에 대해 학습할 때 일반화가 잘 되지 않는 문제점

#### **large-scale Dataset**(14M-300M Images)
대규모의 Dataset으로 학습을 하면 ```inductive bias```능가 가능  
Transformer는 충분한 규모로 사전 학습되고 더 적은 데이터로 fine tuning 할 때 좋은 결과를 얻을 수 있음
- 각 유명한 benchmark에서 ImageNet에서 88.3%, CIFAR-100에서 94.55% 등의 성능으로 SoTA에 접근하거나 이를 능가하는 결과 

## Method
### ViT(Vision Transformer)

![image](https://user-images.githubusercontent.com/72767245/104024839-14ac0a80-5207-11eb-8de4-126939970c79.png)

#### Input Image
![image](https://user-images.githubusercontent.com/72767245/104028021-8b4b0700-520b-11eb-9e27-bcc5db5596e8.png)

#### Architecture
Transformer의 Encoder부분과 동일(즉, BERT)  

![image](https://user-images.githubusercontent.com/72767245/104028678-5b503380-520c-11eb-852d-84e6f2e89439.png)

기존의 Encoder과 다른점 두가지

- ```Pre-Norm```: Norm이 Multi-Head Attention/MLP 전에 위치(* Norm은 Layer Normalization(=LM) 의미)
- ```GELU```: MLP는 2단으로 활성화 함수로 GELU를 채용(Original은 ReLU를 사용)
<br><br>


![image](https://user-images.githubusercontent.com/72767245/104044958-374b1d00-5221-11eb-9dd4-3729f843308a.png)
![image](https://user-images.githubusercontent.com/72767245/104044968-3a460d80-5221-11eb-98f8-a8d703d720ce.png)

- 

#### Pre-trained & fine-tuning
