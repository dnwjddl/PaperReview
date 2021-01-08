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

- ```Encoder```구조는 하나의 인코더가 Self-Attention 및 Feed Forward인 두 개의 sub-layer로 이루어져 있으며, 그들 간의 같은 가중치를 공유하진 않는다.
- ```Encoder```에 들어온 입력은 일단 self-attention layer를 지나게 되는데 이 인코더는 하나의 특정한 단어를 인코딩 하기 위해 입력 내의 모든 다른 단어들과의 관계를 살펴보게 된다.
- 이를 통과한 출력은 다시 feed-forward 신경망으로 들어가게 되고 똑같은 feed-forward 신경망이 각 위치의 단어마다 독립적으로 적용하여 출력을 만듦
- ```Decoder``` 구조 또한 두 층 사이에 Encoder-Decoder Attention이 포함되어 있는데 이는 Decoder가 입력 문장 중에서 각 time step에서 가장 관련 있는 부분에 집중 할 수 있도록 해줌
