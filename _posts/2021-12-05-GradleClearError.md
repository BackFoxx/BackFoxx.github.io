---
layout: single
title: ./gradle clean 오류날 때 대처법

categories: 
 - Spring
---

오류 상황:

./gradle build로 localhost에 접속하는 것에는 성공했는데,

./gradle clean으로 서버를 닫으려 할 때

```
What went wrong:
Execution failed for task ':clean'.
```

이런 오류가 나오면서 서버가 닫히지 않는다.

&nbsp;

이럴 땐 어딘가에서 사용되고 있기 때문이라는데

나는 아무 intelliJ 외에는 켜놓은 게 없는데 이게 무슨 말인가.

&nbsp;

이 때 컴퓨터 프롬프트(cmd) 창을 열어

이렇게 입력해보자.

```
TASKKILL /F /IM java.exe
```

입력 후에

```
성공: 프로세스 "java.exe"(PID *****)이(가) 종료되었습니다.
```

라고 뜨면 성공한 것.

&nbsp;

이후에 작업하던 곳으로 가서

./gradlew clean을 입력해주면 성공적으로 동작한다.
