---
layout: post
title:  "[webGL virtual 3D spatial]"
subtitle:   "Digital Twin Classroom"
categories: graduationproject
tags: graduationproject
comments: true
header-img: img/post_img/spatial.jpg
---

- 목차
	- [Virtual 3D spatial Rendering 계기]
	- [Three.js 사용하기]
	- [webGL canvas 생성하기]
	- [필수요소 설정하기]
  

## 개요
> Virtual 3D spatial(가상 3D 공간) Rendering 하는 과정을 하나하나 나타낸 글 입니다.



## Virtual 3D spatial Rendering 계기
---
이번 digital twin classroom demo시에 실제 공간과 가상 공간 각각 rendering하여 보여주기로 하였다.
실제 공간은 실시간 360camera live web cam을 이용하여 만들어둔 web site에 띄워주기로 하였고 문제는 virtual 3D spatial을 rendering 하는 것이었다.
virtual 공간을 활용하기로 한 이유로는 free positioning을 비교적 쉽게 구현할 수 있을것 같다 생각하였기 때문이다.
따라서 virtual 3D spatial을 rendering 하기위해 필요한 기술은 어떤 것들이 있는지 알아보고 구현해 보기로 하였다.
Virtual 3d 공간생성시에는 openGL에서 만든 webGL을 사용하기로 하였다.
지난 학기 openGL수업을 듣고 3D 공간을 내 local 공간에서 자유로이 다루고 프로젝트도 경험해 보았기 때문에 이와 관련해서는 web page에 띄울수 없나 찾아보다가 webGL이란 3D API를 알게 되었다.
우선 대충 찾아보니 openGL을 다룰줄 아는 나에게 굉장히 도움이 될거란 기쁜 마음으로 시작을 하게 되었다.


## Three.js 사용하기
---
 처음 virtual 3D spatial 구상시에는 html5 canvas를 직접 조작하는 식으로 하려 했다. 그러다가 쉽고 시각적으로 더 보기 좋은 API 인터페이스를 가지고 있는 three.js를 알게 되었다. 따라서 이 api를 사용하기로 하였다.
 

## webGL canvas 생성하기
---
  생성한 프로젝트를 web page에서 띄워주기 위해서는 이를 보여줄 canvas가 필요하다. 우선 html에서 원하는 위치에 canvas를 선언해 주었다.
  이후 css에서 canvas의 크기나 모양, 테두리 색 등을 입혀준다. 그 다음 script로 가서 canvas에 띄우고 싶은 것을 javascript 문법으로 선언해 주었다.
  그러나 만들어둔 박스(canvas) 안에 프로젝트가 들어가지 않는다! 왜그럴까... 왜그럴까.....
  고생을 하여 해결을 하였다 ^^
  그 이유인 즉슨, 캔버스를 직접 만들시에 이를 three.js로 전달하지 않으면 렌더러가 임의로 캔버스를 만들기 때문에 나처럼 원하는 위치에 canvas를 만들 시에는 본인의 document에 추가하여야 한다.

  const canvas = document.querySelector('#c');            // ' '안에는 canvas 이름
  const renderer = new THREE.WebGLRenderer({canvas});

  이런식으로 말이다!

  전에 만들어둔 web page 내의 파란 canvas안에 움직이는 도형을 띄워보았다. 
  잘 작동이 된다. 이제 classroom을 띄워줄 canvas는 완성이 되었다~~


![webGL_img](/assets/img/post_img/webGL_img.png)


## 3D 그래픽 구성요소
---
 가상공간 만들기 프로젝트에 앞서 가장 기본이 되고 또 가장 필수적인 요소들을 알아보고 설정해 보았다.
 우선 오브젝트들을 놓을 공간이 필요하다. 물체를 설정하기에 앞서 물체를 띄워줄 canvas 설정을 말하는 것이다.
 다음으로 피사체가 필요하다. 이는 canvas에 띄워줄 모든 물체를 가리킨다.
 이들을 바라볼 시선인 카메라 역시 필요하다.
 마지막으로 빛이 필요하다. 빛이 없으면 어두운 화면만을 보여주기에 빛이 없으면 앞서 말했던 구성요소들이 의미가 없어지게 된다.
 
> 본격적인 프로젝트 시작에 앞서 설정 및 기본적인 구성에 대해 알아보았다. 아무래도 컴퓨터 그래픽스 설계 수업을 들은 나로써 이해하는데 큰 어려움은 없었다. 이제 기초적인 내용은 건너뛰고 본격적으로 프로젝트에 직접적으로 필요한 부분을 공부하며 진행해보겠다.

//예시
* __Three.js 사용하기__
 - 처음 virtual 3D spatial 구상시에는 html5 canvas를 직접 조작하는 식으로 하려 했다. 그러다가 쉽고 시각적으로 더 보기 좋은 API 인터페이스를 가지고 있는 three.js를 알게 되었다. 따라서 이 api를 사용하기로 하였다.