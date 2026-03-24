# 3. Loss Functions & Optimization 

<Confidence Score & Probability >
1. Sigmoid function: linear classifier에서 inference input의 각 classifier에 대입해서 나온 각 class에 대한 값인 score은 해석이 어렵다.  
   1. 두 개의 클래스를 가정했을 때, s2-s1 의 값이 크면 f(y=c2 | x) 가 1로 증가해야하고, s1-s2 의 값이  크면 f(y=c1|x)이 1로 증가하면 된다. 
   2. 두 클래스에 대해서 두 score의 차이를 입력으로 했을 때, 0과 1사이의 값을 출력해 인간이 해석하기에 좋은 형태로 만들 수 있다. 


$$\sigma (s) = \frac{1}{1+e^{-s}}, \quad where \quad s = s2 - s1$$

$$p(y=c_{2} | x) = \frac{e^{s2}}{e^{s_{1}}+e^{s_{2}}}, \quad where \quad s1 = s_{1} - s_{2}, s2 = s_{2} - s_{1}$$

시그모이드가 확률이 아닌 이유는 1000장 중 800개가 진짜 맞았을 때, 확률이라고 확신할 수 있다. 그냥 confidence score 라고 생각하는 게 좋다. (confidence score != probability)

1. 여러 개의 class에서는 softmax 함수를 사용한다. n>2 일때, 모든 차에대해서 

<How to find Weights (Parameters)>

* margin based-model y = {-1, 1}
  * hinge loss : true/false를 결정하는 결정적인 지점에서 
  * log loss 
  * exponential loss: 불안정 

* loss function: 우리 모델이 잘 배우고 있는지 아닌지 수치화하는 것 