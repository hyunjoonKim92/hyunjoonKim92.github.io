---
layout: post
title: "[TypeScript] 기본 타입(2)"
date: 2022-08-13
description: TypeScript 기본 타입(2)
---

타입 스크립트에서 사용하는 타입 중 void, never, unknown, any 타입에 대해 알아보자.
<br>

#### Void

void 타입은 보통 함수에서 반환 값이 없을 때 반환 타입을 표현하기 위해 사용된다. 물론 일반 타입 변수로 선언할 수 있으나, 해당 변수에는 undefined 만 할당할 수 있기 때문에 사용하지 않는다.

```typescript
let unusable: void = undefined;
unusable = "record";

// 타입 명시
function warnUser(): void {
    console.log("This is my warning message.");
}

// 생략 시 자동으로 타입이 지정되나
// 보통 반환 값이 없을 때만 생략하고 반환 값이 있으면 타입을 명시해준다.
function voidFunc() {
    console.log("This is my warning message.");
}
```

void 타입은 보통 함수에서만 사용하며 반환 값이 없다는 건 바로 보이기 때문에 생략해주는 경우가 많다.

<br>

#### Never

never 타입은 모든 타입에 할당 가능한 하위 타입이나 본인 외에 다른 타입이 할당될 수 없다.

never 타입은 절대 발생할 수 없는 타입을 나타낸다.

가장 흔한 예제로는 에러를 발생시킬 때 사용된다.

```typescript
function fail(msg: string): never {
    throw new Error(msg);
}
```

<br>

#### Unknown / Any

두 타입을 같이 설명하는 이유는 두 타입 모두 타입을 지정하기 애매할 때 사용하기 때문이다.

Unknown 타입에 대해 알아보자.

unknown 타입은 any 처럼 모든 타입을 넣어도 상관없다라기보다는 '이 변수는 어떤 타입이 될 지 모르니 네가 추론해줘.' 라는 의미와 같다.

```typescript
let str: unknown = "anything";
str = 2;
str = [1, 2, 3];
```

unknown 타입의 변수에는 프로퍼티 접근도 못하고 인스턴스 생성 역시 할 수 없고 항상 타입을 확인해야 한다.


Any 타입에 대해 알아보자.

any 타입은 모든 타입을 할당받을 수 있는 타입이다.

```typescript
let str: any = "anything";
str = 2;
str = [1, 2, 3];
```

하지만 모든 타입을 할당받는다는 의미는 의도치 않은 형 변환이나 다른 타입의 값이 대입되는 등 여러 사이드 이펙트를 발생시킬 수 있다는 의미이다.

그리고 해당 타입의 메서드를 사용할 떄 '타입 표명 (type-assertion)' 을 사용해야하기 때문에 유의하여야 한다.

```typescript
// any 타입 변수 할당
let str: any = "anything";
let test: string = str;

// unkown 타입 변수 할당
let str2: unknown = "unknown";
//let test2: string = str2; // error : 'unknown' 형식은 'string' 형식에 할당할 수 없습니다.
let test2: string = (str2 as string);
str = str2;
```

any 타입은 다른 변수에도 할당이 가능하다. 반면에 unknown 타입의 경우 any 타입을 제외한 나머지 타입 변수에는 타입 표명을 하지않는 이상 할당이 불가능하다.