---
layout: single
title: 프론트엔드 api-config 파일 작성시 'backendHost' is assigned a value but never used + Uncaught (in promise) SyntaxError: Unexpected token < in JSON at position ** 경고 해결법
catrgories:
- Javascript
---

![캡처](C:\Users\jojja\Desktop\코딩공부\백준 필기\캡처.JPG)

백엔드 서비스의 주소를 변수에 담고

현재 브라우저의 도메인이 localhost인 경우 로컬 호스트에서 동작하는 백엔드 어플리케이션을 만드는 과정이다. 이게 대체 무슨 말인지는 모르겠지만 오류가 나 확인해보니



![캡처2](C:\Users\jojja\Desktop\코딩공부\백준 필기\캡처2.JPG)

backendHost를 반환하도록 작성해 두었는데 사용되지 않았다 한다. 이상하다 분명 사용했는데!

해결법은 오탈자에 있었다.



![캡처3](C:\Users\jojja\Desktop\코딩공부\백준 필기\캡처3.JPG)

'${backendHost}' => \`${backendHost}\`로 바꿔주면 된다.

' 와 `의 차이라니..
