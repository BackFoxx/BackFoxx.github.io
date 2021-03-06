---
latout: single
title: Java의 정석 - 컬렉션 프레임워크

categories: 
 - Java
---

챕터가 56개나 되는데 무슨 말인지 도통 알 수가 없어

그냥 건너뛰면 안될까 했는데

객체 다음으로 가장 중요한 챕터란다. 

연습문제에서 어느 하나 손 대지 못하여

연습문제 해설을 따라 코드를 따라 쓰면서

눈으로 흘겨본 개념들을 다시 복기하는 방식으로 공부한다.

&nbsp;
---
&nbsp;
&nbsp;

컬렉션 프레임웍이란

다수의 데이터(컬렉션)을 다루고 표현하는 표준화된 프로그래밍 방식(프레임워크)을 의미한다.

학교의 반, 번호, 성적 등이 나열된 다수의 데이터가 있을 때

엑셀처럼 내가 원하는 방식으로 정렬하고

원하는 필터에 맞추어 데이터들을 골라내거나 추가, 삭제하는 데에 사용되는 듯하다.

&nbsp;

개발자들은 다수의 데이터의 집합에는 크게 3가지가 있다 하여

데이터를 다루는 방식을 3가지로 분할했는데

&nbsp;



## 예제 11_1
&nbsp;
> 다음 코드의 실행결과를 적으시오.
&nbsp;
```java
import java.util.*;
class Exercise11_1 {
    public static void main(String[] args) {
        ArrayList list = new ArrayList();
        //0. 중복을 허용하고 저장순서를 유지하는 Arraylist
        list.add(3);
        list.add(6);
        list.add(2);
        list.add(2);
        list.add(2);
        list.add(7);
        
        HashSet set = new HashSet(list); 
        //1. Arraylist→HashSet, HashSet은 중복을 허용하지 않기 때문에 중복되는 요소들이 사라진다. 3,6,2,7(저장순서 또한 정해지지 않아 순서도 뒤죽박죽이 될 수 있다)
        TreeSet tset = new TreeSet(set);
        //2. HashSet → TreeSet, TreeSet은 요소를 정렬해서 저장하는데, 따로 지정하지 않으면 그냥 오름차순으로 정렬한다. 2,3,6,7
        Stack stack = new Stack(); 
        stack.addAll(tset);
        while(!stack.empty())
       	 System.out.println(stack.pop());
        //3, Stack은 처음 넣은 것이 마지막에 나오는 구조다. 그릇을 설거지하는 것으로 흔히 비유가 되는데, 납작한 그릇을 여러개 쌓아놓고 설거지할 때 제일 위 그릇부터 씻지 맨 아래부터 꺼내는 미친 사람은 없지 않은가!(있다면 미안하다)
    }
}
&nbsp;
```
&nbsp;
여담으로 이클립스에 위 코드를 작성하면

코드에 노란 밑줄이 쳐지면서 코드 전체가 노래진다.
&nbsp;
```
The method add(Object) belongs to the raw type ArrayList. References to generic type ArrayList<E> should be parameterized
↑ 이클립스의 노란 줄 아래에 표시되는 경고문구
```
&nbsp;


이게 무슨 일이고 하며 위 경고문을 검색하면

내가 쓴 코드가 Raw type이라고 한다.

인터페이스를 선언할 때 변수를 구성할 매개변수의 타입을 꼭 표기해야 하는데

<>를 이용하여 표기한 인터페이스를 제너릭 인터페이스,

표기하지 않은 인터페이스를 Raw type이라고 부른다 한다.
&nbsp;
```java
ArrayList<String> list = new ArrayList<String>();
```
&nbsp;
이렇게 작성하면 list 내에는 String만 들어갈 수 있으므로 안정성이 높은데 비해

Raw type은 돼지저금통에 동전 넣다가 비타민 c도 넣었다 안경도 넣었다 하면서

안정성이 낮아지기에 이클립스에서는 아예 오류가 나도록 막아두었단다.

&nbsp;

아무튼 위 예제를 통해

Set의 종류와 특징을 파악할 수 있는데

### Set 인터페이스의 메소드에는
&nbsp;
1. HashSet

   객체들을 순서없이 저장하고 중복을 허용하지 않는다.

   hashcode() 메소드를 통해 객체들의 고유한 정수값을 얻고

   새로운 객체가 들어왔을 때 정수값이 겹치면

   저장하지 않는 방식으로 중복요소를 제거한다.

   &nbsp;

   2. LinkedHashSet

      HashSet과 동일한 속성을 가지지만

      이름값대로 객체들을 입력한 순서대로 저장하고 관리하고 있다.

      &nbsp;

   3. TreeSet

      HashSet과 동일한 속성을 가지지만

      입력한 데이터들을 기본적으로 오름차순으로 정렬하여 관리하고 있다.

   &nbsp;

