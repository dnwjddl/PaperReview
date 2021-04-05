# MobileNets: Efficient Convolutional Neural Networks for Mobile Vision Applications, Andrew G. Howard et al

[paper](https://arxiv.org/abs/1704.04861)

## Summary
- MobileNet은 depthwise separable convolution을 사용하여 모바일 환경에서도 사용할 수 있는 가벼운 deep neural network
- 연산이 효율적으로 설계된 MobileNet을 더 효율적으로 사용할 수 있도록 width multiplier 와 resolution multiplier 두가지 파라미터를 도입

## Depthwise separable Convolution

### Depthwise Convolution : 레이어에서 filtering 하는 부분
- H*W*C의 conv output을 C단위로 분리하여 각각 conv filter를 적용하여 output을 만들고 그 결과를 다시 합치면 conv filter가 훨씬 더 적은 파라미터를 가지고 동일한 크기의 output을 낼 수 있음
- 각 필터에 대한 연산 결과가 다른 필터로부터 독립적일 필요가 있을 경우에 장점

```python
class depthwise_conv(nn.Module):
  def __init__(self, nin, kernels_per_layer):
    super(depthwise_separable_conv, self).__init__()
    # groups = nin, 입력 레이어를 nin 개의 서로 다른 group으로 만들어서 해당 연산을 수행하겠다. (group의 default = 1)
    self.depthwise = nn.Conv2d(nin, nin*kernels_per_layer, kernel_size=3, padding= 1, groups = nin)
    
  def forward(self, x):
    out = self.depthwise(x)
    return out
```

### Pointwise convolution: filter된 부분을 comvining 하는 부분
- 1x1 Conv라고 불리는 filter, 주로 기존의 matrix의 결과를 논리적으로 다시 shuffle해서 봅아내는 것을 목적
- Channel수를 줄이거나 늘리는 목적으로도 많이 쓰임

```python
class pointwise_conv(nn.Module):
  def __init__(self, nin, nout):
        super(depthwise_separable_conv, self).__init__()
        self.pointwise = nn.Conv2d(nin, nout, kernel_size=1)

    def forward(self, x):
        out = self.pointwise(x)
        return out
```

## Depthwise Separable Convolution
- Depthwise convolution 후 Pointwise convolution
  - 3x3 filter를 통해 conv 연산 진행, 서로 다른 channel들의 정보도 공유하면서 동시에 파라미터 수도 줄이기 가능

```python
class depthwise_separable_conv(nn.Module):
    def __init__(self, nin, kernels_per_layer, nout):
        super(depthwise_separable_conv, self).__init__()
        self.depthwise = nn.Conv2d(nin, nin * kernels_per_layer, kernel_size=3, padding=1, groups=nin)
        self.pointwise = nn.Conv2d(nin * kernels_per_layer, nout, kernel_size=1)

    def forward(self, x):
        out = self.depthwise(x)
        out = self.pointwise(out)
        return out
```


