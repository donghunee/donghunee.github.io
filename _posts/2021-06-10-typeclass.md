---
layout: post
title: "[TypeScript] Class"
subtitle: "Class"
categories: "study"
tags: "type"
---

# readonly

클래스의 속성에 `readonly` 키워드를 사용하면 아래와 같이 접근만 가능합니다.

```typescript
class Developer {
  readonly name: string;
  constructor(theName: string) {
    this.name = theName;
  }
}

let john = new Developer("John");
john.name = "John"; // error!! name is readonly
```

다음과 같이 작성할 수 있습니다.

```typescript
class Developer {
  readonly name: string;
  constructor(readonly name: string) {}
}
```

<br>

# Accessor

타입스크립트는 객체의 특정 속성의 접근과 할당에 대해 제어할 수 있습니다. 이를 위해선 해당 객체가 클래스로 생성한 객체여야 합니다.

```typescript
class Developer {
  name: string;
}

const josh = new Developer();
josh.name = "josh Bolton";
```

위 코드는 클래스로 생성한 객체의 `name`속성에 `Josh Bolton` 이라는 값을 대입한 코드입니다. 이제 `josh`라는 객체의 `name` 속성은 `Josh Bolton`이라는 값을 갖습니다.

여기서 만약 `name` 속성에 제약 사항을 추가하고 싶다면 아래와 같이 `get`과 `se`을 활용합니다.

```typescript
class Developer {
  private name: string;

  get name(): string {
    return this.name;
  }

  set name(newValue: string) {
    if (newValue && newValue.length > 5) {
      throw new Error("너무 길어용");
    }
    this.name = newValue;
  }
}

const lee = new Developer();
lee.name = "lee donghun"; // error!
lee.name = "lee";
```

> `get`만 선언하고 `set`을 선언하지 않는 경우에는 자동으로 `readonly`로 인식됩니다.

<br>

# Abstract Class

추상클래스(Abstract Class)는 인터페이스와 비슷한 역할을 하면서도 조금 다른 특징을 갖습니다. 추상 클래스는 특정 클래스의 상속 대상이 되는 클래스이며 좀 더 상위 레벨에서 속성, 메서드의 모양을 정의합니다.

```typescript
abstract class Developer {
  abstract coding(): void;
  drink(): void {
    console.log("drink sth");
  }
}

class FrontEndDeveloper extends Developer {
  coding(): void {
    // Developer 클래스를 상속받은 클래스에서 무조건 정의해야 하는 메서드
  }
  design(): void {
    console.log("design web");
  }
}

const dev = new Developer();
const lee = new FrontEndDeveloper();
```
