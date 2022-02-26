---
emoji: 👩‍💻
title: 타입스크립트와 EventTarget💗
date: '2022-02-26 16:30:00'
author: 예슬
tags: 타입스크립트
categories: TYPESCRIPT
---

## 타입스크립트와 EventTarget

타입스크립트를 사용하면서 이벤트 타깃을 사용하면 종종 에러를 마주하곤 한다.

빠르게 그 이유를 말하자면, EventTarget은 **Element type**으로부터 상속받지 않기 때문에 에러를 만나게 되는 것이다. 그렇기에 id 혹은 class와 같은 속성을 인지하지 못하는 것이다. 즉, 이벤트 타깃은 EventTarget의 타입이 있다.

> **그럼 왜 Element type에서 상속받지 않는 것일까?**
> 나도 이 생각을 가장 많이 했다. 결론적으로 우리가 이벤트를 실행시킬 때 가장 많이 하는 일은 앨리먼트에 이벤트를 붙이기 때문이다!

**하지만 우리가 알아야 할 것은 모든 이벤트 타깃이 HTML elements에 한정되지 않는 다는 것이다**

예를 들면, `XMLHttpRequest`, `FileReader`, `AudioNode`, `AudioContext` 등..

### ✨ 해결방법1 : Target의 타입을 지정해준다.

```js
const menuBtn = document.querySelector('.menu_btn');

menuBtn.addEventListener('click', function (e) {
    const target = e.target as Element; // 1️⃣
    (e.target as Element).className; // 2️⃣
}, false);

// 3️⃣
menuBtn.addEventListener('click', function (e: { target: Element }) {
    console.log(e.target.className); // 'foo'
}, false);
```

1. e.target이 Element라는 것을 알려준다.
2. inline으로 사용한다.
3. 만약에 이벤트의 target 속성만 사용할 경우 이렇게 적어준다.

당연한 말이지만 이벤트의 타입을 지정한 것이 아니기 때문에 `e.type`과 같은 타깃 외에 다른 속성을 사용하면 오류가 발생한다.

### ✨ 해결방법2 : Event의 타입을 지정해준다.

이벤트 자체에 타입을 지정해주면 target이외에 다른 속성도 사용할 수 있다.
물론 타깃은 Element외에 다른 타깃도 받아올 수 있기 때문에 함께 지정해주어야 한다!

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

### ✨ 해결방법3 : EventTarget의 타입을 더 명확하게 지정할 수 있으면 그렇게 해야한다..

예를 들며, form event를 작성해야한다고 가정해보자.
아마 대부분의 사람들은 input의 value를 받아오는 작업을 작성하고 있을 것이다 (= 나👩‍💻)

그때 또 다른 **에러**를 마주하게 될 것이다. 🤬
💻 : `"Property 'value' does not exist on type 'EventTarget'"`

그때는 더 디테일하게 Target의 타입을 지정해주면 된다 😑

```js
const input = document.getElementById('input_elem');

input.addEventListener('input', function (e) {
    console.log((e.target as HTMLInputElement).value);
}, false);
```

- EventTarget의 타입에는 없지만 HTMLInputElement 타입에는 value 속성이 있기 때문에 작동이 된다.

### 그 외에 자주 사용하면 타입 모음

```js
// classList 속성 사용 시
e.target as Element
e.target as HTMLElement


e.target as HTMLImageElement
e.target as HTMLMediaElement
e.target as HTMLVideoElement
e.target as HTMLAudioElement
e.target as HTMLInputElement
e.target as HTMLTextAreaElement

// 이렇게 타입을 지정해 준 후 사용도 가능!
type InputType = HTMLInputElement | HTMLTextAreaElement
e.target as InputType
```

출처: [www.designcise.com](https://www.designcise.com/web/tutorial/how-to-fix-property-does-not-exist-on-type-eventtarget-typescript-error)

```toc

```
