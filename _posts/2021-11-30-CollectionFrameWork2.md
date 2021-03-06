---
layout: single
title: Java의 정석 - 컬렉션 프레임워크 2

categories: 
 - Java
---

어제에 이은 예제 분석하기이다.

## 예제 11_6(해결 못한 문제)

```java
import java.util.*;
    class Exercise11_6 {
        public static void main(String[] args) {
            Set set = new HashSet();
            int[][] board = new int[5][5];
            
            for(int i=0; set.size() < 25; i++) {
            set.add((int)(Math.random()*30)+1+"");
            }
            
            Iterator it = set.iterator();
            
            for(int i=0; i < board.length; i++) {
                
            for(int j=0; j < board[i].length; j++) {
            board[i][j] = Integer.parseInt((String)it.next());
            System.out.print((board[i][j] < 10 ? " " : " ")
            + board[i][j]);
            }
            System.out.println();
                
        }
    } // main
}
```

1~30의 숫자를 무작위 배열한

5X5의 빙고판을 생성하는 예제인데,

위 예제를 실행하면 숫자가 잘 섞이지 않는단다.

&nbsp;

이유를 설명하라 하는데 도저히 알 수가 없어 

해설지를 보면서 분석을 하니

&nbsp;

Hashset이 사용하는

데이터 정렬방식에서 기인한 문제였던 것이다!

&nbsp;

### Hash Table

Key값을 배열에 저장할 때,

hashcode() 메소드를 통해 key값을 임의의 정수값으로 바꿔버린다.

그리고 그 값을 배열의 인덱스로 사용한다.

그러니까 숫자를 랜덤으로 바꿔서

랜덤하게 배열에 때려박아도,

&nbsp;

그 숫자를 해시코드로 바꾼 후에

그 해시코드의 순서대로 저장하기 때문에

랜덤하게  넣는 것이 의미가 없다는 뜻으로 해석된다.

(그런데 실행할 때마다 약간씩 순서가 바뀌긴 하던데 그건 왜인지 모르겠다)

&nbsp;

그리고 이 문제의 해결 방법은..

```java
import java.util.*;
    class Exercise11_6_2
    {
    public static void main(String[] args)
    {
        Set set = new HashSet();
        int[][] board = new int[5][5];
        
        for(int i=0; set.size() < 25; i++) {
        set.add((int)(Math.random()*30)+1+"");
        }
        
        ArrayList list = new ArrayList(set);
        //해결0. HashSet의 set을 ArrayList list에 옮겨담는다.
        Collections.shuffle(list);
        //해결1. Collections 클래스의 메서드를 이용해 list 값을 뒤섞는다.
        Iterator it = list.iterator();
        
        for(int i=0; i < board.length; i++) {
            
        for(int j=0; j < board[i].length; j++) {
        board[i][j] = Integer.parseInt((String)it.next());
        System.out.print((board[i][j] < 10 ? " " : " ") + board[i][j]); //난 이게 뭔지 도통 모르겠다. 그냥 " "만 쓰면 되는 것 아닌가..??
        }
        System.out.println();
            
        }
    } // main
}


```

해결방법을 보고

뭐야 그럼 처음부터 Arraylist에 랜덤한 값을 담도록 하면 안되나 싶었는데,

List 인터페이스는 중복된 값을 허용하기 때문에

빙고판에 같은 숫자가 여러 개 찍힐 수 있다.

&nbsp;

HashSet은 해싱 알고리즘이 문제인 것이지

중복된 값을 저장하지 않는다는 특별한 기능이 꼭 필요하다.

&nbsp;

## 예제 11_5

```java
import java.util.*;

class SutdaCard {
	int num;
	boolean isKwang;
	
	SutdaCard() {
		this(1, true);
	}
	
	SutdaCard(int num, boolean isKwang) {
		this.num = num;
		this.isKwang = isKwang;
	}
	
	//Equals 오버라이딩
	public boolean equals(Object obj) {
        //매개변수가 반드시 Object여야 한다. 이유는 모르겠는데 SutdaCard 변수를 매개변수로 쓰면 중복 제거가 안된다.
		if(obj instanceof SutdaCard) {
			SutdaCard c = (SutdaCard)obj;
			return num==c.num && isKwang==c.isKwang;
		} else {
			return false;
		}
	}
	
	public String toString() {
		return num + (isKwang ? "K" : "");
	}
	
	//Hashcode 오버라이딩
	public int hashCode() {
		return toString().hashCode();
	}
}

public class class1_3 {

	public static void main(String[] args) {
		SutdaCard c1 = new SutdaCard(3, true);
		SutdaCard c2 = new SutdaCard(3, true);
		SutdaCard c3 = new SutdaCard(1, true);
		
		HashSet<SutdaCard> set = new HashSet<SutdaCard>();
		set.add(c1);
		set.add(c2);
		set.add(c3);
		
		System.out.println(set);
	}

}

```

