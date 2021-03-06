---
emoji: ๐งโโ๏ธ
title: offsetWidth vs clientWidth vs getBoundingClientRect()
date: '2022-02-26 15:12:00'
author: ์์ฌ
tags: ์๋ฐ์คํฌ๋ฆฝํธ
categories: JAVASCRIPT
---

**ํด๋น ๊ฒ์๊ธ์ width๋ฅผ ๊ธฐ์ค์ผ๋ก ์์ฑ๋์์ต๋๋ค ๐ฉโ๐จ**

## 1. offsetWidth vs clientWidth์ ์ฐจ์ด

- `offsetWidth`๋ border๊น์ง ํฌํจํ ๊ธธ์ด๋ฅผ ๋ปํ๋ค.
  ![offsetWidth ์ค๋ช์ฌ์ง](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Determining_the_dimensions_of_elements/dimensions-offset.png)

- `clientWidth`๋ ์ปจํ์ธ  ํฌ๊ธฐ๋ฅผ ๊ธฐ์ค์ผ๋ก ํ๋ค. (padding ํฌํจ)
- ๊ทธ๋ฆผ์์๋ ๋ณผ ์ ์์ง๋ง ์คํฌ๋กค๋ฐ๋ ํฌํจ๋์ง ์๋๋ค.
  ![clientWidth ์ค๋ช์ฌ์ง](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Determining_the_dimensions_of_elements/dimensions-client.png)

## 2. (offsetWidth vs clientWidth) vs getBoundingClientRect()์ ์ฐจ์ด

### ๐ก 2.1 getBoundingClientRect()์ ๋ง์ ์ผ์ ํด!

- ์ฐ์  getBoundingClientRect() ๋ฉ์๋๋ `DOMRect` ๊ฐ์ฒด๋ฅผ ๋ฆฌํดํ๋ค. ์ด๋ ์๋ฆฌ๋จผํธ์ ์ฌ์ด์ฆ์ ๋ทฐํฌํธ๋ฅผ ๊ธฐ์ค์ผ๋ก ํ ์๋ฆฌ๋จผํธ์ ์์น๋ฅผ ๋ฐํํ๋ค.
- getBoundingClientRect()์ผ๋ก ๋ฆฌํด ๋ฐ์ ์ ์๋ ๊ฐ : `x`/`left`, `y`/`top`, `right`, `bottom`, `width`, `height`
  ![getBoundingClientRect()๋ฉ์๋ ์ค๋ช](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect/element-box-diagram.png)

- ์ฌ๊ธฐ์ `width`์ `height`๋ offsetWidth์ ์ผ์นํ๋ค. ์ฆ padding, border๊น์ง ํฌํจํ ๊ฐ์ด๋ค.

### ๐ 2.2 `box-sizing`์ ์ฃผ์ํ์!

์์) `width: 100px; padding: 10px; border: 2px solid #000;`์ธ ๊ฒฝ์ฐ
| | `clientWidth` | `offsetWidth` | `getBoundingClientRect().width` |
|--- |--- |--- |--- |
| `content-box` | 120px | 124px | 123.999..px |
| `border-box` | 96px | 100px | 99.999...px |

1. `content-box`๋ ์ค์ง `width`์ ๊ธฐ์ค
   ์ฆ, `clientWidth`๋ padding๊น์ง ํฌํจ์ด๊ธฐ ๋๋ฌธ์ width + padding x 2์ด๋ฉฐ, `offsetWidth`๊ณผ `getBoundingClientRect().width`๋ border๊น์ง ํฌํจํด์ผํ๊ธฐ ๋๋ฌธ์ width + padding x 2 + border x 2๊ฐ ๋๋ค.

