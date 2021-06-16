---
layout: post
title:  "[Spring Boot & JPA]"
subtitle:   "JavaSpring 공부"
categories: JavaSpring
tags: Spring boot
comments: true
header-img: img/spring/springboot.PNG
---

## 개요
> Spring Boot & JPA를 공부한 내용을 담은 글입니다.

- 목차
	- [JPA 소개](#) 
	- [Spring boot 시작하기](#) 


## JPA 소개
---
- ORM이란
object relational mapping 의 약자로 객체는 객체대로, 관계형 DB는 관계형 DB대로 설계하는 것이다.  
ORM 프레임워크가 중간에 매핑을 해준다.  


- JPA란
현재 자바 진영의 ORM기술 표준으로 인터페이스 모음이다.  
JPA 인터페이스를 구현한 대표적인 오픈소스가 Hibernate라 할 수 있다.  
동작 과정으로는 애플리케이션과 JDBC 사이에서 동작하며 개발자가 JPA를 사용한다면 JPA 내부에서 JDBC API를 사용하여 SQL을 호출하여 DB와 통신하게 된다.  
즉, 개발자가 직접 JDBC API를 사용하는 것이 아니다.
![jpa](/assets/img/spring/jpa.PNG)  



- 왜 JPA를 사용해야 하나   
1. sql 중심적인 개발에서 객체 중심으로 개발하게 된다.  
2. 생산적이다.    
즉, 마치 Java collection에 데이터를 넣었다가 빼는 것처럼 사용할 수 있게 만든 것이다. 따라서 CRUD가 간단하며 특히 수정이 쉽다. 
3. 유지보수가 편하다.  
기존에는 필드 변경시에 모든 sql을 수정해야 했다면 JPA를 이용하면 필드만 추가하면 된다. 
4. Object와 RDB간 패러다임 불일치 해결
객체 중심의 코딩으로 JPA를 이용하여 저장, 조회 등의 일을 간편하게 할 수 있다. 

등등 많은 일을 할 수 있는데 우선 내가 알아들을 수 있는 일만 작성을 해 보았다. 이후에 추가하도록 하겠다. 



## Spring Boot 시작하기
---
- 내장(Embeded) Tomcat  
기존 웹 개발시에는 WAS를 서버에 설치를 해놓고(tomcat 등을 이용) 자바 코드를 밀어넣는 식이었다면 Boot에는 source에서 내장 WAS를 들고있다.   따라서 실행만 하면 웹 서버가 뜬다.   전에 DB수업때 WAS사용하기위해 애를 먹은걸 생각하면 참으로 신기하다!!  

---

-  로깅(Logging)  
애플리케이션 사용중 문제가 발생하면 먼저 살펴보는 것이 로그메세지이다. 로그는 디버깅 할 때도 필요하지만 실행중인 애플리케이션 성능분석 등의 용도로도 사용가능하다. 스프링부트에서는 SLF4J를 이용하여 로그를 관리하게 된다.   

---

- 스프링 동작 과정  
간단한 예제를 통해 동작과정을 알아보았다.   
우선 웹 브라우저에서 요청이 들어오면 내장된 톰켓 서버를 통해 스프링 컨테이너 내에 controller에서 처리를 하게 된다.   이때 컨트롤러에서 리턴으로 문자를 반환하면 ( ex. return "hello"; ) templates/hello.html을 찾아서 thymeleaf엔진이 처리하게 된다.  
![thymeleaf](/assets/img/spring/thymeleaf.PNG) 

---

- devtools 사용하기  
build.Gradle에서 devtools dependancy를 추가하게 되면 html에 변경사항이 있을 경우 그 파일만 재컴파일 해주면 변경사항이 반영된다. 

---

- 정적 컨텐츠 사용해보기  
정적 웹 컨텐츠의 돌아가는 과정을 살펴보기로 했다.  
우선 웹 브라우저로 요청이 오면 내장 톰켓 서버에서 우선적으로 스프링 컨테이너 내의 컨트롤러가 있는지 확인한 후에 없으면 static 폴더 내 html을 찾아 단순히 반환해준다.
![static](/assets/img/spring/static.PNG) 

---

- MVC와 template엔진  
controller : logic or 내부 처리 (ex. 서버, db)
view : 화면을 그리는데 관련된 일만 처리
웹 브라우저로 요청이 들어오면 내장 톰켓을 거쳐서 컨트롤러 내 작동으로 return, model 등이 설정된다.   이후 화면에 띄워주기 위해 viewResolver가 작동하게 된다.
![mvc](/assets/img/spring/mvc.PNG) 

---

- @ResponseBody사용법  
요청이 스프링 컨테이너 내로 들어오면 컨트롤러를 거치게 되고 컨트롤러 내 Responsebody가 있으면 message converter에서 처리를 한다. 이때 Json converter와 Spring converter가 있는데 단순 문자를 return 하는 경우 spring converter가 문자를 출력하고 객체를 return 하는 경우 Json converter에서 Json 형태로 반환하게 된다.
![ResponseBody](/assets/img/spring/ResponseBody.PNG) 

---


- Test Case 생성하기  


test case는 클래스명에서 alt + enter 단축기를 이용하여 바로 기본적인 틀을 제공한다.    
test case 작성시에 given, when, then 이렇게 나눠서 작성하는 것이 도움이 된다.   


---


- 단축키 정리  


Getter & Setter 생성해주는 Generator : alt + insert  
Test case 틀 : alt + enter  
class 정의 : ctrl + alt + M  
static import로 뽑아내는 방법 : alt + enter  
복사해서 이름만 바꾸기 : shift f6  
변수 추출하기 : ctrl + alt + v   