---
layout: single
title: "JPA 개념 정리"
categories:
-Java
---

## JPA

![캡처](C:\Users\jojja\Desktop\코딩공부\프로젝트 필기\캡처.JPG)

출처: 유튜브 메타코딩 

[메타코딩(링크)]: https://www.youtube.com/channel/UCVrhnbfe78ODeQglXtT1Elw

하나씩 까보도록 하자.

&nbsp;

1. JPA는 Java Persistence API 이다.

   ![JPA](C:\Users\jojja\Desktop\코딩공부\프로젝트 필기\JPA.png)

   **Persistence**: 영구성, 영원함

   RAM에 데이터를 보관하고 있는데 컴퓨터가 꺼지면

   데이터는 완전히 날아간다. 이를 '휘발성' 이라 한다.

   &nbsp;

   그에 반해

   하드디스크의 DBMS에 보관되는 데이터는

   정전이 나거나 컴퓨터가 꺼져도 사라지지 않는다.

   이를 비휘발성, Persistence라고 부른다.

   &nbsp;

   **API**

   ![API](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/API.png)

   B가 어떤 데이터를 만들었다.

   A와 C는 그 데이터를 가져다 쓰려는 사람이다.

   **B의 권한이 큰 경우**, B는 자신의 데이터를 가져다 쓸 때

   '이제부터 나에게 연락을 할 때에는 전화하지 말고 직접 찾아와!'와 같은

   규칙을 정할 수 있다.

   &nbsp;

   A와 C는 그 규칙을 따라야만 한다.

   이 때 B의 규칙을 **인터페이스Interface**라고 한다.

   &nbsp;

   (반면 B가 만든 데이터에 대한 **A, B, C의 권한이 동일한 경우**,

   B의 규칙에 대해 A, C는 싫어!하고 할 수도 있다.

   &nbsp;

   이 때는 A, B, C 모두가 만족할 수 있는 규칙(이메일로 연락하기)을 만들어 사용하게 되는데, 이를 **프로토콜protocol**이라고 한다.)

   &nbsp;

   정리하면

   **JPA:**

   **-Java 자바로 쓴 프로그램을**

   **-Persistence 영구적으로 저장할 수 있게 하는**

   **-Application Programming Interface 인터페이스**

   &nbsp;

2. JPA는 ORM 기술이다.

   ![ORM1](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/ORM1.png)

3. JPA는 반복적인 CRUD 작업을 생략하게 해준다.

4. JPA는 영속성 컨텍스트를 가지고 있다.