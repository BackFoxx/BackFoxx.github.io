---
layout: single
title: Build()와 Builder()의 개념, 사용 이유, Lombok과의 콜라보
categories: Java
---

책 보면서 코딩하다 나온 낯선 코드의 출처를 파해치면서 알게된 개념을 정리했습니다.

> ''이게 뭐지'' 했던 문제의 코드

```java
ResponseDTO<String> response = ResponseDTO
    .<String>builder()
    .data(list)
    .build();
```

본 포스팅은 아래 블로그를 거의 베꼈습니다.

[[JAVA\] 빌더 패턴(Builder Pattern)에 대해 알아보자]: https://lemontia.tistory.com/483

&nbsp;

### 왜 쓰는가?

내가 어떤 클래스의 객체를 만듭니다.
클래스의 변수에 어떤 값을 세팅하면서 객체를 만들고자 할 때
우리는 생성자를 이용합니다.

```java
public class UserInfo {
   private String name; //이름
   private int age; //나이
   private String addr; //주소

   public UserInfo(String name, int age, String addr){
       this.name = name;
       this.age = age;
       this.addr = addr;
   }
    
   public String getUserInfo(){
       return String.format("name: %s, age: %d, addr: %s", name, age, addr);
    }
}
```

&nbsp;

객체를 사용할 때는 이렇게 합니다.

```java
UserInfo userInfo = new UserInfo("테스터", 25, "서울시 강남구");
System.out.println(userInfo.getUserInfo());

// 결과 => name: 테스터, age: 25, addr: 서울시 강남구
```

&nbsp;

근데 만약 주소는 넣지 않겠다. 하면
이렇게 할 수 있습니다.

```java
UserInfo userInfo2 = new UserInfo("테스터", 25, null);
System.out.println(userInfo2.getUserInfo());

// 결과 => name: 테스터, age: 25, addr: null
```

&nbsp;

다만 이렇게하면 null 을 입력하는 것은 모양새가 좋지 않으니 추가로 생성자를 만들어 주는 방법이 있겠네요.

&nbsp;

그런데 만약 요건이 자주 변경된다면 매번 생성자를 만드는 것도 일이 될 것입니다. 
위 경우만 보아도 모든 경우의 수를 고려하여 생성자를 만드려면 
생성자를 6개나 만들어야 합니다.

그래서 이런 상황을 피하기 위해 
좀 더 직관적인 객체를 만들 수 있게 돕는 것이 바로 **빌더 패턴** 입니다.

&nbsp;

## 어떻게 쓰는가?

빌더패턴이 적용된 클래스를 하나 더 만듭니다.

```java
public class UserInfoBuilder {
    private String name;
    private int age;
    private String addr;

    public UserInfoBuilder setName(String name){
        this.name = name;
        return this;
    }

    public UserInfoBuilder setAge(int age){
        this.age = age;
        return this;
    }

    public UserInfoBuilder setAddr(String addr){
        this.addr = addr;
        return this;
    }

    public UserInfo build(){
        return new UserInfo(name, age, addr);
    }
}
```

&nbsp;

객체를 사용할 때는 이렇게 합니다.

```java
UserInfoBuilder userInfoBuilder = new UserInfoBuilder();
UserInfo userInfo3 = userInfoBuilder
        .setName("테스터3")
        .setAddr("주소")
        .setAge(26)
        .build();

System.out.println(userInfo3.getUserInfo());

// 결과 => name: 테스터3, age: 26, addr: 주소
```

Build를 이용하여 객체를 생성할 때에는
**생성자에 들어갈 변수의 순서를 꼭 지키지 않아도 되고**,

만약 Name 또는 Age 등 하나를 빼먹어도
Name은 null, Age는 0 등
**기본값으로 세팅이 되어 객체가 정상적으로 생성**됩니다.
(생성자를 이용하는 처음의 코드에서 생성자를 빼먹으면 에러가 납니다.)

&nbsp;

## Lombok을 이용해 더욱 간단하게

Lombok을 사용하는 새로운 클래스를 만들어 보겠습니다.

```java
import lombok.Builder;
import lombok.Data;

@Data
@Builder
public class UserInfoLombok {
    private String name;
    private int age;
    private String addr;
}
```

&nbsp;

객체는 이렇게 생성합니다.

```java
UserInfoLombok userInfoLombok = UserInfoLombok.builder()
        .name("Lombok 적용")
        .addr("주소 테스트")
        .build();

System.out.println(userInfoLombok);

// 결과=> UserInfoLombok(name=Lombok 적용, age=0, addr=주소 테스트)
```

위 코드보다 훨씬 간단하게 객체를 생성할 수 있습니다.

&nbsp;