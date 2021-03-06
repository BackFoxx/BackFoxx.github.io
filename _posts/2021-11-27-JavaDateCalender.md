---
layout: single
title: Java의 정석 - 날짜와 시간 개념, 예제

categories: 
 - Java
---

&nbsp;

시간과 관련된 클래스는

Date 클래스와 Calender 클래스가 있다.

Date클래스 자체는 사실상 죽은 클래스인데, SimpleDateFormat 클래스에서 Date클래스를 요구하기 때문에

Calender 클래스와 SimpleDateFormat 클래스 사이를 연결하는 도킹용으로 사용되고 있다.

&nbsp;

각각의 역할을 정리하면

&nbsp;

Calender: 클래스의 인스턴스메소드를 통헤

​				날짜를 원하는 조건에 맞게 저장, 수정하는 역할

↑↓

Date: 도킹용

↑↓

SimpleDateFormat:  내가 원하는 메시지 형식에 맞게

​								날짜를 표현할 수 있도록 만든 형식화 클래스 

&nbsp;

## 예제 10_1

> Calendar SimpleDateFormat 2020 클래스와 클래스를 이용해서 년의 매월 두 번째 일요일의 날짜를 출력하시오.

```
2020-01-12은 2번째 일요일입니다
2020-02-09은 2번째 일요일입니다
2020-03-08은 2번째 일요일입니다
2020-04-12은 2번째 일요일입니다
2020-05-10은 2번째 일요일입니다
2020-06-14은 2번째 일요일입니다
2020-07-12은 2번째 일요일입니다
2020-08-09은 2번째 일요일입니다
2020-09-13은 2번째 일요일입니다
2020-10-11은 2번째 일요일입니다
2020-11-08은 2번째 일요일입니다
2020-12-13은 2번째 일요일입니다 
```

&nbsp;

### 내가 쓴 코드

```java
import java.util.*;
import java.text.*;
public class class10_1 {

	public static void main(String[] args) {
			Calendar Day = Calendar.getInstance();
			SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd은 F번째 E요일입니다.");
        	//0. println으로 출력할 메시지의 형식을 정한다
		for(int i=0;i<12;i++) {
			Day.set(Calendar.YEAR, 2020);
            //1. 연도를 2020년으로 정한다
			Day.set(Calendar.MONTH, i);
            //2. 반복문을 이용해 Calender가 매 달로 세팅되도록 한다
			Day.set(Calendar.DAY_OF_WEEK, 1);
            //3. 일요일
			Day.set(Calendar.DAY_OF_WEEK_IN_MONTH, 2);
            //4. 매 달 두 번째 일요일
			Date d = new Date(Day.getTimeInMillis());
            //5.Calender형식의 Day를 Date 형식으로 형변환한다
			System.out.println(df.format(d));
            //6.df의 형식으로 d를 출력한다
		}
	}

}

```

&nbsp;

## 해설지 답안

```java
import java.util.*;
import java.text.*;
class Exercise10_1
{
	public static void main(String[] args) {
    Calendar cal = Calendar.getInstance();
    cal.set(2020, 0, 1); 
    //0. cal의 날짜를 달의 첫번 째 일로 설정한다
        for(int i=0; i < 12;i++) {
        int weekday = cal.get(Calendar.DAY_OF_WEEK);
        //1. cal에 설정된 날짜의 요일을 구한다.
        int secondSunday = (weekday==1) ? 8 : 16 - weekday;
        /*2. weekday(달의 첫 날의 요일)이 일요일(일요일: 1) 이면 
             2번째 일요일은 8일이고,
             일요일이 아니라면
             2번째 일요일은 16-weekday로 구할 수 있다. 
             구한 2번째 일요일 날을 secondSunday에 저장한다. */
        cal.set(Calendar.DAY_OF_MONTH, secondSunday);
        //3. cal = (2020, i, secondSunday)
        Date d = cal.getTime();
        //4. Calender 타입의 cal을 Date 타입으로 전환
        System.out.println(new SimpleDateFormat("yyyy-MM-dd F E 은 번째 요일입니다.").format(d));
        //5. Date 타입의 d를 SimpleDateFormat 형식에 맞추어 출력
        cal.add(Calendar.MONTH, 1);
        //6. 다음 달로 개월을 넘기고
        cal.set(Calendar.DAY_OF_MONTH,1);
        //7. 해당 달의 첫날로 일수를 설정한 후 반복
        }
    }
}
```

&nbsp;

##### 2번 째 일요일을 어떻게 16-weekday로 구할 수 있을까?

