---
layout: post
title: "[TypeScript] Interface"
subtitle: "Interface"
categories: "study"
tags: "type"
---

인터페이스는 상호 간에 정의한 약속 혹은 규칙을 의미합니다. 타입스크립트에서의 인터페이스는 보통 다음과 같은 범주에 대해 약속을 정의할 수 있습니다.

- 객체의 스펙(속성과 속성의 타입)
- 함수의 매개변수
- 함수의 스펙(매개변수, 반환 타입 등)
- 배열과 객체를 접근하는 방식
- 클래스

# 인터페이스 맛보기

인터페이스 대해 예제를 만들어 보겠습니다.

```typescript
let person = { name: "Cat", age: 3 };

function logAge(obj: { age: number }) {
  console.log(obj.age);
}

let person = { name: "Capt", age: 28 };
logAge(person);
```

만약 인터페이스를 적용한다면

```typescript
interface personAge {
  age: number;
}

function logAge(obj: personAge) {
  console.log(obj.age);
}

let person = { name: "Capt", age: 28 };
logAge(person);
```

<br>

# 옵션 속성

인터페이스를 사용할 때 인터페이스에 정의되어 있는 속성을 모두 다 꼭 사용하지 않아도 됩니다. 이를 옵션 속성이라고 합니다.

```typescript
interface 인터페이스_이름 {
  속성?: 타입;
}
```

예시를 들어보면

```typescript
interface CraftBeer {
  name: string;
  hop: number;
}

let myBeer = {
  name: "Saporo",
};

function brewBeer(beer: CraftBeer) {
  console.log(beer.name); // Saporo
}

brewBeer(myBeer);
```

<br>

# 옵션 속성의 장점

옵션 속성의 장점은 단순히 인터페이스를 사용할 때 속성을 선택적으로 적용할 수 있다는 것 뿐만 아니라 인터페이스에 정의되어 있지 않은 속성에 대해서 인지시켜줄 수 있다는 점입니다.

```typescript
interface CraftBeer {
  name: string;
  hop?: number;
}

let myBeer = {
  name: "Saporo",
};

function brewBeer(beer: Craftbeer) {
  console.log(beer.brewery); // Error: Property 'brewery' does not exist on type 'Beer'
}
brewBeer(myBeer);
```

위에 보시는 것처럼 인터페이스에 정의되어 있지 않은 속성에 대해서 오류를 표시합니다.

<br>

# 읽기 전용 속성

읽기 전용 속성은 인터페이스로 객체를 처음 생성할 때만 값을 할당하고 그 이후에는 변경할 수 없는 속성을 의미합니다.

```typescript
interface CraftBeer {
  readonly brand: string;
}
```

인터페이스로 객체를 선언하고 나서 수정하려고 하면 아래와 같이 에러가 납니다.

```typescript
let myBeer: CraftBeer = {
  brand: "MM",
};

myBeer.brand = "KK"; // error
```

<br>

# 읽기 전용 배열

배열을 선언할 때 `ReadonlyArray<T>` 타입을 사용하면 읽기 전용 배열을 생성할 수 있습니다.

```typescript
let arr: ReadonlyArray<number> = [1, 2, 3];
arr.splice(0, 1); // error
arr.push(4); // error
arr[0] = 100; // error
arr = [10, 20, 30]; // error
```

<br>

# 객체 선언과 관련된 타입 체킹

타입스크립트는 인터레이스를 이용하여 객체를 선언할 때 좀 더 엄밀한 속성 검사를 진행합니다.

```typescript
interface CraftBeer {
  brand?: string;
}

function brewBeer(beer: CraftBeer) {
  // ...
}

brewBeer({ brandon: "what" }); // error: Object literal may only specify known properties, but 'brandon' does not exist in type 'CraftBeer'. Did you mean to write 'brand'?
```

이러한 타입 타입 추론을 무시하고 싶다면 아래와 같이 선언합니다.

```typescript
let myBeer = { brandon: "what" };
brewBeer(myBeer as CraftBeer);
```

만약 인터페이스에 정의하지 않은 속성들을 추가로 사용하고 싶을 때는 아래와 같은 방법을 사용합니다.

```typescript
interface CraftBeer {
  brand?: string;
  [propName: string]: any;
}
```

<br>

# 함수 타입

인터페이스는 함수의 타입을 정의할 때에도 사용할 수 있습니다.

```typescript
interface login {
  (username: string, password: string): boolean;
}
```

함수 인자의 타입과 반환 값의 타입을 정합니다.

```typescript
let loginUser: login;
loginUser = function (id: string, pw: string) {
  console.log("로그인 했습니다");
  return true;
};
```

<br>

# 클래스 타입

쿨래스가 일정 조건을 만족하도록 타입 규칙을 정할 수 있습니다.

```typescript
interface CraftBeer {
  beerName: string;
  nameBeer(beer: string): void;
}

class myBeer implements CraftBeer {
  beerName: string = "Baba";
  nameBeer(b: string) {
    this.beerName = b;
  }
  constructor() {}
}
```

<br>

# 인터페이스 확장

```typescript
interface Person {
  name: string;
}

interface Developer extends Person {
  skill: string;
}

let fe = {} as Developer;
fe.name = "josh";
ge.skill = "Type";
```

<br>

# 하이브리드 타입

자바스크립트의 유연하고 동적인 타입 특성에 따라 인터페이스 역시 여러가지 타입을 조합하여 만들 수 있습니다.

```typescript
interface CraftBeer {
  (beer: string): string;
  brand: string;
  brew(): void;
}

function myBeer(): CraftBeer {
  let my = function (beer: string) {} as CraftBeer;
  my.brand = "Beer Kitchen";
  my.brew = function () {};
  return my;
}

let brewedBeer = myBeer();
brewedBeer("My First Beer");
brewedBeer.brand = "Pangyo Craft";
brewedBeer.brew();
```