## 예제 11_2

> 다음 중 ArrayList에서 제일 비용이 많이 드는 작업은?
>
> 단, 작업도중에 ArrayList의 크기 변경이 발생하지 않는다고 가정한다
&nbsp;
1. 첫 번째 요소 삭제 

2. 마지막 요소 삭제 
3. 마지막에 새로운 요소 추가 
4. 중간에 새로운 요소 추가
&nbsp;
정답은 1이다.

그 원리를 알기 위해 List 인터페이스의 종류와 특징을 정리하였다.
&nbsp;
List라는 개념을 처음 보았을 때 제일 먼저 든 생각은

이게 배열과 다른 게 뭐지? 였다.

우연히 본 블로그에서 두 개념의 차이점을 아주 잘 설명해놓아

쪼금 베꼈다.
&nbsp;
[공통점]

1. 동일한 특성의 데이터들을 묶는다.
2. 반복문 내의 변수를 이용하여 하나의 묶음 데이터들을 모두 접근할 수 있다.
&nbsp;
[차이점-배열]

1. 처음 선언한 배열의 길이를 변경할 수 없다.(이를 정적 할당이라고 한다.)
2. 메모리에 연속적으로 나열되어 할당된다. 레고블럭을 나란히 조립한 느낌
3. index에 위치한 하나의 대이터를 삭제하면 그 index는 빈 공간으로 남는다.
&nbsp;
[차이점-리스트]

	1. 리스트의 길이가 가변적이다.(이를 동적 할당이라고 한다.)
	1. 각 데이터들이 주소로 연결되어 있다. 데이터들이 기차칸처럼 연결되어 있어서 중간에 기차칸을 하나 더 넣고자 하면 기차칸들 사이에 끼운 후 연결한 하면 되는 느낌 
	1. 데이터 사이의 빈 공간을 자동으로 메운다.
&nbsp;
### List 인터페이스의 메소드에는
&nbsp;
1. ArrayList

   레고 형식의 데이터 관리 방법을 가진다는 점에서 배열과 매우 흡사하다.

   단 배열은 크기가 고정되어 있고, Arraylist는 크기가 가변적이라

   배열을 추가, 삭제할 수 있는 메소드가 있다.
&nbsp;
1. LinkedList

​	  데이터의 주소끼리 연결하는 기차칸 형식의 데이터 관리 방법을 가진다.
&nbsp;
핵심적인 내용은 이게 끝인데

그래서 뭘 쓰라는거야! 하는 의문이 들었다.

두 인터페이스의 차이점을 잘 정리한 블로그가 있어 좀 베꼈다.
&nbsp;
| /           | ArrayList                                                    | LinkedList                                                   |
| ----------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 순차적 추가 | 원소의 이동 없이 추가만 하면 되기 때문에 빠르다              | 어떤 일을 하든  시작또는 끝으로부터 수정하고자 하는 곳을 탐색해 나아가는 구조로 다소 시간이 걸리지만, 양방향에서 시작하는 구조이므로 큰 차이가 나지는 않는다 |
| 중간에 추가 | 중간에 빈 공간을 만든 후, 원소들을 한칸씩 위로 미뤄야 한다. 매우 비효율적 | 기차칸을 밀어넣듯 주소만 연결해주면 되어 매우 효율적         |
| 중간에 삭제 | 삭제된 데이터의 빈 공간을 채우기 위해 나머지 데이터들이 한칸씩 모두 앞으로 이동한다. 매우 비효율적 | 마찬가지의 과정, 매우 효율적                                 |
| 순차적 삭제 | 원소간의 이동이 필요없어 빠르다                              | 양방향에서 시작하여 수정 지점을 찾기 때문에 순차적 삭제의 경우 큰 차이는 없다 |
| 결론        | 데이터의 수정이 잦지 않고 인덱스를 읽어낼 일이 많은 경우 추천 | 데이터의 수정이 잦고 인덱스를 읽어낼 일이 적은 경우 추천     |


&nbsp;
## 예제 11_3
&nbsp;
다음에 제시된 Student클래스가 Comparable인터페이스를 구현하도록 변경해서   

