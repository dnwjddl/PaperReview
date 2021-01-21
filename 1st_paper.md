## WHAT THIS PAPER WANTS TO SAY
- 일반적으로 컴퓨터 비전의 Image Classification에서는 CNN(Convolution Neural Network) 구조를 사용
- 이 논문에서는 자연어처리(NLP) 분야에서 쓰이는 모델인 ```Transformer```를 Image Classification에 적용
- CNN 구조를 사용하던 기존 Image Classification 중 SoTA인 ResNet, Noisy Student 보다 훨씬 적은 계산 비용으로 더 나은 성능을 보임

✔ **SoTA (State-of-the-art)**  
현재 최고 수준의 결과를 의미  
SoTA는 사전 학습된 신경망들 중 현재 최고 수준의 신경망

## Base Knowledge
- Seq2seq
- Attention Mechanism
- Transformer

<개념>
- ```RNN 계열```(무조건 가까운 단어가 연관성 높게) **Long-Term Dependency 문제 발생**  
- ```LSTM``` 게이트 추가하여 멀리있는 단어에도 영향력이 가해짐 (이후 ```GRU```등장)
  - 거리에 대한 한계가 여전히 존재
  - 순차적으로 연산해야한다는 점이 병렬처리에 어려움이 있어 연산량이 너무 많아 학습속도가 느림
- ```Attention``` 인코더-디코더 구조로 이루어져있으며, 이 구조에서 인코더는 입력 시퀀스 하나를 벡터 표현으로 압축, 디코더는 이 벡터표현으로 출력 시퀀스 만듦
  - 인코더가 입력 시퀀스를 하나의 벡터로 압축하는 과정에서 입력 시퀀스의 정보가 일부 손실 된다는 단점
- ```Transformer``` Attention으로 인코더와 디코더로 구현한 것  
  - 인코더에서 입력 시퀀스를 입력 받고, 디코더에서 출력 시퀀스를 출력하는 인코더-디코더 구조로 되어있음
  - 이전과 다른점은 **인코더와 디코더라는 단위가 N개 존재** 할 수 있다는 것(논문에서는 6개 쌓았다고 함)
  