| 1일의 요일 | weekday | 2번째 일요일 | weekday+ 2번째 일요일 |
| :--------- | ------: | -----------: | --------------------: |
| 일         |       1 |          8일 |                     9 |
| 월         |       2 |         14일 |                    16 |
| 화         |       3 |         13일 |                    16 |
| 수         |       4 |         12일 |                    16 |
| 목         |       5 |         11일 |                    16 |
| 금         |       6 |         10일 |                    16 |
| 토         |       7 |          9일 |                    16 |

첫 날이 일요일임을 제외하면

weekday(요일을 정수로 나타낸 값) + 2번째 일요일 = 항상 16임을 알아낼 수 있다.

weekday을 이항하여

''항상 16 - weekday = 2번째 일요일''이라는 수식을 알아낼 수 있다.

그럼 일요일이 아니라 2번째 다른 요일을 알아내고자 한다면?

| 1일의 요일 | weekday | 2번째 일요일 | weekday+ 2번째 일요일 |
| :--------- | ------: | -----------: | --------------------: |
| 수         |       1 |          8일 |                     9 |
| 목         |       2 |         14일 |                    16 |
| 금         |       3 |         13일 |                    16 |
| 토         |       4 |         12일 |                    16 |
| 일         |       5 |         11일 |                    16 |
| 월         |       6 |         10일 |                    16 |
| 화         |       7 |          9일 |                    16 |

놀랍게도 1일의 요일 순서만 앞장겨질 뿐 수식이 똑같다!

&nbsp;

하지만 내 생각에는

Date 클래스에서 수식 대부분이 해결되는

내 코드가 보기에 더 깔끔한 코드인것 같다.

&nbsp;

---

&nbsp;

## 예제 10_2

> 화면으로부터 날짜를 “2017/05/11”의 형태로 입력받아서 무슨 요일인지 출력하는 프로그램을 작성하시오. 단 입력된 날짜의 형식이 잘못된 경우 메세지를 보여주고 다시 입력받아야 한다.

```
날짜를 yyyy/MM/dd의 형태로 입력해주세요 입력예: (2017/05/11)
>>2009-12-12
날짜를 yyyy/MM/dd의 형태로 입력해주세요 입력예: (2017/05/11)
>>2009/12/12
입력하신 날짜는 토요일입니다.
```

&nbsp;

### 내가 쓴 코드

```java
import java.util.*;
import java.text.*;
//0. 감이 도저히 잡히지 않아 오픈북으로 진행했다.

public class class10_2 {

	public static void main(String[] args) {
		String pattern = "yyyy/MM/dd";
		DateFormat df = new SimpleDateFormat(pattern);
        //1. 입력/출력에 사용될 형식을 pattern 에 따로 빼 저장했다
		Scanner s = new Scanner(System.in);
        //2. cmd에서 입력을 받도록 하는 코드. java.util();을 필요로 한다
		
		Date inDate = null;
		System.out.println("날짜를 "+pattern+"의 형태로 입력해주세요.(입력예: 2017/05/11)");
		System.out.print(">> ");
        //3. 사용자가 입력받을 Date 변수와 cmd에 입력하도록 문구를 작성한다
		
		while(s.hasNextLine()) {
            //4. 베껴쓸 땐 몰랐는데 s에 입력값이 있는지를 판별하여 boolean값을 출력한다
			try {
				inDate = df.parse(s.nextLine());
                //5. 사용자의 입력값을 inDate에 저장하는데,
				break;
			} catch(Exception e) {
				System.out.println("날짜를 "+pattern+"의 형태로 다시 입력해주세요.(입력예: 2017/05/11)");
				System.out.print(">> ");
                //이상한 값을 넣으면 예외를 캐치하여 다시 입력하도록 유도한다.
			}
		}
		
		SimpleDateFormat result = new SimpleDateFormat("입력하신 날짜는 E요일입니다.");
		System.out.println(result.format(inDate));
		//7. 사용자의 입력값을 result 형식에 맞게 변환하여 출력한다.
	
	}

}
```

&nbsp;

### 해설지 답안

