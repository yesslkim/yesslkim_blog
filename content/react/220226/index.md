---
emoji: ๐ฆ
title: ๋ฆฌ์กํธ ๋ผ์ด๋ธ๋ฌ๋ฆฌ ๋ชจ์
date: '2022-02-26 16:00:00'
author: ์์ฌ
tags: ๋ฆฌ์กํธ
categories: REACT
---

## 1. react-custom-scrollbars

- ์ด๋ฆ์ฒ๋ผ ์คํฌ๋กค๋ฐ๋ฅผ ๊ฐ๋จํ๊ฒ ๋ฐ๊ฟ์ฃผ๋ ๋ผ์ด๋ธ๋ฌ๋ฆฌ
- ์ฒซ doc์๋ ์๊ฐ๋ณด๋ค ์์ธํ๊ฒ ์๋์์๋๋ฐ v2 doc์ ์์ธํ๊ฒ ๋์์๋ค.
- ์คํฌ๋กค๊ณผ ์คํฌ๋กค๋ฐ๋ฅผ ์ปค์คํํ๊ธฐ ์ํด์๋ track, thumb์ ๊ธฐ์กด props๋ฅผ ๋ฐ์๋ค์ ์ปค์คํํ๋ ๋ฐฉ๋ฒ์ด ์๋๋ฐ document๊ฐ ๊น์ํ๊ฒ ์จ๊ฒจ ์์ด์ ๊ฐ์ ธ์๋ดค๋ค.

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

// function component๋ก ๋ด๊ฐ ๋ค์ ์์ฑํ ๊ฒ.
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

- ์ฌ๊ธฐ์ ์ค์ํ ๊ฒ์ clasName์ ๋๊ฐ์ด ์์ฑํด์ค์ผ ๊ธฐ์กด์ ๋ผ์ด๋ธ๋ฌ๋ฆฌ๊ฐ ์ง์ ํ ๊ธฐ๋ณธ ์คํ์ผ์ ๋ณ๊ฒฝํ  ์ ์๋ค!

์ถ์ฒ : [react-custom-scrollbars](https://github.com/malte-wessel/react-custom-scrollbars)
์ถ์ฒ2 : [react-custom-scrollbars-2](https://github.com/RobPethick/react-custom-scrollbars-2)

## 2. react-scrollmagic

- ์๋ง ๋๋ถ๋ถ ๋ฆฌ์กํธ๋ก ํ๋ก์ ํธ๋ฅผ ๋ณ๊ฒฝํ๋ฉด์ ์ ์ด์ฟผ๋ฆฌ์์ ์คํฌ๋กค ์ ๋๋ฉ์ด์์ ์ฌ์ฉํ  ๋ ์์ฃผ ์ฌ์ฉํ๋ ๋ผ์ด๋ธ๋ฌ๋ฆฌ ์ผ ๊ฒ์ด๋ค. ์คํฌ๋กค ๋งค์ง์ ๋ฆฌ์กํธ์์๋ ์ฌ์ฉํ  ์ ์๋ค!
- ์ฌ์ฉ๋ฐฉ๋ฒ์ ๋๋ฌด ๊ฐ๋จํ๋ค. ์คํ๋ ค ์ ์ด์ฟผ๋ฆฌ๋ก ์ฌ์ฉํ์ ๋๋ณด๋ค ๋ ์ง๊ด์ ์ธ๊ฑฐ ๊ฐ๊ธฐ๋ํ๋ค ๐

```jsx
import React from 'react';
import { Controller, Scene } from 'react-scrollmagic';

const scrollMagic = () => {
  // scene ๋ถ๋ถ์ ์ํ๋ property๋ฅผ ์์ฑํ๋ฉด ๋๋ค.
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

- ํด๋น ๋ผ์ด๋ธ๋ฌ๋ฆฌ์ ์ ์ผํ ๋จ์ ์ `useRef()`๋ฅผ controller ์์ ์ฌ์ฉํ  ์ ์๋ค๋ ๊ฒ์ด๋ค. ๊ทธ๊ฑด scene์ `triggerElement`๋ฅผ ์์ฑํ๊ณ  ์ต๋ํ controller๊ฐ ํฌํจํ๋ ๋ถ๋ถ์ด ์ ๋๋ก ๋ง๋ค์ด ์ฃผ๋ฉด ๋๋ค.

**ํน์ ๋ค๋ฅธ ๋ฐฉ๋ฒ์ด ์๋ค๋ฉด ๋๊ธ๋ก ๋จ๊ฒจ์ฃผ์ธ์ ๐ง**

์ถ์ฒ: [react-scrollmagic](https://www.npmjs.com/package/react-scrollmagic)

## 3. ๊ณ์ ์ถ๊ฐ ์์  ~ ๐ฉโ๐ฆฐ

```toc

```
