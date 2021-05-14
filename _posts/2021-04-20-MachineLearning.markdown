---
layout: post
title:  "MachineLearning Lect 5-7"
subtitle:   "MachineLearning 공부"
categories: MachineLearning
tags: MachineLearning
comments: true
header-img: img/spring/springboot.PNG
---

## 개요
> Lecture Summary 5-7

- 목차
	- [CNN이란](#) 
	- [고전 모델 소개](#) 
	- [Object detection](#)


* CNN의 필요성
 - 기존 input image를 단순히 flatter하게 일렬로 이미지 정보를 늘여뜨려서 입력값으로 넣으면 상대적으로 가까운 거리에 있는 픽셀 정보들이 멀어지게 되고 이에 따라 공간상의 정보가 무너지며 공간 영역을 잘 표현할 수 없다는 한계가 있다. 따라서 convolution neural network에서는 weight matrix를 2차원 벡터로 만들어서 공간상의 정보를 표현할 수 있도록 설계하였다.  
우선 CNN 역사를 먼저 살펴보기로 하였다. Simple cells, complex cells, hypercomplex cells를 고양이에게 보여주고 고양이의 뇌파를 분석하는 과정에서 빛에 반응하거나 움직임에 반응하고 end point에 반응하는 등의 결과를 보고 이를 표방하여 CNN의 이론을 적립하는데 많은 도움이 되었다고 한다.  
Convolution을 사용한 딥러닝으로는 LeNet이 젤 먼저 소개가 되었다. 이는 input image를 convolution하고 subsampling과 같은 작업을 하여 output을 내었다. 다음으로 Deep convolution Neural Network로 AlexNet이 소개가 되었다. AlexNet을 포함한 다양한 모델들의 자세한 소개는 다음 페이지에서 하기로 하자.  CNN은 꾸준히 발전하여 다양한 형태로 나타나고 있다. Image뿐 아니라 다양한 신호들을 변형시켜서 CNN에 적용도 가능하다.  


* CNN의 구동 원리
- Fully Connected Layer
 이는 input image를 flatten 시켜서 weight parameter과 곱하여 결과를 내는 것이다. 이러한 과정으로 나온 결과들은 각각 하나의 dot product의 결과이다. 그런데 위에서 input을 flatten시키지 않기 위하여 cnn을 도입하였다고 하였는데, 왜 여기서는 flatten을 시키는 것인가??  
그 이유로는 예를 들어 cnn의 결과로 image classification과 같이 각 클래스별 결과를 도출해 내어서 나온 결과와 Ground Truth와 비교를 하는 등의 과정이 필요하기 때문이다.  


- convolution Layer
 input image와 channel 개수가 같은 convolution filter로 input image에 대해 filtering을 하는 layer이다. 이때 기존의 weight parameter을 통과하면서 계산하는 과정과는 달리 공간상에서 인접하게 붙어있는 픽셀들 간의 관계를 모아준다는 장점이 있다. 이러한 과정들을 거치면 Filter가 input image를 지나가면서 계산한 결과가 나온다. 이때 모든 과정에서 동일한 filter을 사용하므로 weight를 공유하게 되고 Input에 비해 filter size가 작으므로 작은 parameter을 사용하여 결과를 낸다는 장점이 있다. 이렇게 한번의 fiilter을 거치면 channel이 1인 activation map이 생성된다. 만약 여러 개의 filter을 사용한다면 activation map이 filter 개수만큼 생기게 되는 것이다. 또한 한번의 ConvNet을 거친 다음에 activation function을 넣게 된다. 주로 Relu function을 넣는다. 마지막에는 위에서 FC layer을 설명할 때 언급하였듯이 각 class별 score을 내야 하므로 FC layer을 거치게 된다.   
그렇다면 filter을 여러 개 겹쳐서 사용하는 이유가 무엇일까? 그 이유로는 각 filter마다 잘 탐지하는 부분이 다르므로 서로 다른 형태의 pattern을 찾기 위해 여러 개를 사용한다.  
그런데 convolution layer을 계속해서 거치게 되면 image의 width와 height가 줄어들게 된다. 이를어떻게 해결해야 할까?   
여기서 stride개념이 나오는데 이는 fitler가 점프하는 칸의 수를 나타낸다. 만약 stride가 1이고 image가 7*7, filter가 3*3이면 5*5의 output이 나오게 된다. 만약 stride가 2이면 3*3의 결과가 나오게 된다. 이를 공식화하면 (N-F) / stride +1이 된다. 여기서  stride를 3으로 늘려주면 소수점이 나오므로 계산이 어렵게 된다. 이를 방지하기 위해 padding을 해줄 수 있다. padding이란 input image를 감싸는 의미 없는 영역을 추가해 주는 것인데, 주로 0을 사용하게 된다. 여기서 padding의 주된 목적은 input image의 size를 줄이지 않기 위함이다. 그렇다면 바로 앞 단락에서 의문을 품었던 부분에 해결책을 줄 수 있다. Convolution layer을 거치더라도 size가 줄어들지 않는 방법이 생긴 것이다. padding까지 고려하여 Convolution layer을 통과한 직후의 output volume을 구하는 공식은 W, H = (N-F+2P)/stride + 1이 된다. Depth는 filter의 개수가 된다.   
사용되는 parameter 개수는 어떻게 될까? 이는 filter의 volume에 각 filter당 bias가 1개씩 들어가고 이를 filter의 개수와 곱해주면 된다. 처음 convolution filter의 사용 목적에 대하여 인접한 픽셀들 간의 공간 정보를 유지시키는데 있다고 하였다. 그런데 크기가 1*1 filter들은 왜 사용을 하는 것인가? 1*1 filter은 차원을 축소, 확대시킨다는 장점을 가지고 있다. 우선 한번의 1*1 filter을 거치게 되면 width와 height는 그대로 두고 dimension만 1로 줄어드는데 여러 개의 filter을 거치면 filter 개수만큼의 dimension이 생기게 되는데 이 개수가 기존의 차원보다 크면 차원의 확대, 기존의 차원보다 작으면 차원의 축소가 일어나게 되는 것이다.   


- pooling layer
 아는 정보를 압축하기 위한 과정으로 image를 더 작게 만드는 것이라 할 수 있다. 그러나 공간상에서만 down sampling을 하며 channel방향으로는 고려를 하지 않는다. Pooling layer을 거치면 image가 가벼워지므로 batch size를 올릴 수 있는 등의 이점이 있다. 대표적인 예로 max pooling이 있는데 예시로 2*2 filter로 stride 2를 주게 되면 2*2 픽셀에서 가장 큰 값 만을 취하여 새로운 image를 만드는 것이다. Pooling의 결과는 앞에서 convolution layer을 거친 후의 결과와 동일한 연산과정을 통해 width, height가 나오게 되고 channel은 그대로 된다. 하지만 필요한 parameter 개수는 0개이다. 그 이유로는 풀링 과정은 단순 연산이기 때문이다.  
이제 앞서 언급하였듯 다양한 CNN Architectures에 대하여 알아보기로 하자. 우선 기본적으로 유명한 CNN 모델 예시로는 AlexNet, VGG, GoogLeNet, ResNet이 있고 이들을 먼저 알아보겠다.  


- AlexNet
 가장 최초의 CNN 기반의 ImageNet challenge winner이다. 설계된 내용을 보면 되게 난잡하게 되어있는데 그 이유로는 많은 시행착오를 겪으면서 실용적으로 설계되었기 때문이다. 여러 개의 convolution layer과 pooling layer가 있고 마지막에는 3개의 fc layer가 있다. 여기서 마지막 fc layer을 지날 때 image를 늘어뜨린 다음 원하는 개수의 class score로 변환하게 되는데 이때 필요한 weight parameter가 많이 필요하다. Class수 * input image의 size만큼 필요하다는 단점이 있다.   


- VGG
 우선 VGG는 기존의 모델들 보다 더 깊어진 networks를 사용한다.(16개, 19개) 그런데 이때 각각의 conv layer은 3*3layer 만을 사용한다는 점이 특이하다. 따라서 전체적인 모델의 결과를 보게 되면 굉장히 질서 있게 정돈된 느낌을 준다. 그렇다면 왜 이런 작은 filter을 사용했는데 결과가 더 좋을 수가 있을까? 우선 이론적으로 1개의 7*7 filter과 연속된 3개의 3*3 filter은 결과적으로 커버하는 영역(receptive field)가 같다. 그러나 small filter을 더 많이 사용하면 더 깊어지고 non-linearity가 더 늘어난다는 장점이 있다. 매 convolution layer을 지날 때마다 activation function을 추가해주기 때문이다.  또한 3*3 filter가 7*7 filter보다 적은 parameter가 들어가므로 메모리적인 면에서 더 좋은 기법이라고 할 수 있다. 전체적인 모델의 진행과정을 살펴보면 처음 convolution layer에서 대부분의 memory가 있는 것을 알 수 있다. 이는 점점 layer을 거치면서 memory가 줄게 되므로 처음부분에 대부분에 들어있게 된다 볼 수 있다. 또한 마지막부분에서 fc layer을 거칠 때 필요한 parameter개수가 input size * class수 만큼 필요하므로 아주 많은 파라미터가 필요해서 많은 memory가 소요된다는 단점이 있다.   


- GoogLeNet
우선 이 모델의 특징을 먼저 말해보자면 이 모델은 22 layer을 사용하였고, VGG 보다는 확연히 줄어든 parameter개수, fc layer가 없다는 특징이 있고, 또 하나 큰 특징으로 inception module을 사용하였다는 것이다. Inception module의 의미는 한 module을 거치고 또 module을 거치고 또 거치는 등 계속해서 모듈 속으로 들어간다는 의미이다. 하나의 inception module을 파헤쳐 보았다. Input을 여러 convolution filter을 병렬적으로 적용하여 일렬로 붙여서 output이 되는데 단순히 일렬로 이어 붙이는 concatenation을 하게 되면 너무 많은 연산과 연산 결과와 output size가 너무 커지게 된다. 따라서 3*3 convolution을 하기 전에 1*1 convolution을 끼워 넣어서 depth를 줄여준 다음 연산을 시도하였다. 그 결과로는 1*1 convolution의 효과에 대해서는 앞서 설명했듯이 차원을 줄여줄 수 있어서 결과적으로 하나의 inception module에서 해야 하는 연산량이 줄어들게 된다. 여기서 주의할 점은 결과값의 크기는 줄어들지 않는다는 것이다. 왜냐하면 연산량이 줄지만 depth는 3*3 conv layer의 개수에 의해 정해지기 때문이다. 이러한 과정들은 googlenNet의 deep한 learning을 하는데 있어서 매우 중요한 역할을 하게 된다. 이처럼 연산량을 줄여주지 않으면 back propagation을 하는 과정에 있어서 시간도 오래 걸리고 잘 진행이 되지 않는다.  
앞서 언급하였던 것들 중 fc layer가 없는 것이 한 특징이라 하였는데, GoogLeNet에서는 모든 convolution 곱을 거치고 나서 global average pooling을 하게 된다. 이는 예를 들어 마지막 convolution의 output으로 H*W*c가 나왔다고 하면 GAP를 거치면서 1*1*c로 변하게 된다. 기존에 모델들이 fc layer을 거치면서 많은 파라미터가 필요했던 것과 굉장히 대조적이면서 획기적이라 할 수 있다.   
GoogLeNet의 또 하나의 특징으로 Auxiliary classification이 있다. 이는 GoogLeNet이 너무 많은 layer들을 사용하기에 back propagation시에 시간이 오래 걸림, 학습이 잘 안됨 등의 문제를 해결하고자 layer 중간중간에 보조할 수 있는 장치를 만들어 두었다고 할 수 있다. 예를 들어 layer 중간에 두개정도의 Auxiliary classification을 만들어 두었다고 할 때, 두개의 Auxiliary classification에서 나온 loss가 L1, L2라 하고 마지막에 나온 결과로 L3라 하면 전체 Loss = L1 + L2 + L3 가 된다. 또한 back propagation 시에 각각의 Auxiliary classification에서 독립적으로 아래로 back propagation을 진행하게 된다. 또한 각각의 Auxiliary classification 마다 가중치를 줘서 Loss에 미치는 비율을 달리 할 수 있다.  


- ResNet
 그 다음으로 소개할 모델은 ResNet이다. 우선 기존 모델들과는 달리 ResNet의 layer은 152개로 비약적인 depth의 혁명을 이뤄냈다. 어떻게 이렇게 depth가 많이 차이나는 모델을 만들수 있었던 것인지 알아보았다.  
우선 깊은 depth를 만들게 된 계기는 많은 layer을 쓰면 더 결과가 좋아지는 것은 자명하나 학습시키기 어렵기 때문인데 이를 보완하기 위해 Residual block이란 장치를 사용하였다. 이는 기존의 convolution layer F(x)을 거치고 나면 어떤 함수 H(x)가 나온다고 할 때, 기존에는 H(x)를 학습시켜서 Loss를 줄이는 방향으로 진행하였다면, Residual block은 F(x)를 학습시켜서 Loss를 줄이는 방향으로 진행하게 된다.   
ResNet은 GoogLeNet과 비슷하게 차원을 줄이는 1*1 convolution도 사용하는데 3*3 convolution 전, 후로 1*1 convolution을 하여 차원을 줄여 계산량을 줄인 후, 다시 차원을 복구 시키는 형태로 사용하게 된다. 이는 깊은 layer을 사용하는 모델들에게 필수적인 요소라 할 수 있다. 이 과정이 있으므로 깊은 layer을 사용할 수 있는 것이다. 이를 bottleneck라 부른다.  
또한 ResNet은 Batch Normalization의 과정도 거친다. 이를 간단히 먼저 말하자면 학습시에 minibatch를 한 단위로 정규화를 하는 것이다. 이를 사용하는 이유는 우선 학습 속도가 높아져서 효율이 올라가고 매 학습시 마다 출력값을 정규화 해주기 때문에 가중치 초기 선택시에 너무 힘을 들이지 않아도 된다. 또한 ResNet이 dropout과 같은 기법을 사용하지 않는데 batch normalization을 통해 과적합을 방지하며 dropout과 같은 기능을 대체할 수 있게 된다. 이 과정을 알아보도록 하겠다. 이는 각 layer에서 데이터의 분포를 정규화 하는 작업을 한다고 할 수 있는데 마치 noise를 넣어주는 것과 같은 방법으로 학습을 할 때마다 활성화 값과 출력 값이 정규화 되기 때문에 초기화의 문제에서 비교적 자유로워진다고 할 수 있다. 각 hidden layer에서 정규화를 하면서 입력분포가 일정해지고, 이에 따라 Learning Rate를 높여도 괜찮아진다. 그 결과로 학습속도가 빨라지게 되는 것이다.   
이와 같이 다양한 기법들을 사용하며 VGGNet, GoogLeNet의 장점들을 모두 취하며 FC layer을 사용하지 않고 GAP를 사용하여 결과를 도출해 내는 모델이다. 
4개의 Network 모델에 대해 알아보았다. 다음으로 더 fancy한 모델들의 과정에 대해 알아보고자 한다. ResNet에서 소개하였던 residual block이란 기법이 있었다. 이 기법에서 더 발전한 기법으로 Wide Residual block이란 것이 있다. 이의 동작과정은 기존 residual block의 3*3 conv에서 filter개수를 늘린 것으로 약 50개의 wide residual block이 152개의 residual block보다 성능이 좋게 나왔다. 또한 residual block과 비슷한 원리로 input x를 모든 layer에 다 더해주는 Dense block도 생겨났다.  
Convolution 곱의 다른 형태도 알아보고자 한다.   


- Dilated Convolution 
 기존의 convolution곱은 가장 인접한 픽셀들을 한 곳으로 매핑해주는 식으로 진행이 되었다면 이는 몇 칸씩 떨어진 것들과 컨볼루션 곱을 하여 매핑을 하는 식으로 진행이 된다. 이 과정의 장점으로는 같은 weight parameter을 사용하여 커버하는 영역을 넓힐 수 있다는 장점이 있다.   


- Separable Convolution
 이 기법은 input image를 기존에는 3*3kernel에 통과하는 식으로 output image를 생성하였다면, 3*3이 아닌 3*1 conv곱을 하고 그 결과를 1*3 conv곱을 하는 식으로 각각을 진행하는 것이다. 이와 비슷한 방식으로 Depth-wise Separable Convolution이 있다. 이는 channel별로 image를 분리하여 각각 convolution을 진행하고 합친 후 1*1filter를 통과시켜서 depth를 1로 만들어주는 것이다. 이러한 과정을 통해 연산량이 줄어들고 시간도 줄어들게 된다. 비슷한 방식으로 Grouped Convolution이 있다. 이는 input image에 대해 쪼갠 후 conv를 통과시킨 후 합치는 것으로 계산 효율성이 높아진다는 장점이 있다.  


- semantic segmentation
 기존의 classification은 영상 내 물체를 단순히 labeling하는 것이라면 semantic segmentation는 모든 pixel에 대해서 segmentation을 진행하는 것이다. training시에 모든 픽셀에 대해 labeling을 해 놓은 후 test시에 추출한 픽셀들을 cnn을 통과시켜서 label을 얻는 식으로 진행이 된다. 그러나 모든 pixel에 대해 진행을 하기 때문에 너무 많은 parameter가 필요하게 된다. 따라서 그냥 conv layer을 통과시키지 않고 down sampling을 한 후 통과시키고 다시 up sampling을 하여 결과를 얻는 방식이다. 이때 up sampling 하는 방식은 unpooling을 주로 사용한다. 이는 pooling과 반대되는 개념이라 생각할 수 있다. 하지만 semantic segmentation에는 단점이 있는데, 같은 label의 두 물체가 붙어있는 경우 이를 분리시켜서 인식하지 못한다는 점이다.   


- object detection & Instance Segmentation
 우선 object detection은 classification과 localization을 모두 하는 것이다. Classification은 cnn을 거친 output image를 class score을 매겨서 Loss를 구하는 과정을 진행함과 동시에 Localization을 해주면서 좌표를 찍어서 object의 위치를 파악하는 것이다. 또한 기존의 semantic segmentation에서는 여러 개의 object를 detection할 수 없었지만 여러 개의 object를 detection할 수 있다. 그러나 너무 많은 crop된 image를 cnn에 통과시키기 때문에 computational 문제가 생긴다. 이에 따라 생겨난 것이 Region Proposal이다. 이는 object가 포함 될 것 같은 구역을 미리 찾아서 그 image에 대해서만 cnn을 적용시키는 selective search 방식이다. 약 2000구역을 선택적으로 뽑아서 cnn에 적용시키기 때문에 굉장히 빠르게 진행이 된다.   이 과정을 조금더 자세히 살펴보겠다. 우선 2000개의 ROI를 추출한 후에 같은 크기로 resize를 시킨다. 이후에 같은 convNet에 적용시켜서 결과를 얻는다. 나온 결과로 SVM을 적용시켜서 classification을 진행한다. 그러나 이러한 과정도 이미지 2000개를 모두 각각 convNet에 적용시키기 때문에 오랜 시간이 소요된다. 따라서 나온 것이 fast R-cnn이다. 우선 input image 전체를 convNet에 적용시킨 다음 기존의 ROI에서 줄어들거나 늘어난 비율을 비례식 등을 이용해 파악하여 ROI를 파악하여 crop하고 resize시킨다. 이후 divide 하여 max pooling을 진행한다. 그 다음에 Linear+softmax를 적용시킨다. 실행시간을 측정해본 결과 fast R-cnn의 test time이 많이 줄긴 하였으나 region proposal을 하지 않았을 때 시간이 너무 줄어들 수 있는 것을 보고서 faster R-cnn을 고안해 낸다. 이는 image를 cnn에 적용시킨 후 Region Proposal을  Network에 포함시킨다. 이후 classification과 bounding box loss를 계산하고 두번째 스텝으로 또 classification과 bounding box loss을 진행시킨다. 첫번째 스텝에서는 object 인지 아닌지와 같은 간단한 classification을 하고 두번째 스텝에서는 어떤 object인지와 bbox는 미세조정까지 하게 된다. 이렇게 해서 나온 test-time은 매우 적은 시간이 소요되는 것을 확인할 수 있다. Instange Segmentation은 faster R-cnn에서 Mask prediction을 추가한 것으로 픽셀단위의 자세한 object detection이 될 수 있다. 추가적으로 예를들어 사람에 대해서 관절의 위치까지 파악 할 수 있는 모델들도 개발 되었다.   
