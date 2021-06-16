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
	- [도메인 설계](#) 
	- [엔티티 클래스 개발](#) 


## 도메인 설계
어떤 도메인을 어떤식으로 동작하게 할 것인가.  
쇼핑몰을 제작해 보기로 하였다. 
![domain](/assets/img/spring/domain.PNG)
위와 같은 테이블로 설계를 진행해 보려고 한다. 


엔티티를 분석해보면 다음과 같다. 
![entity](/assets/img/spring/entity.PNG)


- 연관 관계 매핑  
1대N 관계에서는 연관관계의 주인을 정해야 하는데 왜래키가 있는 (N쪽) 곳이 연관관계의 주인이다.

* 참고
외래 키가 있는 곳을 연관관계의 주인으로 정해야 한다.





## 엔티티 클래스 개발시 주의사항
엔티티를 매핑해 보았다.  
생성은 어렵지 않았고 테이블 간 매핑시에 다대일, 일대다의 관계는 다음과 같이 정의해 주어야 한다.   
![oneToMany](/assets/img/spring/oneToMany.PNG)

이 경우 두 곳에서 모두 접근이 가능하면 안되므로 외래 키가 있는 곳을 주인으로 정해야 한다.  


* getter, setter
getter의 경우 데이터를 조회할 일이 너무 많으므로 열어두는 것이 편하다.  
하지만 setter의 경우 막 열어두면 값을 변경하기 때문에 변경지점이 명확하지 않을 수 있다.  


또한 ORDERS 테이블을 작성시에 주의사항은 order로 만들게 되면 이는 order by의 약어로 혼동되는 경우가 있으므로 ORDERS로 생성해야 한다.  


테이블의 attribute 접근시에 가급적 Getter은 열고 Setter은 닫아두어야 한다.  Setter은 데이터를 변형시킬수 있기 때문이다.   또한 유지보수가 어렵다.  


- @ManyToMany 보다는 ManyToOne, OneToMany를 사용할 것.  
컬럼 추가가 어렵고 세밀한 query를 실행하기 어렵다.  


- 모든 연관관계는 즉시로딩(eager)이 아닌 지연로딩(lazy)으로 설정하여야 한다.  즉시로딩으로 설정할 경우 연관된 모든 sql이 실행될 수 있으므로 예측이 어렵다.  만약 연관된 엔티티를 조회하고자 한다면 fetch join 또는 엔티티 그래프 기능을 사용해야 한다.  
X to one 매핑은 기본으로 EAGER이다.  따라서 일일이 lazy로 바꿔주어야 한다.  


- 컬렉션은 필드에서 바로 초기화를 해 주어야 한다.  
엔티티를 계속 유지하려 할 때 hibernate가 컬렉션을 감싸서 내장 컬렉션으로 변경하게 되므로 컬렉션을 잘못 생성하면 hibernate 내부적으로 문제가 생길 수 있다.  


- hibernate 구현시에 엔티티 필드명을 그대로 table column명으로 사용하는 것이 아닌 underscore을 사용하는 등의 과정으로 바꿔주어야 한다.  


