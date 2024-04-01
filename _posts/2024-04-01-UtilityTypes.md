---
layout: post
title: "[TypeScript] 유틸리티 타입"
subtitle: "유틸리티 타입"
categories: "study"
tags: "type"
---

## Partial<T>

Type의 모든 속성을 optional하게 변경한 새로운 타입을 반환

```typescript
interface User {
  name: string;
  age: number;
  phone: number;
}

type PartialUser = Partial<User>;

// type PartialUser = {
//   name?: string | undefined;
//   age?: number | undefined;
//   phone?: number | undefined;
// };
```

## Required<T>

Type의 모든 속성을 필수로 변경한 새로운 타입을 반환

```typescript
interface User {
  name?: string;
  age?: number;
  phone: number;
}

type Required_User = Required<User>;
/*
type Required_User = {
    name: string;
    age: number;
    phone: number;
}
*/
```

## Record<Key, TYPE>

- 제네릭의 KEY를 속성으로, 제네릭의 TYPE을 속성값의 타입으로 지정하는 새로운 타입을 반환
- {KEY: TYPE, ...} 형태로 반환
- 이 유틸리티는 타입의 프로퍼티들을 다른 타입에 매핑시키는 데 사용

```typescript
type Key = "name" | "age" | "phone";

type Record_User = Record<Key, number>;

/*
type Record_User = {
    name: number;
    age: number;
    phone: number;
}
*/
```

## Pick<TYPE, KEY>

- 제네릭 TYPE으로 부터 제네릭의 KEY에 해당하는 속성을 선택하여 따로 모아 타입을 반환
- 제네릭의 TYPE은 속성을 가지는 인터페이스나 객체 타입

```typescript
interface User {
  name: string;
  age: number;
  email: string;
  isValid: boolean;
}

type Key = "name" | "email";

type Pick_User = Pick<User, Key>;
/*
type Pick_User = {
    name: string;
    email: string;
}
*/
```

## Omit<TYPE,KEY>

- Pick과 반대
- 제네릭의 TYPE으로 부터 제네릭 KEY에 해당하는 속성을 제외한 나머지들을 따로 모아 타입을 반환
- 제네릭 TYPE은 속성을 가지는 인터페이스나 객체 타입

```typescript
interface User {
   name: string;
   age: number;
   email: string;
   isValid: boolean;
}

type Key = 'name' | 'email';

type Omit_User = Omit<User, Key>;
/*
type Omit_User = {
    age: number;
    isValid: boolean;
}

```

출처: https://inpa.tistory.com/entry/TS-📘-타입스크립트-유틸리티-타입-💯-총정리 [Inpa Dev 👨‍💻:티스토리]