이름(name) 이 기본 정렬기준이 되도록 하시오.
&nbsp;
```java
import java.util.*;

class Student implements Comparable {
    //0. Comparable 인터페이스를 구현한다.
    /* 부모 객체는 선언만 한 추상 클래스.
    자식에서 오버라이딩하여 클래스를 완성하는 경우
    implements를 사용한다.
    */
    String name;
    int ban;
    int no;
    int kor, eng, math;
    
    Student(String name, int ban, int no, int kor, int eng, int math) {
        this.name = name;
        this.ban = ban;
        this.no = no;
        this.kor = kor;
        this.eng = eng;
        this.math = math;
    }
    
    int getTotal() {
   		 return kor+eng+math;
    }
    
    float getAverage() {
   		 return (int)((getTotal()/ 3f)*10+0.5)/10f;
    }
    
    public String toString() {
        return name +","+ban +","+no +","+kor +","+eng +","+math
        +","+getTotal() +","+getAverage();
    }
    
    public int compareTo(Object o) {
        //1.CompareTo()를 오버라이딩
        if(o instanceof Student) {
        Student tmp = (Student)o;
        return name.compareTo(tmp.name); 
        } else {
        return -1;
        }
        //
    }
}

class Exercise11_3 {
    public static void main(String[] args) {
    ArrayList list = new ArrayList();
    list.add(new Student(" ",1,1,100,100,100)); 홍길동
    list.add(new Student(" ",1,2,90,70,80)); 남궁성
    list.add(new Student(" ",1,3,80,80,90)); 김자바
    list.add(new Student(" ",1,4,70,90,70)); 이자바
    list.add(new Student(" ",1,5,60,100,80)); 안자바
        
    Collections.sort(list);
    Iterator it = list.iterator();
        
    while(it.hasNext())
  	  System.out.println(it.next());
    }
}

```
&nbsp;
```
출력 결과:
김자바,1,3,80,80,90,250,83.3
남궁성,1,2,90,70,80,240,80.0
안자바,1,5,60,100,80,240,80.0
이자바,1,4,70,90,70,230,76.7
홍길동,1,1,100,100,100,300,100.0
```
&nbsp;
진짜 1도 모르겠어서 그냥 답지를 가져왔다.

정석 책에 나와있는 Comparable과 Compare메소드도 도저히 이해가 안가(내 탓이다. 책은 아주 친절히 나와있다.)서 블로그를 찾아 정리하였다.

&nbsp;

출처: 

[Comparable 설명]: http://tcpschool.com/java/java_collectionFramework_comparable


&nbsp;
Comparable 인터페이스는

객체를 정렬하는 데 사용되는 메소드인 compareTo()를 정의하고 있다.

자바에서 Boolean을 제외한 래퍼 클래스와 String, time, Date 등의 클래스는

comparable 인터페이스를 가지고 있어 고유 기준에 따라 정렬이 가능하다.
&nbsp;


그런데 Student같이 내가 직접 만든 클래스는

Comparable인터페이스 CompareTo 메서드를 내가 직접 만들어

구현해 놓아야 한다.

인터페이스를 구현한 후

Collections.sort(List list)를 소환하면

CompareTo를 호출하면서 정렬 기준을 제공하는 것이다!
&nbsp;


```java
    public int compareTo(Object o) {
        if(o instanceof Student) {
        Student tmp = (Student)o;
        return name.compareTo(tmp.name); 
        } else {
        return -1;
        }
```
&nbsp;
답지대로 따라하다 이상한 점을 발견했는데,

매개변수 o를 받아 o가 Student이거나 Student의 조상이면 비교가 시작되게끔 한 것은 좋은데, raw type의 인터페이스를 제너릭 인터페이스로 수정하는 과정에서

< Object >를 쓰면 계속 무한정 오류가 난다.

오류를 피하려면 <>안에 들어갈 매개변수를 Student로 하고

CompareTo의 매개변수를 "Student o"로 설정해야 한다.
&nbsp;
```java
    public int compareTo(Student o) {
        if(o instanceof Student) {
        Student tmp = (Student)o;
        return name.compareTo(tmp.name); 
            //name.compareTo는 String클래스에 있는 메소드이다.!!!!
        } else {
        return -1;
        }
```
&nbsp;
이렇게 하면 if문의 의미가 없으므로

코드가 줄어 이렇게 된다.
&nbsp;
```java
    public int compareTo(Student o) {
	 return name.compareTo(o.name); 
        //name.compareTo는 String클래스에 있는 메소드이다.!!!!
```
&nbsp;
줄어든 코드도 잘 작동한다.

list 리스트에 Student가 아닌 애가 들어가면 오류가 날텐데 어떡하지? 싶었는데

생각해보니 < Student > 를 붙여 ArrayList에 Student 외에는 들어가지 못하도록 해두었던 것이다.!!!
