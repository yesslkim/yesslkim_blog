---
emoji: 📦
title: 리액트 라이브러리 모음
date: '2022-02-26 15:12:00'
author: 예슬
tags: 리액트
categories: REACT
---

## 1. react-custom-scrollbars

- 이름처럼 스크롤바를 간단하게 바꿔주는 라이브러리
- 첫 doc에는 생각보다 자세하게 안나와있는데 v2 doc에 자세하게 나와있다.
- 스크롤과 스크롤바를 커스텀하기 위해서는 track, thumb의 기존 props를 받은다음 커스텀하는 방법이 있는데 document가 깊숙하게 숨겨 있어서 가져와봤다.

```js
import { Scrollbars } from 'react-custom-scrollbars-2';

class CustomScrollbars extends Component {
  render() {
    return (
      <Scrollbars
        renderTrackHorizontal={props => <div {...props} className="track-horizontal"/>}
        renderTrackVertical={props => <div {...props} className="track-vertical"/>}
        renderThumbHorizontal={props => <div {...props} className="thumb-horizontal"/>}
        renderThumbVertical={props => <div {...props} className="thumb-vertical"/>}
        renderView={props => <div {...props} className="view"/>}>
        {this.props.children}
      </Scrollbars>
    );
  }
}

// function component로 내가 다시 작성한 것.
const CustomScrollbars = () => {
  render() {
    return (
      <Scrollbars
        renderTrackHorizontal={props => <div {...props} className="track-horizontal"/>}
        renderTrackVertical={props => <div {...props} className="track-vertical"/>}
        renderThumbHorizontal={props => <div {...props} className="thumb-horizontal"/>}
        renderThumbVertical={props => <div {...props} className="thumb-vertical"/>}
        renderView={props => <div {...props} className="view"/>}>
        {this.props.children}
      </Scrollbars>
    );
  }
}
export default CustomScrollbars;
```

- 여기서 중요한 것은 clasName을 똑같이 작성해줘야 기존에 라이브러리가 지정한 기본 스타일을 변경할 수 있다!

출처 : [react-custom-scrollbars](https://github.com/malte-wessel/react-custom-scrollbars)
출처2 : [react-custom-scrollbars-2](https://github.com/RobPethick/react-custom-scrollbars-2)

## 2. react-scrollmagic

- 아마 대부분 리액트로 프로젝트를 변경하면서 제이쿼리에서 스크롤 애니메이션을 사용할 때 자주 사용하는 라이브러리 일 것이다. 스크롤 매직은 리액트에서도 사용할 수 있다!
- 사용방법은 너무 간단하다. 오히려 제이쿼리로 사용했을 때보다 더 직관적인거 같기도하다 😘

```jsx
import React from 'react';
import { Controller, Scene } from 'react-scrollmagic';

const scrollMagic = () => {
  // scene 부분에 원하는 property를 작성하면 된다.
  return (
    <div>
      <Controller>
        <Scene duration={600} pin>
          <div>Sticky Example</div>
        </Scene>
      </Controller>
    </div>
  );
};
```

- 해당 라이브러리의 유일한 단점은 `useRef()`를 controller 안에 사용할 수 없다는 것이다. 그건 scene에 `triggerElement`를 작성하고 최대한 controller가 포함하는 부분이 적도록 만들어 주면 된다.

**혹시 다른 방법이 있다면 댓글로 남겨주세요 👧**

출처: [react-scrollmagic](https://www.npmjs.com/package/react-scrollmagic)

## 3. 계속 추가 예정 ~ 👩‍🦰

```toc

```
