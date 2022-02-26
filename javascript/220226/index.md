---
emoji: 🧚‍♀️
title: offsetWidth vs clientWidth vs getBoundingClientRect()
date: '2022-02-26 15:12:00'
author: 예슬
tags: 자바스크립트
categories: JAVASCRIPT
---

**해당 게시글은 width를 기준으로 작성되었습니다 👩‍🎨**

## 1. offsetWidth vs clientWidth의 차이

- `offsetWidth`는 border까지 포함한 길이를 뜻한다.
  ![offsetWidth 설명사진](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Determining_the_dimensions_of_elements/dimensions-offset.png)

- `clientWidth`는 컨텐츠 크기를 기준으로 한다. (padding 포함)
- 그림에서도 볼 수 있지만 스크롤바는 포함되지 않는다.
  ![clientWidth 설명사진](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Determining_the_dimensions_of_elements/dimensions-client.png)

## 2. (offsetWidth vs clientWidth) vs getBoundingClientRect()의 차이

### 💡 2.1 getBoundingClientRect()은 많은 일을 해!

- 우선 getBoundingClientRect() 메서드는 `DOMRect` 객체를 리턴한다. 이는 엘리먼트의 사이즈와 뷰포트를 기준으로 한 엘리먼트의 위치를 반환한다.
- getBoundingClientRect()으로 리턴 받을 수 있는 값 : `x`/`left`, `y`/`top`, `right`, `bottom`, `width`, `height`
  ![getBoundingClientRect()메서드 설명](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect/element-box-diagram.png)

- 여기서 `width`와 `height`는 offsetWidth와 일치한다. 즉 padding, border까지 포함한 값이다.

### 📍 2.2 `box-sizing`을 주의하자!

예시) `width: 100px; padding: 10px; border: 2px solid #000;`인 경우
| | `clientWidth` | `offsetWidth` | `getBoundingClientRect().width` |
|--- |--- |--- |--- |
| `content-box` | 120px | 124px | 123.999..px |
| `border-box` | 96px | 100px | 99.999...px |

1. `content-box`는 오직 `width`의 기준
   즉, `clientWidth`는 padding까지 포함이기 때문에 width + padding x 2이며, `offsetWidth`과 `getBoundingClientRect().width`는 border까지 포함해야하기 때문에 width + padding x 2 + border x 2가 된다.

2. `border-box`의 기준은 width+padding+border를 포함.
   즉, `clientWidth`는 border를 포함해야하지 않기 때문에 border를 빼준 값이며, `offsetWidth`과 `getBoundingClientRect().width`는 모두 포함해야하기 때문에 width값을 그대로 사용하면 된다.

너무나도 길어졌는데 주로 `box-sizing: border-box`를 하는 경우가 많기 때문에 우리가 생각하는 `width`를 구하기 위해서는 **`offsetWidth`** 과 **`getBoundingClientRect().width`**를 사용하는게 맞다.

### 😫 2.3 그럼 `offsetWidth`과 `getBoundingClientRect().width`의 차이는 대체 뭐야?

아마 2.1과 2.2를 읽은 사람이라면 `clientWidth`와 `getBoundingClientRect().width`의 차이는 알았을 것이다. 근데 `offsetWidth`과 `getBoundingClientRect().width`의 차이는?...😥

결론을 말하자면 둘의 값은 같다! **다만 다른 CSS 속성이 width를 변화시키지 않는다면 말이다**

예를 들어, 해당 속성을 가진 박스가 있다고 가정해보자

```css
.box {
  width: 100px;
  height: 100px;
  transform: scale(0.5);
}
```

결론부터 말하자면
`clientWidth` = 100px
`offsetWidth` = 100px
`getBoundingClientRect().width` = 49.999...px

**즉 `getBoundingClientRect().width`은 렌더링 된 `width`를 반환하기 때문에, `transform`이 적용된 값을 리턴한다.**

### 😜 2.4 내가 지어보는 결론

1. 소수점 없는 정수를 원한다: `offsetWidth` `clientWidth`
2. CSS 살펴보기 싫고 최종 `width`값을 원한다: `getBoundingClientRect().width`
3. `box-sizing: border-box` 일 때 우리가 원하는 그 `width`값:
   `offsetWidth` `getBoundingClientRect().width`

- 여기서 말하는 그 `width`값은 width+padding+border를 모두 포함한 값을 일컫는다.

출처 1: [MDN - Determining the dimensions of elements](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Determining_the_dimensions_of_elements)
출처 2: [MDN - Element.getBoundingClientRect()](https://developer.mozilla.org/en-US/docs/Web/API/Element/getBoundingClientRect)
