---
layout: post
title: "[TypeScript] Generics"
subtitle: "Generics"
categories: "study"
tags: "type"
---

제네릭이란 타입을 마치 함수의 파라미터 처럼 사용하는 것을 의미합니다.

```typescript
function getText(text) {
  return text;
}
```

위 함수는 `text` 라는 파라미터에 값을 넘겨 받아 `text`를 반환합니다. 어떤 값이 들어가더라도 그대로 반환합니다.

```typescript
getText("hi"); // 'hi'
getText(10); // 10
getText(true); // true
```

이제 제네릭을 한번 살펴보면

```typescript
function getText<T>(text: T): T {
  return text;
}
```

위 함수는 제네릭 기본 문법이 적용된 형태입니다. 이제 함수를 호출할 때 아래와 같이 함수 안에서 사용할 타입을 넘겨줄 수 있습니다.

```typescript
getText<string>("hi");
getText<number>(10);
getText<boolean>(true);
```

<br>

# 제네릭을 사용하는 이유

```typescript
function logText(text: string): string {
  return text;
}
```

위 코드는 인자를 하나 넘겨 받아 반환하는 함수입니다. 만약 여러가지 타입을 허용하고 싶다면 아래와 같이 `any`를 사용할 수 있습니다.

```typescript
function logText(text: any): any {
  return text;
}
```

이렇게 코드를 작성하면 함수의 인자로 어떤 타입이 들어갔고 어떤 값이 반화되는지를 알 수 없습니다. 왜냐면 `any`라는 타입은 검사를 하지 않기 때문입니다.

이러한 문제점을 해결할 수 있는 방법이 바로 제네릭 입니다.

```typescript
function logText<T>(text: T): T {
  return text;
}
```

이렇게 선언한 함수는 다음과 같이 2가지 방법으로 호출할 수 있습니다.

```typescript
// #1
const text = logText<string>("Hello");

// #2
const text = logText("Hello");
```

<br>

# 제네릭 타입 변수

앞에서 설명한 대로 제네릭을 사용하기 시작하면 컴파일러에서 인자에 타입을 넣어달라는 경고를 볼 수 있습니다.

조금 전 코드를 다시 보면

```typescript
function logText<T>(text: T): T {
  return text;
}
```

만약 여기서 함수의 인자로 받은 값의 `length`를 확인하고 싶다면 어떻게 해야 할까요? 아마 아래와 같이 코드를 작성하겠죠?

```typescript
function logText<T>(text: T): T {
  console.log(text.length); // Error!! T doesn't have .length
  return text;
}
```

위 코드는 에러를 발생시킵니다. `text`에 `.length`가 있다는 단서는 없기 때문입니다.

이러한 경우에는 다음과 같이 제네릭에 타입을 줄 수 있습니다.

```typescript
function logText<T>(text: Array<T>): Array<T> {
  console.log(text.length);
  return text;
}
```

<br>

# 제네릭 타입

제네릭 인터페이스에 대해 알아보겠습니다. 아래의 두 코드는 같은 의미입니다.

```typescript
function
```
