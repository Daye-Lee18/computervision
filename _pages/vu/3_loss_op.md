# Loss Functions & Optimization 

* data-driven approach: 사람은 모델의 형태만 정의하고 데이터를 통해 모델이 학습된다. 인간의 개입을 최소화. 
* Classification때는 cross entropy, Regression은 mse를 보통 사용한다. 
  
<Confidence Score & Probability >
0. Sigmoid -> softmax: 각 클래스별로 confidence score이 차이 값들을 이용해 normalization (0~1) 방법 

````{admonition} confidence score vs. probability 
:class: note 

confidence score: 확률로 바꾸기 전의 값 (logit), 해석이 어려움 
probability: 정규화된 결과, 해당 클래스일 확률 (softmax)

| 구분 | confidence score | probability |
| --- | ---| ---|
| 의미 | 모델의 raw 출력 | 해석 가능한 확률 |
| 범위 | ($-\inf ~ \inf$) | (0 ~ 1) |
| 합 | 의미 없음 | 합 = 1 |
| 사용 | 내부 계산 | Loss/예측|

````

````{admonition} confidence score 해석 
:class: dropdown 

* condidence score란, 데이터 벡터 x를 classifier가 만든 "결정 경계(평면)"에 투영해서 나온 scalar 값이다. 
  * $w^{T}x + b$ = confidence score at boundary= z
    * 평면으로부터 w 방향으로 projection한 값 + bias
* boundary위에 있으면 모델은 중립 상태
  *   $w^{T}x + b$ = confidence score at boundary= 0
````

1. Sigmoid function: linear classifier에서 inference input의 각 classifier에 대입해서 나온 각 class에 대한 값인 score은 해석이 어렵다.  
   1. 두 개의 클래스를 가정했을 때, s2-s1 의 값이 크면 f(y=c2 | x) 가 1로 증가해야하고, s1-s2 의 값이  크면 f(y=c1|x)이 1로 증가하면 된다. 
   2. 두 클래스에 대해서 두 score의 차이를 입력으로 했을 때, 0과 1사이의 값을 출력해 인간이 해석하기에 좋은 형태로 만들 수 있다. 


$$\sigma (s) = \frac{1}{1+e^{-s}}, \quad where \quad s = s2 - s1$$

$$p(y=c_{2} | x) = \frac{e^{s2}}{e^{s_{1}}+e^{s_{2}}}, \quad where \quad s1 = s_{1} - s_{2}, s2 = s_{2} - s_{1}$$

시그모이드가 확률이 아닌 이유는 1000장 중 800개가 진짜 맞았을 때, 확률이라고 확신할 수 있다. 그냥 confidence score 라고 생각하는 게 좋다. (confidence score != probability)

2. Softmax: 여러 개의 class에서는 softmax 함수를 사용한다. n>2 일때, 모든 차에대해서 일반화. 

<How to find Weights (Parameters)>

* margin based-model y = {-1, 1}
  * hinge loss : true/false를 결정하는 결정적인 지점에서 
  * log loss 
  * exponential loss: 불안정 

* loss function: 우리 모델이 잘 배우고 있는지 아닌지 수치화하는 것 
* cross entropy: $-logx$ 함수가 0부터 1범위까지 감소하는 함수 패턴을 이용한다. 실제 데이터 레이블(1)과 예측한 값(0.8)의 곱을 모든 데이터에 대해서 더한다. -> 예측을 잘하면 CE값이 1에 가까워져서 minimum (loss-weight fn)에 도달. 
* optimization: 여러 대안 (alternatives) 중에 best elements를 선택하는 수학적인 방법 
* gradient descent: 모든 데이터셋에 대하여 평균을 내어 최종 gradient 계산. 단점 3가지 정도, convex가 아니라 울퉁불퉁한 local minumum에 빠지거나 미분이 되지 않은 경우 또한 느리다. 
  * 대안 
    * batch (full) gd -> stochastic gd (1) -> mini-batch gd (보통 memory 가 허용하는 곳까지 늘림)
    * 관례상, mini-batch와 SGD는 동일하게 불리움 
* saddle point: 모든 w에 대해 미분값이 0이지만, global minimum이 아님. 예르 ㄹ들어, 2D일때, $w_{1}$에서 함수가 최댓값이고, w_{2}에서 최솟값이라면 두 변수에 대해 미분값이 0이 된다. 
* cross validation: 모델은 training dataset을 암기하는데 "실제 시험"에서 잘 보기위해서는 데이터 자체를 암기하기 보다 어느 곳에라도 적용할 수 있는 추상적인 개념 이해 (general pattern)가 필수이다. 
  * training / validation / test 로 분리. 
  * 보통 콘테스트에서는 test set이 아예 주어지지 않음.
  * test는 정말 그 어떠한 경우에도 사용되면 안됨. 
* K-fold validation: validation set은 hyperparameter나 model selection하는데 사용되는데, 이걸 나중에 트레이닝때 사용해도 되지만, 이걸로 모델을 세팅해서 이 셋에 오버피팅될 확률이 높다. 모델 학습에 사용할지는 선택이긴 하다. 