```java
import java.util.*;
import java.text.*;

class Exercise10_2 {
    public static void main(String[] args) {
        String pattern = "yyyy/MM/dd";
        //0. 입력받을 형식을 저장한다.
        String pattern2 = "입력하신 날짜는 E요일입니다."
        //1. 최종 출력할 형식을 저장한다. 근데 이걸 굳이 지금?
        
        DateFormat df = new SimpleDateFormat(pattern);
        DateFormat df2 = new SimpleDateFormat(pattern2);
        //0.1과 동일
        
        Scanner s = new Scanner(System.in);
        Date inDate = null;
        //2. Scanner코드와 입력값을 저장할 코드를 선언한다.
        
        do {
            System.out.println("날짜를 " + pattern
            + " 의 형태로 입력해주세요.(입력예 :2017/05/11)");  
        try {
            System.out.print(">>");
            inDate = df.parse(s.nextLine()); 
            //3. 입력받은 날짜를 inDate에 저장한다.
            break; 
            //4. 위 코드가 정상적으로 수행되었다면 반복문을 빠져나가고,
            // 에러가 발생한다면 반복문의 처음으로 돌아간다.
        } catch(Exception e) {}
        } while(true);
        
        System.out.println(df2.format(inDate));
        //5. inDate를 df2의 형식으로 변환하여 출력한다.
    } // main
}
```

베껴썼기 때문에 큰 차이는 없다.

대신 나의 코드는 입력값을 받는 과정에서

에러가 났을 때의 대처가 포함되어 있다는 점이 차이점이다.

&nbsp;

## 예제 10_3

> 어떤 회사의 월급날이 매월 21일이다. 두 날짜 사이에 월급날이 몇 번있는지 계산해서 반환하는 메서드를 작성하고 테스트 하시오.

&nbsp;

### 내가 쓴 코드

```java
import java.util.*;
import java.text.*;
// 작동 순서대로 설명하였다. 책에는 작성 순서가 적혀 있어서 작동 순서를 고려해서 쓴 건 아니다.

public class class10_3 {
	
	static int paycheckCount(Calendar from, Calendar to) {
		if(from==null || to==null) { return 0; }
        //4_1. 입력값이 비어있으면 0을 반환한다
		if(from.getTimeInMillis()==to.getTimeInMillis() && from.get(Calendar.DATE) == 21 ) { return 1; }
        //4_2. 날짜가 같은데 그 날이 21일(월급날)이면 1을 반환한다
		int monDiff = ( to.get(Calendar.YEAR)*12+to.get(Calendar.MONTH) ) - ( from.get(Calendar.YEAR)*12+from.get(Calendar.MONTH) );
        //4_3. 두 날짜의 개월 수를 monDiff에 저장한다. 년도에 12를 곱해 월로 바꾼 후 월수끼리 계산하였다. 이 monDiff가 월급 받는 횟수이다.
		if(monDiff < 0) { return 0; } //4_4. to가 from보다 앞 날짜면 0을 반환한다.
		if( ( from.get(Calendar.DAY_OF_MONTH) <= 21 ) && ( 21 <= to.get(Calendar.DAY_OF_MONTH) ) ) {
			++monDiff;
       /*5_1. from이 21일보다 작거나 같고, to가 21일보다 크거나 같으면 1을 카운트에 추가한다.
       예를 들어 06.10과 8.29는 개월 수로 2달 차이이지만 월급날은 6.21,7.21,8.21로 총 3번이다. */
		} else if ( ( from.get(Calendar.DAY_OF_MONTH) > 21 ) && ( 21 > to.get(Calendar.DAY_OF_MONTH) ) ) { --monDiff; }
       /*5_2. from이 21일보다 크고, to가 21일보다 작으면 1을 카운트에서 뺀다.
       예를 들어 05.23과 8.1는 개월 수로 3달 차이이지만 월급날은 6.21 , 7.21로 총 2번이다. */
		
		return monDiff;
        //6. 월급 횟수를 반환한다.
	}
	
	static void printResult(Calendar from, Calendar to) {
		Date fromDate = from.getTime();
		Date toDate = to.getTime();
        //2. 매개변수를 저장한다
		
		SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
		System.out.print(sdf.format(fromDate) + " ~ " + sdf.format(toDate) + " : ");
        //3. fromDate로부터 toDate 사이의 월급날 수는? 이라는 문구를 출력한다
		System.out.println(paycheckCount(from,to));
	}
	
	public static void main(String[] args) {
		Calendar fromCal = Calendar.getInstance();
		Calendar toCal = Calendar.getInstance();
        //0. 비교할 두 날짜를 선언한다
		
		fromCal.set(2020, 0, 1);
		toCal.set(2020, 0, 1);
        //1. 두 날짜를 기재한다
		printResult(fromCal, toCal);
		
		fromCal.set(2020, 0, 21);
		toCal.set(2020, 0, 21);
		printResult(fromCal, toCal);
		
		fromCal.set(2020, 0, 1);
		toCal.set(2020, 2, 1);
		printResult(fromCal, toCal);
		
		fromCal.set(2020, 0, 1);
		toCal.set(2020, 2, 23);
		printResult(fromCal, toCal);
		
		fromCal.set(2020, 0, 23);
		toCal.set(2020, 2, 21);
		printResult(fromCal, toCal);
	
		fromCal.set(2021, 0, 22);
		toCal.set(2020, 2, 21);
		printResult(fromCal, toCal);
	}

}

```

