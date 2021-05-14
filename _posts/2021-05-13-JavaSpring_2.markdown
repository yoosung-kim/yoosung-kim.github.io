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
	- [Spring boot 프로젝트 해보기](#) 


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
1. sql 중심적인 개발에서 객체 중심으로 개발하게 된다. 2. 생산적이다.  
즉, 마치 Java collection에 데이터를 넣었다가 빼는 것처럼 사용할 수 있게 만든 것이다. 따라서 CRUD가 간단하며 특히 수정이 쉽다. 
3. 유지보수가 편하다.  
기존에는 필드 변경시에 모든 sql을 수정해야 했다면 JPA를 이용하면 필드만 추가하면 된다. 
4. Object와 RDB간 패러다임 불일치 해결
객체 중심의 코딩으로 JPA를 이용하여 저장, 조회 등의 일을 간편하게 할 수 있다. 

등등 많은 일을 할 수 있는데 우선 내가 알아들을 수 있는 일만 작성을 해 보았다. 이후에 추가하도록 하겠다. 