HashSet은 중복된 값을 허용하지 않는다.

그런데 SutdaCard라는 클래스는 내가 만든거라

HashSet이 중복값을 알아낼 기준,

equals() 메소드와 hashCode() 메소드가 구현되어 있지가 않다.

그래서 차례대로

&nbsp;

equals() : num과 isKwang이 같은 값이면 true를 출력하도록 구현

hashCode(): sutdacard의 toString()이 num과 isKwang을 이용해 문자열을 만들어 반환하므로, toString의 결과물을 해시코드로 변환함으로써 구현





## 예제 11_4

> 제시된 BanNoAscending 클래스를 사용하여
>
> Student 인스턴스들이 반과 번호로 오름차순 정렬되게 하시오.
>
> (반이 같은 경우 번호를 비교한다)





### 내가 쓴 코드

```java
import java.util.*;

class Student {
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
    
}

class BanNoAscending implements Comparator<Student> {
	public int compare(Student o1, Student o2) {
		if(o1.ban<o2.ban) { return -1; }
		else if(o1.ban>o2.ban) { return 1; }
		else { 
			
			if(o1.no<o1.no) { return -1; }
			else if(o1.no>o1.no) { return 1;}
			else { return 0; }
			
		}
		
	}
}

public class classh {
    public static void main(String[] args) {
    ArrayList<Student> list = new ArrayList<Student>();
    list.add(new Student("김길동",2,1,100,100,100)); 
    list.add(new Student("남궁성",2,2,90,70,80)); 
    list.add(new Student("정자바",1,3,80,80,90)); 
    list.add(new Student("이자바",4,4,70,90,70)); 
    list.add(new Student("안자바",1,5,60,100,80)); 
        
    Collections.sort(list, new BanNoAscending());
    Iterator<Student> it = list.iterator();
        
    while(it.hasNext())
  	  System.out.println(it.next());
    }
}

```

바로 전(11_3) 예제에서는 Comparation을 쓰더니

이번에는 왜 Comparator를 사용하지? 라는 의문이 들어

구글을 열심히 뒤진 결과 깔끔한 결론을 낼 수 있었다.





1. Comparation: 클래스의 기본 정렬 방법을 정한 것. 쇼핑몰에서 아무 정렬 방식도 정하지 않았을 때 최신순이나 인기순으로 정렬되는 느낌이다.
2. Comparator: 기본 정렬 방법 외에 내가 직접 정렬 방법을 따로 만들고 싶을 때 사용하는 것. 최신순으로 기본 정렬된 쇼핑몰에서 정렬 방법 탭을 클릭해 리뷰 많은 순, 평점 높은 순 등으로 정렬하는 느낌



comparator를 구현할 때 우리가 꼭 구현해야 하는 객체는 Compare()메소드이다.

if문을 사용하여 데이터들을 오름차순으로 정렬되도록 깔쌈하게 만들었다.

```java
class BanNoAscending implements Comparator<Student> {
	public int compare(Student o1, Student o2) {
		if(o1.ban<o2.ban) { return -1; }
		else if(o1.ban>o2.ban) { return 1; }
		else { 
			
			if(o1.no<o1.no) { return -1; }
			else if(o1.no>o1.no) { return 1;}
			else { return 0; }
			
		}
		
	}
}

```





해설지는 좀 더 깔쌈하게 만들어

작으면 음수, 같으면 0, 크면 양수라는 간단한 메커니즘만 구현하면 되는 걸로 했다.

둘을 그냥 빼기로 한 것이다.

```java
class BanNoAscending implements Comparator {
    public int compare(Object o1, Object o2) {
        if(o1 instanceof Student && o2 instanceof Student) {
        Student s1 = (Student)o1;
        Student s2 = (Student)o2;
        int result = s1.ban - s2.ban;
            
        if(result==0) { //반이 같으면 번호를 비교한다
        return s1.no - s2.no;
        }
            
        return result;
        }
        return -1;
    }
}
```





이렇게 하여 개좆같은 컬렉션 프레임웍의 틀을 전체적으로 이해하는 여행을 마친다.

자바의 정석 책에 나오는 내용만 대강 이해할 수 있도록 쓴 블로그인데

블로그에 기록하기 위해 이것저것 찾아보고 지식을 연결하는 과정에서

컬렉션 프레임웍의 인터페이스 종류, 특징, 메커니즘까지

엄청나게 많은 것을 깊이 이해할 수 있었다.





앞으로 이해가 가지 않거나 반만 이해한 내용들은

깃허브에 정리해 기록하면서 깊이 이해하는 시간을 가질 계획이다.

만약 내 깃허브가 장기간 아주 활발한 활동을 하고 있다면

내가 그만큼 똥멍청이라는 뜻이다.
