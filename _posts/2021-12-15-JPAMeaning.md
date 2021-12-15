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

   **모델링**: 건물 설계도를 실제 건물로 지어 올리는 것을 모델링이라 하듯

   추상적인 것을 실존하는 것으로 바꾸는 것을 모델링이라 한다.

   &nbsp;

   데이터가 담긴 **Table**이 있고 **Java** 가 있을 때

   Java에서 Table에 데이터를 요청(INSERT, DELETE, UPD9ATE)할 수 있고

   Table에서 Java에 데이터를 요청(SELECT)할 수 있는데,

   **Java와 Table은 서로의 언어를 이해하지 못한다.**

   &nbsp;

   그래서 **둘 사이에 Class을 넣어**

   **서로가 이해할 수 있는 언어로 모델링(변환)하는 작업을 거친다.**

   ![ORM2](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/ORM2.png)

   모델링 Class와 Table 사이에는 순서가 있는데

   (1)Table을 먼저 만든 후 (2)Class를 만드는 방법이 있고,

   &nbsp;

   **(1)Class를 JPA의 형태로 만들면**

   **(2)프로그램 실행시 Table이 자동으로 생성되게 하는 방법이 있는데**

   **이 방식을 ORM이라고 한다.**

   &nbsp;

3. JPA는 반복적인 CRUD 작업을 생략하게 해준다.

   ![ORM3](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/ORM3.png)

   **CRUD**: Create, Read, Update, Delete, 

   자바와 DB간에서 가장 많이 사용되는 작업이다.

   &nbsp;

   자바에서 데이터를 가져올 때

   (1) 자바에서 DB로 커넥션을 요청하면

   (2) DB에서 세션을 오픈한다.

   (3) 이루 자바에서 쿼리를 전송하면

   (4) DB에서 원하는 데이터를 반환한다.

   (5) 그럼 자바에서 자바의 언어로 읽을 수 있도록 데이터를 가공한다.

   (6) 이후 DB에서 세션을 끊고

   (7) 자바에서 커넥션을 끊는데

   이 일련의 과정은 모두 단순한 반복작업이다.

   &nbsp;

   위 과정을 데이터를 불러올 때마다 작성해야 한다면 매우 고통스러운데,

   JPA를 사용하면

   위 일련의 CRUD 과정을 함수 하나로 축약할 수 있다.

   &nbsp;

   정리하면 

   ORM을 사용하면

   **(1) 프로그램을 실행하면 자동으로 DB Table을 만들어 주고**

   **(2) DB와 상호작용하는 데에 쓰이는 일련의 과정을 함수 하나로 대신해주는**

   매우 중요한 귀찮음 해결사이다.

   &nbsp;

4. JPA는 영속성 컨텍스트를 가지고 있다.