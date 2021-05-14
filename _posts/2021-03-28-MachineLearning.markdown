---
layout: post
title:  "MachineLearning Lect 1-4"
subtitle:   "MachineLearning 공부"
categories: MachineLearning
tags: MachineLearning
comments: true
header-img: img/spring/springboot.PNG
---

## 개요
> Lecture Summary 1-4

- 목차
	- [Machine learning이란](#) 
	- [다양한 Machine learning 모델](#) 
	- [Loss 계산을 위한 다양한 기법](#)


## Machine learning이란
---
 - 지도학습   
 : 정답이 있는 데이터를 활용하여 데이터를 학습시키는 방법입니다.  
예를 들어 입력 값이 주어지면 입력 값에 대한 label을 주어 학습시키며 대표적으로 분류, 회귀가 있습니다.  
1) 분류(classification)  
주어진 데이터를 정해진 label에 따라 분류하는 것.   
이진 분류 / 다중 분류 문제가 있다.  
2) 회귀(regression)  
주어진 데이터들의 feature을 기준으로 그래프를 예측하여 패턴이나 경향 등을 예측하는 것.  


 - 비지도 학습  
 :  정답 label이 없는 데이터를 비슷한 특징을 가진 데이터끼리 군집화 하여 새로운 데이터에 대한 결과를 예측하는 것. 대표적으로 clustering, GAN 등이 있다.  

 - 선형 회귀 (Linear Regression)  
 : 독립 변수 x, 종속변수 y가 있을 때 x값을 토대로 y값을 추출해 내기 위하여 x값들의 특징을 잘 나타내는 직선을 그려내는 과정. 이때 도출한 직선이 y = ax + b라 할 때 최적의 a, b를 찾아내는 과정이라고도 할 수 있다.  

 - 최소 제곱법(linear least squares)  
 : x, y를 이용하여 기울기 a를 알아내는 방법.  

 - 평균 제곱 오차(MSE)  
 : 도출해낸 식의 기울기가 잘 그려졌는지 평가하여 조금씩 수정해 가기 위한 수단. 오차가 작을수록 좋은 모델이므로 이 계산 결과가 가장 작은 선을 찾는 작업이 중요하다.  
즉, 선형회귀란 임의의 직선을 그어 이에 대한 평균 제곱 오차를 구하고 이 값을 가장 작게 만들어주는 a, b를 찾는 작업이라 할 수 있다.  
 
 - Nearest Neighbors  
: 새로운 데이터를 입력 받았을 때 가장 가까이 있는 것이 무엇인가를 중심으로 새로운 데이터의 종류를 정해주는 알고리즘.  
  inter class : 클래스간 분산 정도  
  intra class : 클래스 내부의 분산 정도  

 - KNN 알고리즘
 : 데이터로부터 거리가 가까운 k개의 다른 데이터의 label을 참조하여 분류(classification)하는 알고리즘
간단하고 구현하기 쉬운 장점. 데이터가 많아질수록 분류속도가 느려지고 계산량이 많아지는 단점이 있다.  
여기서 k는 hyper parameter에 해당한다.  

 - Linear Classification
 : 선을 이용하여 두개 이상의 집단으로 분류하는 것.  
 
작동 원리 : 위의 그림에서 input image인 3072차원의 벡터를 넣어주면 Linear classifier을 거쳐서 분류 해야 할 class의 개수인 10개의 벡터가 나오게 됩니다. 여기에 bias를 더해주게 되면 classifier가 예측한 값이 나오게 됩니다.  
최종 목표 : 정확도 score를 높이기 위해 최적의 Weight값을 설정하는 것. Loss function을 줄이는 것.

 - Deep neural network  
 : 여러 개의 Linear classifier을 합쳐 놓은 것  
		
 - SVM(support vector machine)
: 분류를 위한 기준 선을 정의하는 모델.  
Margin : 결정 경계와 서포트 벡터 사이의 거리  
정답 클래스가 아닌 다른 클래스 스코어보다 margin 이상이어야 loss가 발생하지 않는다.  
-> 데이터 포인트 중에서 서포트 벡터만 잘 골라내면 나머지 수많은 데이터 포인트들을 무시할 수 있다. 따라서 속도가 매우 빠르다  
개별적인 학습 데이터들을 모두 포함시키기 위해 마진을 작게 잡으면 overfitting이 발생할 수 있다.  
또한 그 반대로 마진을 너그럽게 잡으면 서포트 벡터와 결정 경계 사이의 거리가 멀어져서 underfitting이 발생할 수 있다.  
하지만 이 알고리즘은 확률로 표현하기가 힘들다. 따라서 이를 확률로 바꾸기 위해 softmax function을 사용한다.  

 - Softmax function
: 분류 해야하는 정답지의 개수를 k라 할 때, k차원의 벡터를 입력 받아 각 클래스에 대한 확률을 추정하는 것.  
Svm function에서 나온 값을 exp를 취하고 정규화를 한 후 크로스 엔트로피 함수에 대입합니다.   


 - Gradient descent(경사 하강법)
: cost 함수의 그래프가 포물선인 경우에 경사를 내려가며 W를 찾기 위한 방법.  
최소화 문제의 경우에 많이 사용하며 변수가 많을 경우에도 사용한다.  
기울기가 양의 값이면 W를 감소시키고, 음의 값이면 W를 증가시키는 결과  

f = Wx 만으로 W를 구하면 계산이 복잡하다  
>	Computational graphs + backpropagation  

 - Backpropagation(역전파)   
: upstream gradient를 이용하여 downstream gradient를 구하고 downstream gradient가 다시 upstream gradient가 되어서 역으로 구해가는 알고리즘.  
중간에 sigmoid local gradient같은 과정이 나열되어 있다면 이를 한번에 구할 수도 있다.  

 - Regularizaion
: 모델에 제약을 주는 것. 완벽한 fitting을 피하고 높은 complexity를 피하기 위하여 쓰는 방법.  
 대표적으로 L1, L2 Regularization이 있다.  

 - Data Preprocessing
: 일반적으로 평균을 0에 맞추고 각 축의 스케일을 맞춰주는 작업을 한다.  

 - Weight initialization
: deep neural network에서 local minimum이 아닌 optimum으로 수렴하기 위한 중요한 설정.  
또한 활성화 함수로 여러 함수 중에 하나를 선택하게 되는데 그중 tanh를 선택한 경우 W를 너무 작게 설정하면 layer을 거칠수록 값이 너무 작아지는 현상이 나타난다.  
ReLU함수를 사용한 kaiming/MSRA initialization의 경우 sqrt(2/Din)을 곱해주게 되는데 이 initializaion은 layer을 거쳐도 scaling이 잘 된다.  

 - Stochastic Gradient Descent
: Loss function을 계산할 때 전체 데이터가 아닌 일부 데이터(mini-batch)의 모음을 사용하여 loss function을 계산하는 것.  계산 속도가 빠르고 local minimum에 빠지지 않고 더 좋은 방향(Global minimum)으로 수렴할 가능성이 높다.  
 epoch : 전체 data set을 몇 번 학습시킬 것인가  
 batch size : 전체 data set을 나눈 것 중 하나의 sub set size  
 iteration : batch 의 n번째 수  

  - Optimization
 : 여러 종류의 optimizer가 있으며 위에서 설명한 gradient descent, SGD 모두 이 예시이고 SGD를 보완하기 위해 SGD에 momentum을 더해준 것도 있다.  
  