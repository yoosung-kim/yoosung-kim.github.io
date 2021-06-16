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


## 스프링 빈과 의존관계
---
 - 스프링 빈 등록하기 두가지 방법


1. 컴포넌트 스캔과 자동 의존관계 설정   
스프링 컨테이너 내에 등록되어 있는 객체들을 autowired를 이용하여 관계를 맺어주는 것.   

-  자동 의존관계 설정  
@Autowired : 생성자에 선언이 되어 있으면 스프링이 연관된 객체를 컨테이너에서 찾아서 넣어준다.  이렇게 의존관계를 외부에서 넣어주는 것을 의존성 주입(DI)이라 한다.  즉, 컨트롤러와 서비스를 연결시켜주는 역할을 한다고 볼 수 있다. 

![bean](/assets/img/spring/bean.PNG) 

아래 그림에서와 같이 memberController 생성자에 autowired를 선언해주면 스프링 빈에 등록되어 있는 memberService 객체들을 주입해준다.  이후 memverService생성자에 autowired를 선언해주면 스프링 빈에 등록되어 있는 memberRepository객체들을 주입해준다.  이로써 세 개의 연결이 완성되었다. 


컨트롤러, 서비스, 리포지토리 관계 : 컨트롤러를 통해 외부 요청을 받고 서비스에서 비즈니스 로직을 만들고 리포지토리에서 데이터를 저장한다.   


2. 자바 코드로 직접 스프링 빈 등록하기  

![BeanCode](/assets/img/spring/BeanCode.PNG) 



## 클래스 의존 관계
- 멤버 서비스 등록
멤버 서비스, repository, memory repository는 아래 그림과 같은 구조로 되어 있다. 개발시에는 데이터 저장소만을 바꿔주는 식으로 구현을 쉽게 할 수 있다.
![interfaceMMR](/assets/img/spring/interfaceMMR.PNG) 


## 회원 웹 기능 등록
아래 이미지는 회원 등록 html form이다.  
submit 버튼을 누르게 되면 action의 url으로 post방식으로 넘어오게 된다.  
여기서 postMapping은 data를 form형태로 넣어서 전달/등록할 때에 사용이 되고 get은 조회할 때에 주로 사용이 된다.   
![formhtml](/assets/img/spring/formhtml.PNG) 


membercontroller에서 postmapping으로 members/new라는 url이 요청이 되면 member에 접근을 하여 등록할 수 있도록 만들어주면 된다.   
![postmapping](/assets/img/spring/postmapping.PNG) 


- 멤버 서비스 조회  
전체 멤버 서비스를 조회할 때에는 getMapping에서 member list를 model에 모두 add해준 다음에 mapping된 url html에서 thymeleaf를 이용하여 모든 member model을 조회해주면 된다.   


## JPA
- jpa는 기존의 반복코드를 알아서 실행해주는 JDBC template에 추가로 기본적인 sql query도 만들어서 실행을 해준다.    
또한 jpa사용시 sql과 데이터 중심의 설계에서 객체 중심 설계로 전환할 수 있다.    
따라서 개발 생산성을 크게 높일 수 있다.   

사용하다 보면 jpa, hibernate, jpa repository등의 개념이 나온다.  
이를 명확히 하고자 한다.    
우선 jpa는 java interface의 하나이다. 그리고 이를 구현하기 위한 구현체가 hibernate인 것이다.  


- java file 작성하기  
자바 파일에서 @Entity로 annotation을 해주게 되면 jpa가 관리하는 entity라는 뜻이다.  또한 @Id로 PK를 mapping해 주어야 한다. 이때 strategy로 identity라는 명령을 하면 db가 알아서 생성해주도록 하는 것이다.   
아래 그림처럼 annotation이 되어있는 java file에서 insert, select등을 구현할 수 있게 된다.  
![jpajava](/assets/img/spring/jpajava.PNG) 


이제 member repository에서 db동작을 구현하면 된다.  
jpa는 entity manager에 의해 모든 동작을 control하게 된다. 
생성자를 통해 객체를 만들어둔 상태에서 CRUD기능을 사용할 수 있다.  
이때, 조회나 삭제 등을 할 경우 key값으로 구현한 경우 객체에서 함수를 불러 간편하게 사용할 수 있다.  
![jpaEM](/assets/img/spring/jpaEM.PNG)   


하지만 key값이 아닌 경우 query문으로 구현을 해주어야 한다.  
![jpaEMquery](/assets/img/spring/jpaEMquery.PNG) 


주의사항으로 jpa를 사용할 때에 transaction이 있어야 데이터를 저장하거나 변경할 수 있다.   
이후 스프링 설정을 entity manager 객체를 memberRepository의 return값으로 주면 된다.   
![setEM](/assets/img/spring/setEM.PNG) 


## 스프링 데이터 JPA
- 스프링 부트와 JPA를 합쳐서 탄생한 새로운 기술이라 할 수 있다.  

우선 spring data JPA interface를 생성하고 인터페이스를 받고 있으면 자동으로 구현체를 만들어서 스프링 빈에 자동으로 등록한다.  
즉, spring data jpa가 jpa기술을 사용하는 것이라 할 수 있다.  
![bootJPA](/assets/img/spring/bootJPA.PNG) 

동작 과정을 더 자세히 살펴보면 우선 spring data jpa가 객체를 알아서 생성하여 스프링 빈에 올리게 되면 이는 JpaRepository 인터페이스를 참조하도록 되어 있고, JpaRepository는 대부분의 기능(CRUD, 단순 조회)이 이미 만들어져 있다.   

- 제공되는 기능들
![jpaRepositopy](/assets/img/spring/jpaRepositopy.PNG) 


하지만 통용되지 않는 객체 이름 등의 attribute등은 database마다 가지는 이름이 다르다.  따라서 이러한 경우 query를 직접 짜서 사용하거나 라이브러리 등을 이용하여 구현할 수 있다. 


# AOP란?
모든 메소드의 호출 시간을 측정하고자 할 경우에 사용  
기존의 경우 모든 logic의 시작과 끝에 시간 측정 함수를 추가하여 일일이 측정을 진행하였다.   
그러나 이를 별도의 공통 로직으로 만들기도 어렵고 수정해야할 경우 역시 엄청난 시간이 투자되어야 하며 이는 핵심 관심사항도 아니다.   
따라서 AOP(aspect oriented programming)을 사용하여야 한다.  
AOP란 공통 관심사항과 핵심 관심사항을 분리하는 것을 말하며 예를들어 시간 측정 로직을 생성하여 원하는 곳을 지정하기만 하면 그 곳의 시간측정이 되는 것이다.   


# AOP 사용하기
우선 Aspect를 annotation 한 후 logic을 완성한다.
![AOP_logic](/assets/img/spring/AOP_logic.PNG) 
위와 같이 로직을 완성한 후에 스프링 빈에 등록해주면 된다.  또한 적용대상을 한정하여 원하는 대상에만 적용할 수도 있다.  


# AOP 동작과정
스프링 컨테이너에 AOP가 적용이 되면 proxy기술이 사용이 된다.  
이는 코드를 복제하여 조작하는 기능이라 생각하면 된다.  
따라서 controller, service, repository 각각 AOP가 적용이 된다면 각각의 proxy가 실행이 되고 그 다음 proxy내에 joinPoint등의 과정이 진행이 되는 것이다.  
![AOP_proxy](/assets/img/spring/AOP_proxy.PNG) 