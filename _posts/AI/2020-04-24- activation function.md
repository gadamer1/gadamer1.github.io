---
layout: post

title: 2020-04-24 activation function

postImage: https://cdn.pixabay.com/photo/2017/02/26/00/05/cranium-2099128_1280.png

category: AI

tags:
  - AI
---

# activation function 정리

## activation function이란

인공 뉴런 합성망에서 activation function(활성 함수)은 input갑에 대한 output의 형태를 결정해주는 중요한 역할을 합니다.
활성 함수의 도움을 받아 뉴럴 모델은 예측치와 관련이 있도록 가깝도록 가중치를 조절하여 각 셀들의 활성화 여부를 결정합니다.
활성 함수는 연산량이 많아 효율적인 알고리즘을 요구합니다.

## 활성함수의 종류

### 1. binary step function

![binary step](https://missinglink.ai/wp-content/uploads/2018/11/binarystepfunction.png)
binary function은 threshold를 기준으로 활성화를 시킵니다.
multi-value를 출력하지 못한다는 단점이 존재합니다.(yes or no)

### 2. linear activation function

![linear](https://missinglink.ai/wp-content/uploads/2018/11/graphsright.png)
y = cx 의 형식입니다.
다양한 값을 출력한다는 점에서 binary step의 단점을 보완 합니다.
단, 단점이 존재합니다.

1. backpropagation 불가능
   미분 해봤자 상수 값 c밖에 얻을 수 없겠죠?
2. 모든 네트워크층이 단순한 linear function으로 귀결됩니다.
   선형 함수의 합성함수는 선형함수입니다. 즉, 마지막 계층의 함수또한 선형 함수입니다. 너무 단순해집니다.

# 3. non-linear function

비정형적인 함수를 사용해 복잡한 관계를 구축하여 필요한 정보를 이끌어냅니다.
장점은 다음 두가지 입니다.

1. backpropagation 가능
   미분이 가능합니다!
2. 다층망을 쌓아올려 복잡한 데이터 인풋에 대해 높은 수준의 정확도를 이루어낼 수 있습니다.

## non-linear function 종류

### 1. sigmoid / logistic 함수

![sigmoid](https://missinglink.ai/wp-content/uploads/2018/11/sigmoidlogisticgraph.png)
장점:

- 유연한 미분값
- 출력값을 (0,1)의 범위를 갖도록 normalizing합니다.
- X값이 0에서 멀어질 수록 1또는 0에 가까워집니다. 예측값을 갖도록 합니다. 예측값이 선명하다고 할 수 있습니다.

단점:

- vanishing gradient: 미분값이 (0, 1/4)범위로 한정.
- gradient의 값이 모두 양수또는 음수의 값을 가져 지그재그 꼴로 학습합니다. (not zero centered)
- 연산비용이 많이 듭니다.

### 2. tanh

![tanh](https://missinglink.ai/wp-content/uploads/2018/11/tanhhyperbolic.png)
장점:

- zero centered
- 나머지는 sigmoid와 같음

단점:

- sigmoid와 같음

### 3. ReLU ( Rectified Linear Unit)

![ReLU](https://missinglink.ai/wp-content/uploads/2018/11/relu.png)

장점:

- 연산이 효율적입니다
  비교연산 한번으로 값이 결정됩니다.
- 비 선형적입니다
  backpropagation이 가능합니다.

단점:

- 입력값이 양수가 아닐 때 gradient값은 음수가 됩니다. 이경우 학습을 못합니다. dying ReLU

### 4. Leaky ReLU

![Leaky](https://missinglink.ai/wp-content/uploads/2018/11/leakyrelu.png)
Dying ReLU 문제를 해결하기위해 고안되었습니다.
단점:

- 입력값이 음수일 때 결과가 일정하지 않습니다.
- 성능이 ReLU보다 항상 나은 것은 아닙니다.

### 5. softmax

![softmax](https://missinglink.ai/wp-content/uploads/2018/11/softmax.png)

출력값을 (0,1)로 normalizing하고, 총합은 1이되는 특징을 갖습니다.
마지막 레이어에 많이 사용됩니다.
장점:

- 다중 클래스에 사용가능합니다.
- 정규화 기능을 갖습니다.

### 6. swish

![swish](https://missinglink.ai/wp-content/uploads/2018/11/swish.png)

sigmoid 함수에 입력값을 곱한 형태입니다.
비슷한 컴퓨팅 효율로 ReLU및 다른 활성화 함수를 대체하기위해 고안되었고 더 좋은 성능을 가진다고 합니다.
