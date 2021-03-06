---
emoji: ๐ฉโ๐ป
title: ํ์์คํฌ๋ฆฝํธ์ EventTarget๐
date: '2022-02-26 16:30:00'
author: ์์ฌ
tags: ํ์์คํฌ๋ฆฝํธ
categories: TYPESCRIPT
---

## ํ์์คํฌ๋ฆฝํธ์ EventTarget

ํ์์คํฌ๋ฆฝํธ๋ฅผ ์ฌ์ฉํ๋ฉด์ ์ด๋ฒคํธ ํ๊น์ ์ฌ์ฉํ๋ฉด ์ข์ข ์๋ฌ๋ฅผ ๋ง์ฃผํ๊ณค ํ๋ค.

๋น ๋ฅด๊ฒ ๊ทธ ์ด์ ๋ฅผ ๋งํ์๋ฉด, EventTarget์ **Element type**์ผ๋ก๋ถํฐ ์์๋ฐ์ง ์๊ธฐ ๋๋ฌธ์ ์๋ฌ๋ฅผ ๋ง๋๊ฒ ๋๋ ๊ฒ์ด๋ค. ๊ทธ๋ ๊ธฐ์ id ํน์ class์ ๊ฐ์ ์์ฑ์ ์ธ์งํ์ง ๋ชปํ๋ ๊ฒ์ด๋ค. ์ฆ, ์ด๋ฒคํธ ํ๊น์ EventTarget์ ํ์์ด ์๋ค.

> **๊ทธ๋ผ ์ Element type์์ ์์๋ฐ์ง ์๋ ๊ฒ์ผ๊น?**
> ๋๋ ์ด ์๊ฐ์ ๊ฐ์ฅ ๋ง์ด ํ๋ค. ๊ฒฐ๋ก ์ ์ผ๋ก ์ฐ๋ฆฌ๊ฐ ์ด๋ฒคํธ๋ฅผ ์คํ์ํฌ ๋ ๊ฐ์ฅ ๋ง์ด ํ๋ ์ผ์ ์จ๋ฆฌ๋จผํธ์ ์ด๋ฒคํธ๋ฅผ ๋ถ์ด๊ธฐ ๋๋ฌธ์ด๋ค!

**ํ์ง๋ง ์ฐ๋ฆฌ๊ฐ ์์์ผ ํ  ๊ฒ์ ๋ชจ๋  ์ด๋ฒคํธ ํ๊น์ด HTML elements์ ํ์ ๋์ง ์๋ ๋ค๋ ๊ฒ์ด๋ค**

์๋ฅผ ๋ค๋ฉด, `XMLHttpRequest`, `FileReader`, `AudioNode`, `AudioContext` ๋ฑ..

### โจ ํด๊ฒฐ๋ฐฉ๋ฒ1 : Target์ ํ์์ ์ง์ ํด์ค๋ค.

```js
const menuBtn = document.querySelector('.menu_btn');

menuBtn.addEventListener('click', function (e) {
    const target = e.target as Element; // 1๏ธโฃ
    (e.target as Element).className; // 2๏ธโฃ
}, false);

// 3๏ธโฃ
menuBtn.addEventListener('click', function (e: { target: Element }) {
    console.log(e.target.className); // 'foo'
}, false);
```

1. e.target์ด Element๋ผ๋ ๊ฒ์ ์๋ ค์ค๋ค.
2. inline์ผ๋ก ์ฌ์ฉํ๋ค.
3. ๋ง์ฝ์ ์ด๋ฒคํธ์ target ์์ฑ๋ง ์ฌ์ฉํ  ๊ฒฝ์ฐ ์ด๋ ๊ฒ ์ ์ด์ค๋ค.

๋น์ฐํ ๋ง์ด์ง๋ง ์ด๋ฒคํธ์ ํ์์ ์ง์ ํ ๊ฒ์ด ์๋๊ธฐ ๋๋ฌธ์ `e.type`๊ณผ ๊ฐ์ ํ๊น ์ธ์ ๋ค๋ฅธ ์์ฑ์ ์ฌ์ฉํ๋ฉด ์ค๋ฅ๊ฐ ๋ฐ์ํ๋ค.

### โจ ํด๊ฒฐ๋ฐฉ๋ฒ2 : Event์ ํ์์ ์ง์ ํด์ค๋ค.

์ด๋ฒคํธ ์์ฒด์ ํ์์ ์ง์ ํด์ฃผ๋ฉด target์ด์ธ์ ๋ค๋ฅธ ์์ฑ๋ ์ฌ์ฉํ  ์ ์๋ค.
๋ฌผ๋ก  ํ๊น์ Element์ธ์ ๋ค๋ฅธ ํ๊น๋ ๋ฐ์์ฌ ์ ์๊ธฐ ๋๋ฌธ์ ํจ๊ป ์ง์ ํด์ฃผ์ด์ผ ํ๋ค!

```js
const menuBtn = document.querySelector('.menu_btn');

menuBtn.addEventListener(
  'click',
  function (e: Event & { target: Element }) {
    console.log(e.target.className); // 'menu_btn'
    console.log(e.type); // 'click'
  },
  false,
);
```

### โจ ํด๊ฒฐ๋ฐฉ๋ฒ3 : EventTarget์ ํ์์ ๋ ๋ชํํ๊ฒ ์ง์ ํ  ์ ์์ผ๋ฉด ๊ทธ๋ ๊ฒ ํด์ผํ๋ค..

์๋ฅผ ๋ค๋ฉฐ, form event๋ฅผ ์์ฑํด์ผํ๋ค๊ณ  ๊ฐ์ ํด๋ณด์.
์๋ง ๋๋ถ๋ถ์ ์ฌ๋๋ค์ input์ value๋ฅผ ๋ฐ์์ค๋ ์์์ ์์ฑํ๊ณ  ์์ ๊ฒ์ด๋ค (= ๋๐ฉโ๐ป)

๊ทธ๋ ๋ ๋ค๋ฅธ **์๋ฌ**๋ฅผ ๋ง์ฃผํ๊ฒ ๋  ๊ฒ์ด๋ค. ๐คฌ
๐ป : `"Property 'value' does not exist on type 'EventTarget'"`

๊ทธ๋๋ ๋ ๋ํ์ผํ๊ฒ Target์ ํ์์ ์ง์ ํด์ฃผ๋ฉด ๋๋ค ๐

```js
const input = document.getElementById('input_elem');

input.addEventListener('input', function (e) {
    console.log((e.target as HTMLInputElement).value);
}, false);
```

- EventTarget์ ํ์์๋ ์์ง๋ง HTMLInputElement ํ์์๋ value ์์ฑ์ด ์๊ธฐ ๋๋ฌธ์ ์๋์ด ๋๋ค.

### ๊ทธ ์ธ์ ์์ฃผ ์ฌ์ฉํ๋ฉด ํ์ ๋ชจ์

```js
// classList ์์ฑ ์ฌ์ฉ ์
e.target as Element
e.target as HTMLElement


e.target as HTMLImageElement
e.target as HTMLMediaElement
e.target as HTMLVideoElement
e.target as HTMLAudioElement
e.target as HTMLInputElement
e.target as HTMLTextAreaElement

// ์ด๋ ๊ฒ ํ์์ ์ง์ ํด ์ค ํ ์ฌ์ฉ๋ ๊ฐ๋ฅ!
type InputType = HTMLInputElement | HTMLTextAreaElement
e.target as InputType
```

์ถ์ฒ: [www.designcise.com](https://www.designcise.com/web/tutorial/how-to-fix-property-does-not-exist-on-type-eventtarget-typescript-error)

```toc

```
