---
layout: post
title:  "[API]RESTful API"
subtitle:   "django-restframework"
categories: study
tags: django
---

그동안 django를 웹을 만드는데 사용했는데, 이번에 모바일 앱 서버를 구축할 일이 생겨서 찾아보던 중 Django의 restframework를 알게 되었고 공부를 시작해 볼까 한다.

---
# REST

우선 REST라는 용어가 나왔는데 잠깐만 알아보고 진행하도록 하겠습니다. 

REST 는 **RE**presentational **S**tate **T**ransfer 의 약자입니다. 이는 소프트웨어 아키텍쳐의 한  형식입니다.

REST API를 이용해서 무엇을 할 수 있느냐 보단, 어떤 일을 할 때 훨씬 쉽고 간단하게 일을 진행할 수 있게 만들어줍니다.

즉, 행위에 대한 표현이 **HTTP method**로 들어가게 됩니다.

예를 들면  
```
GET  url: /postname => 게시물 이름 표시

POST url: /postname => 게시물 이름 추가

PUT url: /postname => 게시물 이름 변경

DELETE url: /postname => 게시물 이름 삭제
```

다음과 같이 깔끔하게 정리가 가능해집니다.

또한 확장도 매우 쉬워지는데

```
GET  url: /postname/user => 사용자 이름 표시

POST url: /postname/user => 사용자 이름 추가

PUT url: /postname/user => 사용자 이름 변경

DELETE url: /postname/user => 사용자 이름 삭제
```

url만 건드렸지만 서버에서 하는 일이 달라졌습니다.

**REST API**의 장점은 다음과 같습니다.

**프로그래머가 쉽게 확장 수정이 가능하게 만들어준다.**
