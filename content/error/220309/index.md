---
emoji: 😱
title: SCRIPT5022 SecurityError
date: '2022-03-09 02:39:00'
author: 예슬
tags: IE, 에러, SecurityError
categories: ERROR
---

## IE11에서 SCRIPT5022 SecurityError

- 아마 리액트-타입스크립트 프로젝트를 하면서 만나는 수많은 IE의 에러 중 하나
- 읽어보니 문제는 웹소켓을 로컬 도메인에서 열려고 할 때 생기는 에러라고 한다.

### ✨ 해결방법 :

- 인터넷 옵션에 들어가서 보안 관련 항목을 변경해준다
- `Tools > Internet Options > Security > Local Intranet > Sites`

![internetoption](https://i.stack.imgur.com/fqpzH.png)

### ✨ 또 다른 해결방법 :

- 인터넷 옵션에 들어가서 localhost 주소를 추가해준다.
- `ls > Internet Options > Security > Local Intranet > Sites > Advanced`

![internetoption](https://i.stack.imgur.com/x7rQZ.png)

출처: [stackoverflow](https://stackoverflow.com/questions/15114279/websocket-on-ie10-giving-a-securityerror/20145203#20145203)

```toc

```
