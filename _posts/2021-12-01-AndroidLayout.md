---
layout: single
title: Android Studio 기본 강의 정리-1

categories: 
 - Android
---

레이아웃: 뷰가 배치되는 모양을 결정하는 것

1. **Linear Layout**: 좌에서 우, 위에서 아래 방향으로 뷰를 배치하는 레이아웃

   oriantation: 뷰의 배치 방향

   (프로젝트 최초로 생성할때 레이아웃을 일단 LinearLayout으로 하는 게 좋다 한다.)

   Weight: 공간 중에서 weight에 비례해 차지하는 공간이 늘어난다






1. **Relative Layout**: 뷰들간의 관계를 설정함. 레이아웃 자체는 별 기능이 없다.

   alignparent* = 자신의 *를 부모의 *에 맞추도록 배정한다. 기본적으로 left+top 

   ```xml
   android:layout_centerInParent="true"
   ```

   

   

   center* =자신을 부모의 중앙에 맞춘다(*는 세로또는 가로,또는 전체)

​		align* = 지정된 객체의 *에 자신의 *를 맞추어 정렬한다.	

        ```xml
        android:layout_height="wrap_content"
        ```



## 글자

​		



TextView : 사용자에게 문자열을 보여준다.

​		Text: 문자열을 설정한다.

​		textAppearance: 문자를 꾸민다.





MainActivity.java 파일과 연동하여
문자열과 관련된 메소드를 사용할 수 있다.

```java
package kr.co.softcampus.relativelayout;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {

    //뷰의 주소값 담을 참조변수
    TextView text1;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        //id가 text2인 뷰의 주소 값을 얻어온다
        text1 = (TextView) findViewById(R.id.Text2);
        //새로운 문자열 설정
        text1.setText("새로운 문자열");
    }
}
```

TextView.setText(" ") : 지정한 문자열을 수정한다.

​		



## 버튼

```java
package kr.co.softcampus.relativelayout;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {

    //뷰의 주소 값을 담을 참조 변수
    TextView text1;
    Button button1, button2, button3, button4;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        text1 = (TextView) findViewById(R.id.textView4);
        button1 = (Button)findViewById(R.id.button6);
        button2 = (Button)findViewById(R.id.button);
        button3 = (Button)findViewById(R.id.button2);
        button4 = (Button)findViewById(R.id.button3);
        //0. xml의 button6을 button1 변수에 저장한다.

        BtnListener1 listener1 = new BtnListener1();
        BtnListener2 listener2 = new BtnListener2();
        BtnListener34 listener34 = new BtnListener34();
        //BtnListener1 인스턴스 객체를 만든다.
        button1.setOnClickListener(listener1);
        button2.setOnClickListener(listener2);
        button3.setOnClickListener(listener34);
        button4.setOnClickListener(listener34);

        //리스너를 버튼 객체에 설정한다.
    }

    //버튼을 눌렀을 때 수행되는 동작을 오버라이딩한다.
    class BtnListener1 implements View.OnClickListener {
        @Override
        public void onClick(View v) {
            text1.setText("첫 번째 버튼을 눌렀습니다");
        }
        //view v에는 누른 버튼 객테의 주소값이 들어온다
    }

    //두번 째
    class BtnListener2 implements View.OnClickListener {
        @Override
        public void onClick(View v) {
            text1.setText("두 번째 버튼을 눌렀습니다");
        }
    }

    //세번 째,네번 째
    class BtnListener34 implements View.OnClickListener {
        @Override
        public void onClick(View v) {
            //이벤트 발생된 뷰의 id 추출
            int id = v.getId();
            //id로 분기
            switch (id) {
                case R.id.button2:
                    text1.setText("세 번째 버튼을 눌렀습니다");
                    break;

                case R.id.button3:
                    text1.setText("네 번째 버튼을 눌렀습니다");
            }
        }
    }

    //다섯 번째 버튼을 누르면 호출되는 메서드
    public void btn5Method(View view) {
    text1.setText("다섯 번째 버튼을 눌렀습니다"); }

    //다섯 번째 버튼을 누르면 호출되는 메서드
    public void btn6Method(View view) {
    text1.setText("여섯 번째 버튼을 눌렀습니다"); }

    //일곱 번째, 여덟 번째
    public void btn78Method(View view) {
        int id = view.getId();
        switch (id) {
            case R.id.button7:
                text1.setText("일곱 번째");
                break;
            case R.id.button8:
                text1.setText("여덟 번째");
                break;
        }
    }
}


```





1. 버튼 변수를 선언한다.

   ```java
   TextView text1;//글자
   Button button1, button2, button3, button4;//버튼
   ```






1. 변수에 xml에 있는 버튼을 연결한다.

   ```java
   text1 = (TextView) findViewById(R.id.textView4);
   button1 = (Button)findViewById(R.id.button6);
   ```





3. 버튼을 눌렀을 때 일어날 동작을 클래스로 만든다.

   ```java
       class BtnListener1 implements View.OnClickListener {
           @Override
           public void onClick(View v) {
               text1.setText("첫 번째 버튼을 눌렀습니다");
           }
           //view v에는 누른 버튼 객테의 주소값이 들어온다
       }
   ```

   조상 View.onClickListener를 상속하기 위애 onClick을 반드시 오버라이딩해야 한다.






3. 클래스가 인스턴스이므로 객체를 생성한다

   ```java
   BtnListener1 listener1 = new BtnListener1();
   ```





5. 버튼을 누르면 listener1이 동장하도록 연결한다.

   ```java
   button1.setOnClickListener(listener1);
   ```






onclick은 너무 많이 쓰이는 거라

public 메소드만 써놓으면 3번만 수행하고도 위와 같은 효과를 낼 수 있도록 되어있다.

**onclick 하나만!**





0. 버튼을 누르면 수행될 메소드를 만든다.

   ```java
   public void btn5Method(View view) {
   text1.setText("다섯 번째 버튼을 눌렀습니다"); }
   ```





1. xml에서 버튼을 눌러 onclick과 연결한다.
