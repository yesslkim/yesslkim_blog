---
emoji: ๐ป
title: Variable 'age' is used before being assigned - Typescript
date: '2022-02-26 18:58:00'
author: ์์ฌ
tags: ํ์์คํฌ๋ฆฝํธ, ์๋ฌ
categories: ERROR TYPESCRIPT
---

## `let age;` ์ธ๋ฐ ํ ๋น๋๊ธฐ ์ ์ ์ฌ์ฉ๋์๋ค๊ณ ?

์์๋ฅผ ๋ค์ด๋ณด์

```ts
let age: number; // 1๏ธโฃ num์ด number type์ผ๋ก ์ง์ ๋จ.

if (isActive) {
  age = 100;
}

console.log(`๋ด ๋์ด๋ ${age}์ด์ด์ผ`);
// 2๏ธโฃ ๐คฏ ERROR : Variable 'age' is used before being assigned
```

๋ถ๋ช let age๋ก ์ ์ธ๋์๋๋ฐ ์ ์ ๋ฐ ์๋ฌ๊ฐ ๋ฐ๊น?
์ฐ๋ฆฌ๋ ์ฌ๊ธฐ์ ์์์ผ ํ๋ค. `let age;`๋ **ํ ๋น(assigned)** ๋ ๊ฒ์ด ์๋๋ผ **์ ์ธ(declare)** ๋ ๊ฒ์ด๋ค.

- ์ฌ๊ธฐ์ ์ ์ ์๋ ๊ฒ์ ๋ง์ฝ์ if๋ฌธ์ด ์คํ๋์ง ์์ผ๋ฉด `age`๋ ์ ์ธ๋ง ๋์์ ๋ฟ ํ ๋น๋์ง ์์๋ค. ์ฆ ์ ํ ํ ๋น๋์ง ์์ ๊ฒ์ด๋ค.

### ๊ทผ๋ฐ ์ ํ ๋น๋์ง ์์ ๊ฒ์ผ๊น?

ํด๋ต์ ์ฌ๊ธฐ์๋ค

```ts
let age: number;
```

์ฐ๋ฆฌ๊ฐ age๋ฅผ number type์ผ๋ก ์ง์ ํ์๊ธฐ ๋๋ฌธ์ ๋ค๋ฅธ ๊ฐ์ด ๋ค์ด์ค๋ฉด ์๋ฌ๊ฐ ๋จ๊ฒ ๋๋ค.

## โจ ํด๊ฒฐ ๋ฐฉ๋ฒ

1. undefined ๊ฐ๋ ๊ด์ฐฎ์ ๊ฒฝ์ฐ : ์ด๊ธฐ ๊ฐ์ธ undefined๋ ํจ๊ป ํ์์ผ๋ก ์ง์ ํด์ค๋ค.

```ts
let age: number | undefined = undefined;
```

2. ๋ฌด์กฐ๊ฑด number ํ์์ผ๋ก ์ง์ ๋  ๊ฒฝ์ฐ : Definite Assignment Assertions์ ์ฌ์ฉํ๋ค.
   [Definite Assignment Assertions](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-7.html#definite-assignment-assertions)์ด๋ ์ปดํ์ผ๋ฌ์๊ฒ ๊ฐ์ด ๋ฌด์กฐ๊ฑด ํ ๋น๋์ด ์๋ค๊ณ  ์ปดํ์ผ๋ฌ์๊ฒ ์ ๋ฌํ๋ ๊ฒฝ์ฐ์ด๋ค. ์ฆ ์ฒ์์ `number | undefined`์ผ๋ก ์ง์ ๋์ง๋ง ๊ฐ์ด ํ ๋น๋๋ฉด number type์ผ๋ก ์ธ์งํ๋ค.

- ์ฐธ๊ณ ๋ก (!)๋ Non-null assertion operator๋ก๋ ์ฌ์ฉ๋๋ค. ์ฆ null์ด ์๋๋ผ๊ณ  ๋จ์ธํด์ค ๋ ์ฌ์ฉ๋๋ค.

์ฐธ๊ณ ์๋ฃ: [Definite Assignment Assertions](https://stackoverflow.com/questions/67351411/what-s-the-difference-between-definite-assignment-assertion-and-ambient-declarat)

์๋ฌธ ์ถ์ฒ: [Variable 'test' is used before being assigned - Typescript](https://stackoverflow.com/questions/44832316/variable-test-is-used-before-being-assigned-typescript)

```toc

```
