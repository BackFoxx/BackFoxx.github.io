---
layout: single
title: "버튼의 값을 State에 할당하는 방법"
categories:
- javascript
---

참고: 

[스택플로우]: https://stackoverflow.com/questions/56142032/binding-and-saving-react-button-value

&nbsp;

내가 하려던 것은 간단했다.

&nbsp;

![20211217-2](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/20211217-2.JPG)

여기에 state가 있다.
컴포넌트 내부에 임시로 저장하기 위해
part를 초기화했다.

&nbsp;

![20211217-1](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/20211217-1.JPG)

그리고 여기에 버튼이 있다.
버튼에 적힌 글과 value값은 같다.

&nbsp;

나는 버튼을 누르면 버튼의 값이 state에 저장되었으면 했다.
대부분 텍스트박스를 하나 만들고 
거기에 입력하는 내용을 state에 저장하는 방법만 알려주던데
내가 하려는 건 훨씬 단순했다. 넣으려는 값이 정해져 있으니까!

그런데도 뭐가 문제인건지
끝없이 오류가 나고 3시간을 해맸다.

&nbsp;

그러다 스택플로우에 올라온 글을 발견!
innerHTML을 이용해 \<Button>\</Button> 내부의 값을 state에 넣는다는
멋진 답변을 보고 적용해 보았다.

![20211217-3](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/20211217-3.JPG)

 ![20211217-4](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/20211217-4.JPG)

대성공이다! 수고했다 나 자신