### Seq2Seq
![image](https://user-images.githubusercontent.com/72767245/105385040-3f11b500-5c56-11eb-8676-17cf94c6ec14.png)
Encoder와 Decoder 두개의 Architecture로 구성  
인코더와 디코더 내부는 RNN 구조로 구성(실제로는 Vanilla RNN이 아닌 LSTM이나 GRU셀로 구성)  
<sos>는 디코더의 초기입력으로 문장의 시작을 의미  
문장의 끝은 <eos>로 다음 단어로 예측할때까지 반복

**RNN기반 seq2seq의 문제점**  
- (인코더를 거친 후)하나의 고정된 크기의 벡터에 모든 정보를 압축하여 정보 손실 발생
- RNN의 기울기 소실 문제(Vanishing Gradient Problem)이 존재
- 이런 문제들 때문에 입력 문장이 길면 번역 품질이 떨어지는 현상 발생
### Attention Mechanism
디코더에서 출력 단어를 예측하는 매 시점(time step)마다 인코더에서의 전체 입력 문장을 다시 한 번 참고  
단, 전체 입력 문장을 전부 다 동일한 비율로 참고하는 것이 아닌, 해당 시점에서 예측해야할 단어와 연관이 있는 입력 단어 부분을 좀 더 집중함  

### Dot-Product Attention(어텐션의 한 종류)

**Attention Value** 구해야됨  
#### [과정]
디코더의 t시점에서의 은닉상태와 인코더의 각 은닉상태 내적 >> **Attention-score** >> softmax >> **Attention Distribution**&**Weighted Sum** >> weighted sum >> **Attention value**


![image](https://user-images.githubusercontent.com/72767245/105388457-05db4400-5c5a-11eb-987a-16a814149657.png)  

- Attention value는 ```Context vector```라고함  
- Attention 값이 구해지면 Attention 값과 디코더 현재 시점의 은닉상태와 결합하여 하나의 벡터로 만듦

![image](https://user-images.githubusercontent.com/72767245/105390402-5a7fbe80-5c5c-11eb-902c-39af310d926c.png)

![image](https://user-images.githubusercontent.com/72767245/105390356-49cf4880-5c5c-11eb-97d4-67ac50c064de.png)


### NLP에서의 Transformer

![image](https://user-images.githubusercontent.com/72767245/105394744-50ac8a00-5c61-11eb-97b2-172e906834b8.png)

<br>

**Attention을 RNN의 단점을 보완하는 정도가 아니라 인코더, 디코더를 전부 어텐션 구조로 구성**

<br><br>


**RNN 구조를 없애고 전부 Attention mechanism으로 구성했기 때문에 각 단어의 위치정보를 RNN과 다른 방식으로 알려줘야함(```positional encoding```)**

<br>

![image](https://user-images.githubusercontent.com/72767245/105395170-cc0e3b80-5c61-11eb-8df7-4f819f09fd41.png)

<br>
  

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

![image](https://user-images.githubusercontent.com/72767245/104045189-842ef380-5221-11eb-8080-0d6846bc8321.png)

- Transformer Encoder는 Multi-headed self-attention 및 MLP block으로 구성된다
- Layer Norm(LN)은 모든 block 이전에 적용되고 residual connection은 모든 block 이후에 적용됨

![image](https://user-images.githubusercontent.com/72767245/104045210-8b560180-5221-11eb-8522-2c6fa43318b8.png)

[CLS] 토큰에 위치 엔코딩을 더하기 때문에 "패치 + [CLS] = N + 1"이 된다. E를 입력한 후에 입력의 맨 앞부분에 [CLS] 토큰 연결 (BERT와 동일)  
✔ BERT 내의 [CLS]
- 모든 Sentence의 첫번째 token은 언제나 [CLS]이다.  
- [CLS] token은 transformer 전체 층을 다 거치고 나면 token sequence의 결합된 의미를 가지게 되는데, 여기에 **간단한 classifier를 붙이면 단일 문장, 또는 연속된 문장의 classification을 쉽게 할 수 있음**. (classification task가 아니면 무시 가능)


<br><br>식(2)는 Multi-head Attention을 표시하는 것이고 식(3)은 MLP를 나타내는 것. 식(4)에서 z0L는 최종 단계의 출력에 있어서 이전부터 0번째의 벡터 표현이므로 (즉, [cls] token 의 최종 출력) 이것을 LN에 넣어 y를 얻어냄. MLP 헤드 자체의 식은 논문에 나오지 않지만 후에 이 y를 MLP에 넣는 것으로 최종적인 예측까지 나오는 것 같다.

##### Hybrid Architecture
이미지를 patch로 나누는 대신 ResNet의 중간 feature map에서 input sequence를 형성할 수 있다.  
Hybrid Model에서 patch embedding projection E(식1)은 ResNet의 early stage로 대체됨  
ResNet의 중간 2D feature map 중 하나는 sequence로 flatten되고 transformer dimension에 projection된 다음 transformer의 input sequence로 feed 됨  
Classification input embedding 및 position embedding은 위에서 설명한 대로 transformer에 대한 input에 추가됨

#### Pre-trained & fine-tuning
Fine-Tuning: ViT의 MLP head를 대체한다. 이 외에 세 부분정도 아이디어를 더함
- pre-train시에 해상도(e.g 224)보다도 fine-tuning시의 해상도를 높게(e.g 384) 한다.
- patch의 크기는 pre-train 과 fine-tuning 둘 다 일정(즉, fine-tuning시에는 해상도가 높으므로 patch의 수가 증가)
- pre-train에서 학습된 position Encoding을 fine-tuning 에서 부족한 부분에 삽입하여 보완한다.  


이를 위해 pre-train 된 prediction head 를 제거하고 0으로 초기화 된 D x K feedforward layer 를 연결한다. 여기서 K 는 downstream class 의 수를 뜻한다. pre-train 보다 높은 해상도로 fine-tuning 을 하는 것이 성능에 도움이 된다.   

더 높은 해상도의 이미지가 주어질 때 패치 크기를 동일하게 유지하게 되므로 유효한 시퀀스 길이가 더 커지게 된다. Vision Transformer 는 임의의 시퀀스 길이(up to memory constraint)를 처리 할 수 있지만 pre-train 된 position embedding 은 더 이상 의미가 없기 때문에 원본 이미지에서의 position 에 따라 pre-train 된 position embedding의 2D interpolation 을 수행한다. 이러한 해상도 조정 및 패치 추출은 이미지의 2D 구조에 대한 inductive bias 가 Vision Transformer 에 수동으로 적용되는 유일한 지점이라고 할 수 있다. 

## Experiments
