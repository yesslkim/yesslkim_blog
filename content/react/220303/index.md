---
emoji: 😏
title: 리액트 useMemo
date: '2022-03-04 12:05:00'
author: 예슬
tags: 리액트
categories: REACT
---

## useMemo

- Memoization은 동일한 값을 리턴하는 함수가 있을 때, 해당 값을 메모리에 저장해서 필요할 때마다 재사용 하는 것.
- 즉, 자주 사용하는 값을 캐싱하는 것.
- 여기서 알 수 있는 것은 함수 컴포넌트의 경우 렌더링 될 때 모든 내부의 변수가 초기화 되면서 다시 렌더링하게 된다.

```jsx
function Component() {
  const value = calculate(); // 👈 이 경우 함수가 호출되면 다시 렌더링된다.
  const valueMemo = useMemo(() => {
    calculate(), [];
  }); // useMemo로 값을 저장할 수 있음.

  return <div>{value}</div>;
}
```

- **valueMemo**를 보면 `useMemo`의 구조를 알 수 있다.
- 두개의 인자를 가지고 있으며, callback 함수와 의존성 배열을 가지고 있다.
- 의존성 배열을 통해 값을 원하는 순간에만 업데이트 후 다시 저장할 수 있다.
- 하지만 그렇다고 해서 불필요한 값까지 저장하게 된다면 성능저하로 이어질 수 있다
  👉 메모리에 값을 저장하는 것이기 때문
