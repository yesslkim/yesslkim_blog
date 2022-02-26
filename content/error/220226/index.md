---
emoji: 👻
title: Variable 'age' is used before being assigned - Typescript
date: '2022-02-26 18:58:00'
author: 예슬
tags: 타입스크립트
categories: TYPESCRIPT
---

## `let age;` 인데 할당되기 전에 사용되었다고?

예시를 들어보자

```ts
let age: number; // 1️⃣ num이 number type으로 지정됨.

if (isActive) {
  age = 100;
}

console.log(`내 나이는 ${age}살이야`); // 2️⃣ 🤯 ERROR : Variable 'age' is used before being assigned
```

분명 let age로 선언되었는데 왜 저런 에러가 뜰까?
우리는 여기서 알아야 한다. `let age;`는 **할당(assigned)** 된 것이 아니라 **선언(declare)** 된 것이다.

- 여기서 알 수 있는 것은 만약에 if문이 실행되지 않으면 `age`는 선언만 되었을 뿐 할당되지 않았다. 즉 전혀 할당되지 않은 것이다.

### 근데 왜 할당되지 않은 것일까?

해답은 여기있다

```ts
let age: number;
```

우리가 age를 number type으로 지정하였기 때문에 다른 값이 들어오면 에러가 뜨게 된다.

## ✨ 해결 방법

1. undefined 값도 괜찮은 경우 : 초기 값인 undefined도 함께 타입으로 지정해준다.

```ts
let age: number | undefined = undefined;
```

2. 무조건 number 타입으로 지정될 경우 : Definite Assignment Assertions을 사용한다.
   [Definite Assignment Assertions](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-7.html#definite-assignment-assertions)이란 컴파일러에게 값이 무조건 할당되어 있다고 컴파일러에게 전달하는 경우이다. 즉 처음은 `number | undefined`으로 지정되지만 값이 할당되면 number type으로 인지한다.

- 참고로 (!)는 Non-null assertion operator로도 사용된다. 즉 null이 아니라고 단언해줄 때 사용된다.

참고자료: [Definite Assignment Assertions](https://stackoverflow.com/questions/67351411/what-s-the-difference-between-definite-assignment-assertion-and-ambient-declarat)

원문 출처: [Variable 'test' is used before being assigned - Typescript](https://stackoverflow.com/questions/44832316/variable-test-is-used-before-being-assigned-typescript)

```toc

```
