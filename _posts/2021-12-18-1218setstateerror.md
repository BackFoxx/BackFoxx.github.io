---
layout: single
title: "state값의 일부만 업데이트하기"
categories:
- Frontend
---

## 문제상황

![1218-D1](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/1218-D1.JPG)

App.js의 기본 state 상태.

&nbsp;

![1218-D5](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/1218-D5.JPG)

![1218D2](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/1218D2.JPG)

버튼을 누르면 app.js의 state 값이 업데이트 되도록 구현해 두었다.

&nbsp;

![1218-D3](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/1218-D3.JPG)

![1218-D4](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/1218-D4.JPG)

그런데 각 파트의 버튼을 누르면
다른 파트의 state값이 빈칸으로 초기화되는 일이 발생하였다.
setState의 특성 때문에 생긴 문제인 것 같았다.

&nbsp;

## 해결

![1218-D6](https://raw.githubusercontent.com/BackFoxx/BackFoxx.github.io/master/_image/1218-D6.JPG)

part 버튼의 로직을 위와 같이 수정하였더니
깔끔히 해결되었다.^^