2. `border-box`์ ๊ธฐ์ค์ width+padding+border๋ฅผ ํฌํจ.
   ์ฆ, `clientWidth`๋ border๋ฅผ ํฌํจํด์ผํ์ง ์๊ธฐ ๋๋ฌธ์ border๋ฅผ ๋นผ์ค ๊ฐ์ด๋ฉฐ, `offsetWidth`๊ณผ `getBoundingClientRect().width`๋ ๋ชจ๋ ํฌํจํด์ผํ๊ธฐ ๋๋ฌธ์ width๊ฐ์ ๊ทธ๋๋ก ์ฌ์ฉํ๋ฉด ๋๋ค.

๋๋ฌด๋๋ ๊ธธ์ด์ก๋๋ฐ ์ฃผ๋ก `box-sizing: border-box`๋ฅผ ํ๋ ๊ฒฝ์ฐ๊ฐ ๋ง๊ธฐ ๋๋ฌธ์ ์ฐ๋ฆฌ๊ฐ ์๊ฐํ๋ `width`๋ฅผ ๊ตฌํ๊ธฐ ์ํด์๋ **`offsetWidth`** ๊ณผ **`getBoundingClientRect().width`**๋ฅผ ์ฌ์ฉํ๋๊ฒ ๋ง๋ค.

### ๐ซ 2.3 ๊ทธ๋ผ `offsetWidth`๊ณผ `getBoundingClientRect().width`์ ์ฐจ์ด๋ ๋์ฒด ๋ญ์ผ?

์๋ง 2.1๊ณผ 2.2๋ฅผ ์ฝ์ ์ฌ๋์ด๋ผ๋ฉด `clientWidth`์ `getBoundingClientRect().width`์ ์ฐจ์ด๋ ์์์ ๊ฒ์ด๋ค. ๊ทผ๋ฐ `offsetWidth`๊ณผ `getBoundingClientRect().width`์ ์ฐจ์ด๋?...๐ฅ

๊ฒฐ๋ก ์ ๋งํ์๋ฉด ๋์ ๊ฐ์ ๊ฐ๋ค! **๋ค๋ง ๋ค๋ฅธ CSS ์์ฑ์ด width๋ฅผ ๋ณํ์ํค์ง ์๋๋ค๋ฉด ๋ง์ด๋ค**

์๋ฅผ ๋ค์ด, ํด๋น ์์ฑ์ ๊ฐ์ง ๋ฐ์ค๊ฐ ์๋ค๊ณ  ๊ฐ์ ํด๋ณด์

```css
.box {
  width: 100px;
  height: 100px;
  transform: scale(0.5);
}
```

๊ฒฐ๋ก ๋ถํฐ ๋งํ์๋ฉด
`clientWidth` = 100px
`offsetWidth` = 100px
`getBoundingClientRect().width` = 49.999...px

**์ฆ `getBoundingClientRect().width`์ ๋ ๋๋ง ๋ `width`๋ฅผ ๋ฐํํ๊ธฐ ๋๋ฌธ์, `transform`์ด ์ ์ฉ๋ ๊ฐ์ ๋ฆฌํดํ๋ค.**

### ๐ 2.4 ๋ด๊ฐ ์ง์ด๋ณด๋ ๊ฒฐ๋ก 

1. ์์์  ์๋ ์ ์๋ฅผ ์ํ๋ค: `offsetWidth` `clientWidth`
2. CSS ์ดํด๋ณด๊ธฐ ์ซ๊ณ  ์ต์ข `width`๊ฐ์ ์ํ๋ค: `getBoundingClientRect().width`
3. `box-sizing: border-box` ์ผ ๋ ์ฐ๋ฆฌ๊ฐ ์ํ๋ ๊ทธ `width`๊ฐ:
   `offsetWidth` `getBoundingClientRect().width`

- ์ฌ๊ธฐ์ ๋งํ๋ ๊ทธ `width`๊ฐ์ width+padding+border๋ฅผ ๋ชจ๋ ํฌํจํ ๊ฐ์ ์ผ์ปซ๋๋ค.

์ถ์ฒ 1: [MDN - Determining the dimensions of elements](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Determining_the_dimensions_of_elements)
์ถ์ฒ 2: [MDN - Element.getBoundingClientRect()](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect)

```toc

```
