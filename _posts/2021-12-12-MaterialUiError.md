---
layout: single
title: "Material UI 사용시 Invalid hook call. Hooks can only be called inside of the body of a function component. material ui 오류 해결법"
categories:
- Java
---





'React.js, 스프링 부트, AWS로 배우는 웹 개발 101' 책을 보며 실습하던 도중

Material ui를 이용한 디자인 (실습코드 3-13, 3-14)에서 오류에 직면했습니다.

![](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/%EC%BA%A1%EC%B2%98.JPG)

분명 책의 예제와 토시 하나 틀리지 않았건만..



![캡처2](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/%EC%BA%A1%EC%B2%982.JPG)

이런 개같은!

오류 메시지를 복사하여 구글에 검색해도 이렇다할 해결법은 없었습니다.



Material Ui 메뉴얼을 천천히 보다가

혹시 이게 문제인가? 하며

![캡처3](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/%EC%BA%A1%EC%B2%983.JPG)

import문을 괄호에 넣지 않고 하나하나 분리해서 작성해 보았습니다.



![캡처4](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/%EC%BA%A1%EC%B2%984.JPG)

해결되었습니다. 