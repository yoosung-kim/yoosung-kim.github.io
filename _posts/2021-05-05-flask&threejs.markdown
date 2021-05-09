---
layout: post
title:  "[Flask & Three.js]"
subtitle:   "Digital Twin Classroom"
categories: graduationproject
tags: graduationproject
comments: true
header-img: img/post_img/spatial.jpg
---

- 목차
	- [flask 백엔드]
	- [Three.js 사용하기]
	- [flask를 이용하여 Three.js 동적으로 나타내기]
  

## 개요
> Flask를 이용하여 백엔드를 구축한 후에 처리된 영상을 통해 Three.js를 이용하여 웹페이지에 동적으로 obj 등을 띄워주는 작업을 하였습니다. 



## Flask 이용하기
---
우선 flask를 쓰게된 계기는 360카메라로 frame 단위로 웹에 띄워주는 것은 가능하나 얼굴이 인식된 프레임을 보고자 시작하였다. 웹 애플리케이션에 주로 쓰이는 것은 Django와 Flask인데 우리는 비교적 가벼운 framework인 flask를 이용하기로 하였다.
 전에 학교 프로젝트로 jsp나 DataBase 등을 이용한 웹페이지를 만든 경험은 있으나 웹 어플리케이션을 다뤄본 경험은 전무하여 이번 프로젝트에서 내가 제일 큰 열의를 가지고 하겠다고 나섰다!


## Flask란
---
웹 브라우저에서 URL을 방문하면 서버에 요청을 보내고, 서버는 그 요청을 처리해서 브라우저에 응답을 반환하게 된다. 그 반환된 결과를 HTML 문서로 보내주면 그 웹 페이지를 브라우저가 띄워주는 것이다. 이같은 과정을 제대로 된 구조로 만들려면 일관된 구조와 기능을 가진 템플릿을 활용해야 한다. 
메인 python 파일으로 app.py라는 파이썬 파일을 생성하자. 이후 templates라는 폴더를 생성하고 안에 index.html 파일을 생성하였다. url을 render_template 함수를 이용하여 경로를 index.html로 연결되도록 하는 것이다. 
나는 추가적으로 프로젝트에서 필수적인 부분인 streaming된 canvas를 메인 html에 띄워야 하므로 flask 내에서 처리된 frame을 받아오는 것을 하나의 요청으로 하고 그 요청에 대한 응답부분을 웹의 캔바스에 띄워주는 식으로 진행하였다. 



## Flask 구조 
---
간단한 flask의 구조에 대해 말해보자면 html이 들어가야할 templates와 이미지, js, css 등 링크를 통해 참조하는 파일들이 들어가야할 static 폴더로 구성된다. 
html을 templates 폴더 안에 두어야 render_template 등의 함수를 사용하여 동적인 페이지를 생성할 수 있게 된다. 



## Three.js 사용하기
---
flask 구성을 완료한 뒤에는 포르젝트의 최종 데모시에 보여주고자 하는 가상 환경을 만들기 위해 Three.js를 사용하였다.
이는 지난 포스팅에서 마지막에 언급을 한 바 있는데 웹페이지에 3D 객체를 쉽게 렌더링하도록 도와주는 java script 라이브러리이다. 
three.js를 사용하여 렌더링 하고자 하였던 내용은 3D로 만든 사람의 얼굴과 책상, 큐브맵으로 만든 공간, 사람의 이름을 출석 유무에 따라 나타내기 등이었다. 
미리 생성해둔 3D 얼굴과 책상을 렌더링 한 후에 이름을 머리 위에 띄워줄 수 있도록 3D Text를 생성하고 위치를 조정해 주었다. 
광원 설정, obj parsing, cube map을 통한 공간구축 등을 완료하였다. 





## flask를 이용하여 Three.js 동적으로 나타내기
---
flask에서 계속해서 매 웹캠 프레임마다 얼굴인식을 진행하고 있기 때문에 학생이 웹캠에 잡히면 파란 이름을, 잡히지 않으면 결석을 뜻하므로 빨간 이름을 띄워주었다. 
굉장히 반영이 잘 되었다!
다음 데모시에는 출석  UI와 database를 생성하여 application을 만들어 보겠다.
![gif_img]](/assets/img/post_img/class_gif.gif)

