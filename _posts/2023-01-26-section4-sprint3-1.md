---
title: 합성곱 신경망(Convolutional Neural Network)과 전이 학습(Transfer Learning)
author: yun
date: 2023-01-26
categories: [Blogging, Study, Ai, Summary]
tags: [study, python, deep learning, convolutional neural network, transfer learning]
---



# 개념
## CNN(합성곱 신경망) 의 장점
* 입력된 데이터의 공간적인 특성을 보존하며 학습할 수 있다.


## 합성곱
* 컨볼루션에서의 가중치 수는 **커널크기의 제곱 × 커널의 개수 × 채널 수**에 비례하게 된다.

```
model = Sequential()
model.add(Conv2D(3, (5, 5), activation='relu', input_shape=(100, 100, 3))) # ---- (A)
model.add(MaxPooling2D((2, 2)))
model.add(Flatten())
model.add(Dense(5, activation='softmax'))
```

따라서 (A)에서 학습될 가중치의 개수는 225개 이다. ($5^2$ * 3 * 3)


## 풀링(Pooling)
* feature map의 가로, 세로 방향의 공간을 줄일 수 있다.
* 풀링의 방법에는 최대 풀링(Max Pooling), 평균 풀링(Average Pooling)이 있다.
* 풀링에는 학습해야 할 가중치가 **없다**.


## 전이학습
* 사전학습된 모델을 가져와서 우리가 풀고자 하는 문제에 적용시키는 것.
* 대량의 데이터로 사전 학습한 모델의 가중치를 가져와서 사용한다.
* 사전 학습에서 학습된 가중치는 보통 학습되지 않도록 고정한다.
* 사전 학습에서 학습된 가중치를 가져오고 고정할 경우, 모델의 학습 속도가 빠르다.


## ResNet
* 구조적 특징 `Residual Connection(=Skipped Connection)`을 적용했다.
  * Residual Connection(=Skipped Connection)
    * 층을 거친 데이터의 출력(F(x))에 거치지 않은 출력(x)을 더해 줍니다.
    * 층을 깊게 쌓아 발생하는 기울기 소실 문제를 어느정도 해결할 수 있습니다.
    * (A)를 적용하기 위해서는 층을 거치지 않은 출력(x)과 층을 거친 데이터의 출력(F(x))의 차원이 같아야 합니다.


## 이미지 증강(Image Augmentation)
* 자르기
* 채도 변경
* 회전
* 좌우 





# Q&A

1. 풀링은 꼭 진행해야하는 과정인가요? : 아닙니다.

2. 필터는 가중치 이다.

3. 지막에 softmax 10 값은 데이터셋의 특성들이 10개로 정리될 수 있는 `cifar10`이라서 10으로 설정된 건가요? : 네 맞습니다.

4. 필터를 여러개 사용하는 이유? : 각각의 필터가 서로 다른 특징을 잡아내기 때문이다.

5. GlobalAveragePooling2D을 써야하는 경우와 flattne을 써야하는 경우가 다른가요? : 비슷합니다. case by case 입니다.

6. 입력값 (28,28,3)중에 입력 채널 3개마다 커널이 존재하는거죠? : 네 맞습니다.

7. 필터가 랜덤한 초기 가중치를 가지고 있기에 시작점이 달라서 다른 특징을 뽑아내는거죠? : 맞습니다. 정확한 설명입니다.



1x1 convolutional layers 를 사용하면 비선형성의 장점이 있다고 하는데, 파라미터가 줄어드는데 어떻게 비선형성이 더 향상되나요? : Layer도 결국에는...
비선형성이 추가되면 추가될 수록 과적합이 될 우려가 있습니다.




** 전이학습



** vgg

1. 3x3 필터 사용. 계산하는 양이 적다는 이점이 있다.
2. 채널이란? RGB: 3, 흑백: 1
3. 왜 224x224x3 에서  224x224x64가 될까요? 필터링을 거쳐서.
4. 풀링 레이어는 채널이 변하지 않는다.
5. 필터는 채널 수가 됩니다. (디스커션 참조)
 



**