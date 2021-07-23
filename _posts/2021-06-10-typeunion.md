---
layout: post
title: "[TypeScript] 연산자를 이용한 타입 정의"
subtitle: "연산자를 이용한 타입 정의"
categories: "study"
tags: "type"
---

# Union Type

유니온 타입이란 자바스크립트의 OR 연산자 `||`와 같이 A이거나 B이다 라는 의미의 타입입니다.

```typescript
function logText(text : string || number) {
  // ..
}
```

# Union Type의 장점

```typescript
// any를 사용하는 경우
function getAge(age: any) {
  age.toFixed(); // 에러 발생, age의 타입이 any로 추론되기 때문에 숫자 관련된 API를 작성할 때 코드가 자동 완성되지 않는다.
  return age;
}

// 유니온 타입을 사용하는 경우
function getAge(age: number | string) {
  if (typeof age === "number") {
    age.toFixed();
    return age;
  }
  if (typeof age === "string") {
    return age;
  }

  return new TypeError("age must be number or string");
}
```

<br>

# Intersection Type

인터섹션 타입은 여러 타입을 모두 만족하는 하나의 타입을 의미합니다.

```typescript
interface Person {
  name: string;
  age: number;
}

interface Developer {
  name: string;
  skill: number;
}

type Capt = Person & Developer;
```

위 코드는 Person 인터페이스의 타입 정의와 Developer 인터페이스의 타입 정의를 & 연산자를 이용하여 합친 후 Capt 이라는 타입에 할당한 코드입니다. 결과적으로 Capt의 타입은 아래와 같이 정의됩니다.

```typescript
{
  name: string;
  age: number;
  skill: string;
}
```
