---
emoji: 📌
title: useRef()와 useRef() type 설정하기
date: '2022-02-28 17:54:00'
author: 예슬
tags: 리액트, 타입스크립트
categories: REACT TYPESCRIPT
---

## ✨ useRef

- `useRef`은 mutable ref object를 리턴함.
- reference는 **read-only**이거나 **mutable**하다.
  - read-only : 읽기 전용 / mutable : 변경 가능한.
- ref 객체를 리액트에 전달하면 리액트는 `.current` 속성에 상응하는 DOM node값을 set한다.
- 여기서 중요한 것은 `ref`는 마운트 될 때 DOM node에 set되고, DOM node가 사라지면 `null`로 변경된다.

즉 useRef()는 초기 값을 그대로 읽거나 혹은 초기 값에서 변경되는 값을 사용한다.

## useRef()는 언제 사용할까?

### 📍 옵션 1: DOM Element Ref

- 주로 useRef()를 사용하는 방법 중 하나는 DOM element를 참조할때이다.
- 초기 값은 `null`로 설정한다.
- 이때는 DOM 엘리먼트를 참조하는 것이기 때문에 값은 **읽기-전용**으로 사용된다.
- DOM Element를 참조할 때는 어떤 엘리먼트를 참조하는지 type을 지정해준다.
- `HTMLDivElement` >>>> `HTMLElement` 👉 최대한 자세하게 타입을 지정해준다.

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

- 만약에 해당 ref가 절대 null이 아닌 경우 `non-null assertion operator (!)`를 사용한다.

```tsx
const divRef = useRef<HTMLDivElement>(null!);
```

### 📍 옵션 2: Mutable value ref

- ref를 바뀌는 값을 참조하는 용도로 사용하려면 `initial value`의 타입을 토대로 지정해주면 된다.

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

- 아직 사용해본 적이 없어서 적당한 예시를 찾지 못했는데 예를 들어서 숫자를 카운팅해주는 버튼의 이전 값을 보관하고 싶은 경우 ref로도 값을 보관할 수 있다.
- useRef()의 경우 리렌더링을 발생시키지 않는다. (useState()와 다른점)

출처 : [react-typescript-cheatsheet](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/hooks/#option-1-dom-element-ref)

```toc

```
