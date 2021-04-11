# SNIPER: Efficient Multi-Sclae Training
### RCNN & Fast RCNN의 소개

#### RCNN
- RCNN detector에서 진화된 Object Detection 알고리즘들은 비지도 알고리즘으로 Region Proposal을 생성 (주어진 이미지에서 물체가 있을법한 위치 찾기)
- 이렇게 생성된 proposal들을 224x224사이즈로 resize한 다음 CNN으로 classify함 
  - RCNN 저자들은 이미지넷 데이터(ILSVRC2012 classification)로 미리 학습된 CNN 모델을 가져온 다음, fine tune하는 방식
- scale invarient하지만 proposal이 많아질수록 연산량이 많아짐
- 보완 -> ```Fast R-CNN```

#### Fast RCNN
- 모든 propossal이 up&dwom sampling의 대상
- RCNN에서는 모든 proposal들이 224x224로 resize
- 즉 large object는 not upsampled, small object들은 not downsampled 되었다면 Fast RCNN은 모든 proposal에 대해서 up&down sampling을 모두 진행
- 따라서 RCNN이 더 효율적으로 up&down sampling을 함


#### SNIPER
- RCNN은 Fast RCNN과 다르게 연산을 공유하지않기 때문에 훨씬 느린 단점이 있고 저자는 이에 따라 둘의 장점을 서로 합친 ```SNIPER```을 제안

---

- Scale specific context-regions(A.K.A chips)을 생성
- Fast RCNN처럼 칩 안의 모든 proposal을 분류
- 다수의 proposal에 대한 효율적인 분류를 가능하게 함
- RCNN처럼 large object가 있는 이미지는 upsampling하지않고, 쉬운 Background region도 processing을 따로 하지않기 때문에 Fast RCNN detector보다 빠름
- SNIPER은 Chips를 생성하기 때문에 효율적으로 multi scale training을 가능하게 함

### multi-scale Strategies : Detector들이 Multi-scale 문제를 푸는 방법


## Chip Generation
- 이미지 안의 multi-scale에 대해 칩들을 생성
- 즉 하나의 image로 다양한 scale의 image를 먼저 만들고 그 image들 안에서 stride를 돌면서 칩을 생성하는데 
- Chip size는 512x512로 고정
  - 작게 scale된 image에서의 칩은 보다 큰 object Detection을 할때 쓰임, 크게 scale이 된 image에서는 칩은 보다 작은 object를 detection할 때 쓰임
- 각 Chip은 equal interval을 두고 생성되는데 paper에서는 interval d = 32로 설정

## Positive Chip Selection
- 각 scale마다 desired area range R(i) 존재




---
**SNIP(Scale Normalized Image Pyramid)[CVPR 2018]**  

