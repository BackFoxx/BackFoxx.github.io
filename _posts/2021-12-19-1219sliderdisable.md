---
layout: single
title: "mui(material-ui) 비활성화/활성화 상태 바꾸는 기능 구현하기"
categories:
- Frontend
---

## 문제상황

mui로 만든 슬라이더 오브젝트에는 
'disabled'라는 attribute가 있다.
disabled가 true일 때는 슬라이더가 하얗게 변하며 비활성화 상태가 되는데,

나는 슬라이더의 disabled를 평소에는 true로 두다가,
슬라이더 옆의 체크박스를 누르면 disabled가 false로 변하는 기능을 구현하려 했다.

![1219-A5](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/1219-A5.JPG)

(↑ disabled={true} )

![1219-A7](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/1219-A7.JPG)

(↑ disabled={false} )

&nbsp;

![1219-A](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/1219-A.JPG)

반복문으로 만든 리스트라 슬라이더마다 id가 있는데,
getElementById로 슬라이더를 가져온 후
getAtribute로 disabled의 값을 반대로 바꾸면 되겠지! 했는데
아니나 다를까 반응이 없었다.

&nbsp;

![1219-A1](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/1219-A1.JPG)

왜인가를 테스트하기 위해
slider의 disabled를 콘솔로 출력해 살펴보기로 했다.



![1219-A2](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/1219-A2.JPG)

true 아니면 false가 나와야 하는데
아무 값도 없었다!

왜인가를 테스트하기 위해
가져온 슬라이더 자체를 한번 뜯어보기로 했다.
![1219-A3](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/1219-A3.JPG)

&nbsp;

![1219-A4](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/1219-A4.JPG)

비주얼 스튜디오 코드 안에서는 분명 \<slider>\</slider>인 것이
HTML 안에서는 span 다발로 렌더링되어 있었다.

그래도 일단 id는 양호하군.
만약 disabled가 활성화되어 있다면?

![1219-A6](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/1219-A6.JPG)

''Mui-disabled"라는 클래스가 추가되어 있다.
그럼 옳거니, 클래스명에 Mui-disabled를 넣었다 뺐다 하는 기능만 넣으면 되겠구나!
곧바로 로직을 수정했다.

&nbsp;

![1219-A10](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/1219-A10.JPG)

className, classList를 이용해 disable 추가/삭제 메소드를 완성했다.

classList로 통일하려니 배열이 readon 형태라 indexOf, includes함수가 적용이 안되고,
className으로 통일하려니 disabled를 빼자마자 클래스가 NaN으로 날아가버렸다.
부득이하게 둘을 적절히 분리하여 완성하였다.

&nbsp;

![1219-A11](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/1219-A11.JPG)

굳굳