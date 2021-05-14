---
layout: post
title:  "Spring Boot"
subtitle:   "JavaSpring 공부"
categories: JavaSpring
tags: Spring boot
comments: true
header-img: img/spring/springboot.PNG
---

## 개요
> JavaSpring을 기본기부터 공부한 내용을 담은 글입니다.

- 목차
	- [Spring boot 시작하기에 앞서](#) 
	- [Spring boot란](#) 


## Spring boot 공부하기에 앞서...
---
- Apache & Tomcat
apache는 웹 서버 프로그램으로 appache http server를 의미한다.  
먼저 웹 서버는 HTTP 서버를 의미하며 URL(웹주소) 및 HTTP(프로토콜 주소)를 이해하는 소프트웨어이다.  
HTTP 서버는 저장하는 웹 사이트의 도메인 이름을 통해 액세스 할 수 있으며 이러한 호스팅 된 웹 사이트의 콘텐츠를 최종 사용자의 장치로 전달한다.  
아파치서버란 클라이언트에서 요청하는 HTTP요청을 처리하는 웹서버를 의미한다.  

 - 톰켓 WAS(web application server)  
jsp와 servlet을 구동하기 위한 서블릿 컨테이너 역할을 수행한다.  
DB연결, 다른 응용프로그램과  상호작용 등 동적 기능 사용가능하다.  

 - 컨테이너  
동적인 데이터들을 가공하여 정적인 파일로 만들어주는 모듈

 - 서블릿  
클라이언트의 요청을 받고 처리하여 결과를 클라이언트에게 제공하는 자바 인터페이스  
![apache](/assets/img/spring/apache.PNG)  



이제 spring boot를 시작해 보겠다.


## Spring boot 란
---
 - Java spring을 공부하기 전에 먼저 Spring boot를 공부해 보기로 하였다. 우선 spring boot가 뭔가?  
1. 복잡한 설정없이 쉽고 빠르게 만들어주는 라이브러리입니다.  
2. 자주 사용되는 기본설정을 알아서 해줍니다.   
3. pom.xml에 스프링부트 버젼을 입력하면 모든 라이브러리 버전을 알아서 다운해줍니다.   
4. @EnableAutoConfiguration 어노테이션을 선언해서 스프링에서 자주 사용 했던 설정들을 알아서 등록해줍니다.   
5. Tomcat을 내장하고 있어 @EnableAutoConfiguration 어노테이션이 선언 되어있는 클래스의 main()을 실행함으로써 서버를 구동시킬 수 있습니다.  
이렇게 정의할 수 있다.  


다음 posting에서는 Spring boot & JPA 활용에 대해 다뤄보겠다.
