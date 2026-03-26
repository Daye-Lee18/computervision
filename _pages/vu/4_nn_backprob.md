# Neural Networks and Backpropagation 

* Linear classifier issues: one template for each class (visually), linear boundaries (geographically) -> not useful with complex data 
  * dimension expansion: linear classifier가 있는데, 데이터가 liear boundary로 분류할 수 없을 경우에는, feature space dim을 높이면 데이터를 분리할 수 있다. 
    * 극단적으로는 데이터개수만큼 확장하면 모든 데이터가 분류될 것이다. 
    * 예를 들어, imaginary number의 polar -> euler formula로 변환시켜서 데이터를 분리시킬 수 있고, 그 과정에서 데이터에 대한 손실된 정보는 없다. 
* Feautures: input-ouput을 직접적으로 연결시키지 않고 주로 높은 차원으로 보낸뒤에 representation
  * 보통, 극단적으로 n개 만큼의 dimension으로 안 보내도 특정 패턴이 있으면 어느 정도 크기에서 separable가능하게 된다.
  * 이미지 데이터; 원본 데이터의 dim이 기본적으로 커서 피처를 뽑은때 dimension을 오히려 줄인다. 
* Image clasifiwe with pre-extracted feautres
  * 원래 전통방식에서는 이미지 feature extractiom은 사람의 intuition으로 뽑고 그 feature와 클래스를 맵핑(학습)하는 방식인데, end-to-end 인공지능은 이 모든 과정을 컴퓨터가 하게한다. 
  * 문제는 그래서 인간의 개입을 최소화 하기 때문에, 어떤걸 발견했는지 설명하기 어려울 때가 있다. 성능은 잘 나오지만.
  * 따라서, data-driven approach방식을 취하는 딥러닝이라도,
    * 기존에 쌓아온 도메인 지식을 적극적으로 활용해서 적은 데이터로도 학습할 수 있도록 하는 것도 좋다
* XOR problem: '여러개의' perceptron layer( f(wx), 여기서 f는 activation fn) 으로 풀 수 있다. 힐튼 박사.
* Activation fn : 멀티레이어 쌓을때 중간에 activation fn을 사용하지 않으면 하나의 레이어나 다름 없기 때문에, 복잡한 문제를 풀기위해선 (예를 들어 xor이상의 ) nonlinear fn을 계속 사용해줘야함 -> 또 다른 역할이 있나?
* Computing gradients: loss -> w_n .... , chain rule 이용

* Backprop: 각 파라미터들의 기여도 계산
  * 에시) logistics Regression = linear perceptron + Sigmoid (이진 분류에 사용됨)
  * 뒤에서부터 계산하는 이유: loss에서 가까운 쪽부터 계산해야하니까. 실제 그래디언트 계산 upstream gradient는 항상 처음엔 1이라 계산 먼저
  * 각 노드에서 계산 
    * upstream 을 받고 local gradient를 계산해서 그 둘을 곱해서 앞으로 보낸다. 
    * 체크! Gradient at the same edge (노드) == original upstream gradients == downstream gradient Dimension the same 
* Backprop with vector and matrix
  * Upstream / downstream은 forward pass에서의 해당 지점에서의 Dim과 동일한 dim을 가짐. 
  * local gradient는 upstream과 downstream의 dim을 곱하면 된다. 
    