&nbsp;

### 해설지 답안

```java
import java.util.*;
import java.text.*;

class Exercise10_3 {
    
    static int paycheckCount(Calendar from, Calendar to) {

    if(from==null || to==null) return 0;

    if(from.equals(to) && from.get(Calendar.DAY_OF_MONTH)==21) {
    return 1;
    }
        
    int fromYear = from.get(Calendar.YEAR);
    int fromMon = from.get(Calendar.MONTH);
    int fromDay = from.get(Calendar.DAY_OF_MONTH);
    int toYear = to.get(Calendar.YEAR);
    int toMon = to.get(Calendar.MONTH);
    int toDay = to.get(Calendar.DAY_OF_MONTH);
        

    int monDiff = (toYear * 12 + toMon) - (fromYear * 12 + fromMon);

    if(monDiff < 0) return 0;

    if(fromDay <= 21 && toDay >= 21)
    monDiff++;

    if(fromDay > 21 && toDay < 21)
    monDiff--;
        
    return monDiff;
    }
    
    static void printResult(Calendar from, Calendar to) {
        Date fromDate = from.getTime();
        Date toDate = to.getTime();
        
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
        
        System.out.print(sdf.format(fromDate)+" ~ "
        +sdf.format(toDate)+":");
        System.out.println(paycheckCount(from, to));
    }
    
    public static void main(String[] args) {
    Calendar fromCal = Calendar.getInstance();
        Calendar toCal = Calendar.getInstance();
    fromCal.set(2020,0,1);
    toCal.set(2020,0,1);
    printResult(fromCal, toCal);

    ...
```

calender 변수끼리 비교할 때 equals가 사용됨을 이 예제를 보고 알았다.

그 외에는 큰 차이는 보이지 않는다.

&nbsp;

## 예제 10_4

> 자신이 태어난 날부터 지금까지 며칠이 지났는지 계산해서 출력하시오.

자유롭게 코딩하도록 아무 조건도 주어지지 않아 재밌게 풀었던 문제이다.

Calender와 SimpleDataFormat 개념도 앞 예제를 풀면서 많이 익숙해졌다.

&nbsp;

### 내가 쓴 코드

```java
import java.util.*;
import java.text.*;
public class class10_4 {

	public static void main(String[] args) {
		Calendar mybirth = Calendar.getInstance();
		Calendar now = Calendar.getInstance();
		//0. 생일과 현재 날짜를 담을 calender(따로 지정해주지 않은 calender는 현재 시각으로 저장된다고 한다)
		mybirth.set(2001, 1, 1);
        //1. 내 생일을 저장
		
		long difference = ( now.getTimeInMillis() - mybirth.getTimeInMillis() )/1000/60/60/24;
        //2. 현재와 생일 사이의 간극을 일단위로 저장한다.

		Date nowMil = new Date(now.getTimeInMillis());
		Date birthMil = new Date(mybirth.getTimeInMillis());
        //3. calender 변수들을 Date 변수로 변환
		
		SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd");
		
		System.out.println("birth day="+df.format(birthMil));
		System.out.println("today="+df.format(nowMil));
		System.out.println(difference+" days");
        //4. df형태로 변수들을 출력
	}

}

```

&nbsp;

### 해설지 답안

```java
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;

class Exercise10_4 {
    public static void main(String[] args) {
        Calendar date1 = Calendar.getInstance();
        Calendar date2 = Calendar.getInstance();
        
        date1.set(2000, 0, 1); 
        date2.set(2016, 0, 29); 
        
        SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd");
        
        System.out.println("birth day="
        + df.format(new Date(date1.getTimeInMillis())));
        System.out.println("today ="
        + df.format(new Date(date2.getTimeInMillis())));
        
        long difference =
        (date2.getTimeInMillis() - date1.getTimeInMillis())/1000;
        
        System.out.println(difference/(24*60*60) +" days"); 
    }
}
```

&nbsp;

