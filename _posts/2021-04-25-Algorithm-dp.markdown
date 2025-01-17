---
layout: post
title:  "Algorithm DP"
subtitle:   "Algorithm DP"
categories: Algorithm
tags: review blockchain
comments: true
---

## 개요
> Algorithm DP 기본기부터 공부한 내용을 담은 글입니다.


## Algorithm DP 기본기
---

이번 알고리즘 공부 주제는 DP이며 간단한 이론부터 구현까지 해 보도록 하겠다.
우선 DP를 쉽게 설명하자면 피보나치 수열을 예로 들 수 있다. 
그러나 피보나치 수열을 일일이 다 계산하지 않고 이미 계산을 한 적이 있는 배열에 대해서는 값을 어느 한 배열에 저장해 두었다가 필요할 때 꺼내쓰는 식으로 진행을 해야 실행시간에 많은 단축이 된다. 

몇개의 예제를 풀어보기로 하였다. 



# 백준 1463번
X가 3으로 나누어 떨어지면, 3으로 나눈다.
X가 2로 나누어 떨어지면, 2로 나눈다.
1을 뺀다.

- 풀이 
횟수 f(n)에 대하여 min( f(n/3)+1, f(n/2)+1, f(n-1) +1 ) 을 구하였다. 여기서 n/3, n/2는 나뉘어 떨어지는 경우에만 가능하다.  
![1463](/assets/img/algo/1463.PNG)



# 백준 9465번
- 스티커 떼기

이 문제에서는 2중 배열을 선언하여 DP를 짜는 문제입니다. 파이썬으로 2중배열을 선언해본지가 좀 오래되어서 시간이 걸렸지만 점화식을 세우고 문제를 푸는데는 큰 문제가 없었습니다. 
우선 이중배열을 선언하는 법!

dp = []     # 배열 선언
for _ in range(2):
    dp.append(list(map(int, input().split())))

이렇게 배열을 append하여 세웠습니다.
또한 배열의 값으로 각 단계까지의 최대값을 가지게 하며 갱신을 해 주었습니다.
점화식은 f(n)을 구하는 데 있어서 f(n-2)와 f(n-1)을 비교하여 더 큰값으로 갱신하였습니다. 

![9465](/assets/img/algo/9465.PNG)



# 백준 2294번
- 동전 최소개수 구하기

처음 문제를 보면 그리디 알고리즘을 이용하여야 하나 싶었지만 마냥 그리디적으로 접근을 하면 예시와 같이 15와 같은 수가 주어졌을 때 발생할 수 있는 문제가 있다. 
result[j] = min(result[j], result[j-coin[i]]+1)
정답을 나타내는 배열을 점화식 함수를 통해 계속해서 갱신 될 수 있도록 만들었다. 그리디와 다른 점은 for문을 통해 모든 coin에 대해 배열을 업데이트 해 주었다는 점이다. 
![2294](/assets/img/algo/2294.PNG)




# 백준 12865번 knapsack
- 배낭에 들어갈 최대의 가치 구하기

이번 문제는 knapsack의 대표적인 기본 문제라 할 수 있다. 사실 예전에 knapsack 이론을 공부한 적이 있어서 처음에는 고전을 하였지만 아주 조금의 해설을 보고서 해결할 수 있었다. knapsack의 이전 문제들과의 가장 큰 차이점은 전에는 dp라는 1차원 배열을 update해 주었지만 이번 문제에서는 2차원 배열 dp를 update해 주었다. dp[i][j]에서 i 는 돌멩이 개수를, j는 최대 가치를 나타내었다. 따라서 개수에 따라 최대 가치를 update하면 되는 문제였다. 
![12865img](/assets/img/algo/12865image.PNG)
![12865](/assets/img/algo/12865.PNG)




# 백준 11055번 증가부분수열
- 증가하는 부분 수열중에 합이 가장 큰 값을 리턴

이번문제는 증가하는 부분 수열중에 가장 큰 값을 리턴하는 문제로 처음 접해보는 유형이었지만 검색해보니 꽤 유명한 유형의 문제였다. 처음에 dp의 값이 이상하다 여겨서 애를 먹긴 했지만 이내 해결을 하였다. dp[i]에서 i번째 배열을 꼭 포함을 하는 수열중에 i보다 작고 증가하는 증가부분수열을 만들고 그렇게 나온 dp수열에서 max값을 리턴하면 되는 문제였다. 
![11055](/assets/img/algo/11055.PNG)




# 백준 11051번 이항계수
- 이항 계수 (n, k)를 구하는 문제

우선 이항계수를 잘 몰랐다... 이항계수에 대한 개념은 구글링을 통해 배우기로 했다. 
![11051](/assets/img/algo/11051.PNG)
이런 식의 규칙이 있었다. 
규칙을 보니 쉬운 문제일 거라 생각하고 풀기 시작했다.
그러나 배열을 선언하는데 어려움이 있었다. dp[5][2] 이런 식으로 배열을 선언하고자 하였다.
따라서 dp =[], dp.append([1]*(n+1)) 과 같은 방식으로 점점 배열 내 배열의 크기가 증가하도록 선언해 주었다.
이후의 점화식을 세우는 과정은 어렵지 않게 세울 수 있었다.
![11055](/assets/img/algo/11051-1.PNG)




# 백준 11057번 오르막수
https://www.acmicpc.net/problem/11057
- 오름차순으로 되어있는 수의 개수를 숫자의 길이가 주어졌을때 구하는 문제이다.

배열을  선언하는데 있어서 애를 먹었다ㅠㅠ 아직도 이런부분에서 헤매다니..
배열 선언은 2중배열이긴 한데 안에 있는 배열은 각 자리수에서의 몇번째를 나타낸다.
두자릿수 이면  dp = [[ 0, 0, 0, 0, 0], [ 1, 1, 1, 1, 1]] 이렇게 나타낸다.
배열 선언은 그렇고 이 문제에서는 가장 마지막 자릿수를 기준으로 점화식을 세워야 더 이해하기 쉽게 풀 수 있다.
dp[i][j] = dp[i-1][j] + dp[i][j-1] 이런 점화식을 세워서 문제를 풀어나가면 된다.
![11057-1](/assets/img/algo/11057-1.PNG)
![11057](/assets/img/algo/11057.PNG)




# 백준 10844번 쉬운계단수
https://www.acmicpc.net/problem/10844

 - 위의 문제와 유사한 유형으로 모든 자리수의 차이가 1이 나는 수의 개수를 찾는 문제이다.
점화식으로는 우선 이중 배열 dp[i][j]가 있을때 전 자리수에서 1씩 차이나는 j+1, j-1부분을 더해주면 되는 문제였다.
dp[i][j] = dp[i-1][j-1] + dp[i-1][j+1]
![10844](/assets/img/algo/10844.PNG)
