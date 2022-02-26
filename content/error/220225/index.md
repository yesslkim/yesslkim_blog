---
emoji: 👻
title: EventTarget에 'getBoundingClientRect'이 되지 않을 때
date: '2022-02-25 21:42:00'
author: 예슬
tags: 에러, 타입스크립트
categories: ERROR TYPESCRIPT
---

## 1. Property 'getBoundingClientRect' does not exist on type 'EventTarget'.ts(2339)

![타입스크립트 event.target 대신 사용할 수 있는 해답](solution.PNG)

적당히 해석해보면 React.MouseEvent는 target 대시 parameter로 currentTarget을 받을 수 있다는 내용이다.

출처: https://github.com/facebook/react/issues/16201

```toc

```
