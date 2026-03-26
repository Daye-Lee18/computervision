# First Approaches for Image Classification 

1. 테스크마다 데이터셋이 있을텐데 데이터셋의 특징을 구분하는 것이 중요하다. 예를 들어, 이미지 분류에서는 같은 Label에 대해서 deformation, illumination, clutter, occlusion의 이슈로 성능이 낮아질 수 있기 때문이다. 이 한계를 극복하기 위한 방법론 연구도 연구 주제로 이어질 수 있다. 
2. Classification은 query와 training data 속 value의 ‘similarity’를 계산하여 예측하는 과정이다. 
    1. Distance/similarity 계산 방식은 다양하게 존재.
3. K-nearest neighbor classifier: training data N개와 query의 similarity 비교 (inference complexity: O(N)) 후, the first largest similarity를 가진 K중 majority vote로 최종 classification. 
   1. 장점: 구현이 간단함 
   2. 단점: inference 시간이 O(N)으로 크다. 
   3. 특징: K값을 키울수록 robust 해진다. k가 매우 작을수록 outlier 에 취약해진다. 
4. Machine learning: data-driven approach, 사람의 개입을 최소화해서 컴퓨터가 데이터를 통해 특정 테스크를 잘 수행할 수 있도록 함. 
5. Machine learning에서 training이란, “데이터를 암기”하는 과정이다. 따라서, training data를 그냥 불러오는 것 자체도 암기를 다 했다고 가정하면, 이미 training 이 끝난 상태라고 할 수 있다. (Training time complexity O(1)). Deep learning에서는 space가 작은 곳에 embedding하는 encoder를 따로 만들어 데이터를 암기한다고 생각할 수 있겠다. 
6. Curse of dimensionality: 데이터의 dimension이 커진다면, 해당 공간을 같은 일정한 간격으로 ‘채우기’ 위해 필요한 데이터의 수는 "지수적 (exponentially)"으로 증가함. 
7. Parametric approach는 학습 시 특정 parameters (=weights) 를 가진 함수를 이용해 데이터를 암기하는 방법을 뜻한다. 
    1. 장점: 학습 후에 training dataset을 몰라도, weights W matrix만 알면 된다. (Space efficient)
8. Linear Classifier: weighted sum of input pixels
    1. (CIFAR10 데이터셋 가정) Classifier 모델의 각 weights matrix row (10개)가 각 class의 classifier = 유사도 계산 기계, 
    2. 각 클래스 이미지별 특징 필터라고 할 수 있다. 내적 유사도가 높으려면 같은 위치의 값은 비슷해서 내적값이 커져야 유사도가 커짐 
9.  Weights and bias: bias is affecting the output without interacting with data x
10. Linear Classifier 모델의 해석 
    1.  F = W*x W $\in$ (10, 32*32*3 + 1), x $\in$ (32*32*3)에서, 각 weights row는 각 class의 classifier 이다.
        1.  W의 크기 (output class의 크기, input 크기): transpose해서 dimension을 맞추면 되기 때문에 순서자체는 상관없다. 
    2.  다시 한번, classfier는 similarity 계산한다.
    3.  linear classifier는 dot product로 유사도를 계산하여 클래스를 구별하는데, 
        1.  이 score (s) 값 자체는 우리가 해석하기 어렵다. 
    4.  따라서, 값이 커야 해당 클래스로 분류되기 때문에, 각 classifier를 이미지로 변환해서 보면 각 클래스의 이미지 특징을 볼 수 있다. 
    5.  즉, classifier = 유사도 계산 기반 클래스 feature filter. 
    6.  각 class마다 classifier에 대입해서 나온 score가 같은 지점 = boundary 
