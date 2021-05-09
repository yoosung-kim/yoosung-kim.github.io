---
layout: post
title:  "[Face Detection]]"
subtitle:   "Digital Twin Classroom"
categories: graduationproject
tags: graduationproject
comments: true
header-img: img/post_img/spatial.jpg
---

## 개요
> 졸업 프로젝트 주제로 Digital Twin Classroom을 구현하는 과정을 나타낸 포스트 입니다.

- 목차
	- [Face Detection 을 위한 mtcnn & VGGFace2](#) 
	- [Speaker 검출을 위한 mouth detection](#)
	- [Web Page User Interface 구축](#누가-읽어야-하는가)
  


## Face Detection 을 위한 mtcnn & VGGFace2
---
2017년 여름부터 2018년 1월까지 비트코인의 열풍은 그 어느 때 보다도 뜨거웠다. 연령이 젊은 사람들은 대부분 소액이라도 투자를 해봤을 것이고 노년층도 예외는 아니었다. 투기의 광풍은 블록체인의 진가를 바래게 만들었지만 다른 한편으로는 블록체인의 인지도 대중화에 기여를 했다고 생각한다. 비트코인이 블록체인 기술 및 시장에 끼치는 양면은 이 책에도 언급하고 있듯이 퍼블릭 블록체인(무허가형 원장)과 프라이빗 블록체인(허가형 원장)의 대립으로 나타났고 과연 관련 업계, 기술 및 비지니스 진영 그리고 대중들은 어느 진영을 손을 들어주었는지 궁금했다.

* __퍼블릭 블록체인(Public Blockchain)__
  - 비트코인의 창시자 나가모토 사토시의 개발 철학이 핵심. 리먼브라더스 부도를 수습하고자 정부는 양적완화 정책을 펼쳤고 그 피해는 고스란히 서민이 떠안게 되어 자본주의 경제체제는 결코 민주주의가 아님을 천명하였다. 모두에게 공정한 경제 체제를 유지하고자 비트코인을 창시한 것으로 알려져있으며 현재 우리의 불공평한 자본주의 시장을 해결하는데 가상 이상적인 제도라고 주장한다. 
  - 퍼블릭블록체인의 체계를 유지하기 위해 POW(작업증명) 방식으로 채굴을 통한 경제적 보상이 이루어지며 이는 금본위제 당시의 공정성에 착안한다.
  
