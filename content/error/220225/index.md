---
emoji: ๐ป
title: EventTarget์ 'getBoundingClientRect'์ด ๋์ง ์์ ๋
date: '2022-02-25 21:42:00'
author: ์์ฌ
tags: ์๋ฌ, ํ์์คํฌ๋ฆฝํธ
categories: ERROR TYPESCRIPT
---

## 1. Property 'getBoundingClientRect' does not exist on type 'EventTarget'.ts(2339)

![ํ์์คํฌ๋ฆฝํธ event.target ๋์  ์ฌ์ฉํ  ์ ์๋ ํด๋ต](solution.PNG)

์ ๋นํ ํด์ํด๋ณด๋ฉด React.MouseEvent๋ target ๋์ parameter๋ก currentTarget์ ๋ฐ์ ์ ์๋ค๋ ๋ด์ฉ์ด๋ค.

์ถ์ฒ: https://github.com/facebook/react/issues/16201

```toc

```
