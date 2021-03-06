---
emoji: ๐
title: useRef()์ useRef() type ์ค์ ํ๊ธฐ
date: '2022-02-28 17:54:00'
author: ์์ฌ
tags: ๋ฆฌ์กํธ, ํ์์คํฌ๋ฆฝํธ
categories: REACT TYPESCRIPT
---

## โจ useRef

- `useRef`์ mutable ref object๋ฅผ ๋ฆฌํดํจ.
- reference๋ **read-only**์ด๊ฑฐ๋ **mutable**ํ๋ค.
  - read-only : ์ฝ๊ธฐ ์ ์ฉ / mutable : ๋ณ๊ฒฝ ๊ฐ๋ฅํ.
- ref ๊ฐ์ฒด๋ฅผ ๋ฆฌ์กํธ์ ์ ๋ฌํ๋ฉด ๋ฆฌ์กํธ๋ `.current` ์์ฑ์ ์์ํ๋ DOM node๊ฐ์ setํ๋ค.
- ์ฌ๊ธฐ์ ์ค์ํ ๊ฒ์ `ref`๋ ๋ง์ดํธ ๋  ๋ DOM node์ set๋๊ณ , DOM node๊ฐ ์ฌ๋ผ์ง๋ฉด `null`๋ก ๋ณ๊ฒฝ๋๋ค.

์ฆ useRef()๋ ์ด๊ธฐ ๊ฐ์ ๊ทธ๋๋ก ์ฝ๊ฑฐ๋ ํน์ ์ด๊ธฐ ๊ฐ์์ ๋ณ๊ฒฝ๋๋ ๊ฐ์ ์ฌ์ฉํ๋ค.

## useRef()๋ ์ธ์  ์ฌ์ฉํ ๊น?

### ๐ ์ต์ 1: DOM Element Ref

- ์ฃผ๋ก useRef()๋ฅผ ์ฌ์ฉํ๋ ๋ฐฉ๋ฒ ์ค ํ๋๋ DOM element๋ฅผ ์ฐธ์กฐํ ๋์ด๋ค.
- ์ด๊ธฐ ๊ฐ์ `null`๋ก ์ค์ ํ๋ค.
- ์ด๋๋ DOM ์๋ฆฌ๋จผํธ๋ฅผ ์ฐธ์กฐํ๋ ๊ฒ์ด๊ธฐ ๋๋ฌธ์ ๊ฐ์ **์ฝ๊ธฐ-์ ์ฉ**์ผ๋ก ์ฌ์ฉ๋๋ค.
- DOM Element๋ฅผ ์ฐธ์กฐํ  ๋๋ ์ด๋ค ์๋ฆฌ๋จผํธ๋ฅผ ์ฐธ์กฐํ๋์ง type์ ์ง์ ํด์ค๋ค.
- `HTMLDivElement` >>>> `HTMLElement` ๐ ์ต๋ํ ์์ธํ๊ฒ ํ์์ ์ง์ ํด์ค๋ค.

```tsx
function swingBox() {
  const divRef = useRef<HTMLDivElement>(null);

  useEffect(() => {
    if (!divRef.current) return;
    animateBox(divRef.current);
  });

  return <div ref={divRef}>BOX</div>;
}
```

- ๋ง์ฝ์ ํด๋น ref๊ฐ ์ ๋ null์ด ์๋ ๊ฒฝ์ฐ `non-null assertion operator (!)`๋ฅผ ์ฌ์ฉํ๋ค.

```tsx
const divRef = useRef<HTMLDivElement>(null!);
```

### ๐ ์ต์ 2: Mutable value ref

- ref๋ฅผ ๋ฐ๋๋ ๊ฐ์ ์ฐธ์กฐํ๋ ์ฉ๋๋ก ์ฌ์ฉํ๋ ค๋ฉด `initial value`์ ํ์์ ํ ๋๋ก ์ง์ ํด์ฃผ๋ฉด ๋๋ค.

```tsx
import { useRef, useState } from 'react';

const CountNum = () => {
  const [num, setNum] = useState(0);
  const buttonRef = useRef<number | null>(null);
  return (
    <button
      type="button"
      onClick={() => {
        buttonRef.current = num;
        setNum((prevState) => prevState + 1);
      }}
    >
      {num}
    </button>
  );
};

export default CountNum;
```

- ์์ง ์ฌ์ฉํด๋ณธ ์ ์ด ์์ด์ ์ ๋นํ ์์๋ฅผ ์ฐพ์ง ๋ชปํ๋๋ฐ ์๋ฅผ ๋ค์ด์ ์ซ์๋ฅผ ์นด์ดํํด์ฃผ๋ ๋ฒํผ์ ์ด์  ๊ฐ์ ๋ณด๊ดํ๊ณ  ์ถ์ ๊ฒฝ์ฐ ref๋ก๋ ๊ฐ์ ๋ณด๊ดํ  ์ ์๋ค.
- useRef()์ ๊ฒฝ์ฐ ๋ฆฌ๋ ๋๋ง์ ๋ฐ์์ํค์ง ์๋๋ค. (useState()์ ๋ค๋ฅธ์ )

์ถ์ฒ : [react-typescript-cheatsheet](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/hooks/#option-1-dom-element-ref)

```toc

```
