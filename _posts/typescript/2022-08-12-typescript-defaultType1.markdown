---
layout: post
title: "[TypeScript] 기본 타입(1)"
date: 2022-08-12
description: TypeScript 기본 타입(1)
sidebar:
  nav: "docs"
---

타입 스크립트에서 사용하는 타입 중 string, number, boolean, undefined, null 타입에 대해 알아보자.
<br>
TypeScript 는 단지 타입만 지정해주는 것으로 JavaScript 와 사용법이 동일하다 생각하면 된다.
<br>
JavaScript 에서 아주 흔하게 사용되는 3가지의 원시 타입인 string, number, boolean 에 대해 먼저 배워보자.
<br>

## 문자열 (String)

기본적으로 JavaScript 에서 사용하는 것과 마잔가지로 큰 따옴표, 작은 따옴표, 백 틱도 사용할 수 있다.

```
let str: string = "Hello World!";
str = "Hello TS";

const blog = "mine-it-record";
str = `Hello, my ${blog} blog`;
```

<br>

## 숫자 (Number)

JavaScript 와 마찬가지로 TypeScript 역시 모든 숫자든 부동 소수 값이다.

```
let num: number = 6;
num = 7;
num = Number("8");
```

<br>

## 불리언 (Boolean)

기본적으로 null 과 undefined 는 모든 타입의 하위 타입으로 number 같은 타입에 할당할 수 있는데, --strictNullChecks (tsconfig.json 이나 jsconfig.json 파일에 설정하거나, 기본적으로 VSCode 설정 탭에서 설정이 가능하다.) 를 사용하게 되면 null 과 undefined 는 오직 any 타입과 각자 자신들 타입에만 할당이 가능하다. 예외로 undefined 는 void 에 할당이 가능하다.

```
// 이 밖에 이 변수들에 할당할 수 있는 값이 없어 사용하지 않는다.
let u: undefined = undefined;
let n: null = null;

// 보통 이런식으로 사용된다.
let num: number | undefined;
let str: string | null;
```

추가적으로 strictNullChecks 옵션을 설정하는 것을 항상 권장하기도 하며 저렇게 유니온 타입을 통해 undefined 와 null 을 넣어주었다면 코드의 안정성을 위해 항상 체크해줘야 한다.

```
// 단순 체크
function doSomething(x: string | undefined) {
  if (x === undefined) {
    // 아무 것도 하지 않는다.
  } else {
    console.log("Hello, " + x.toUpperCase());
  }
}

// 접미사 (!) 사용
function liveDangerously(x?: number | undefined) {
  // 오류 없음
  console.log(x!.toFixed());
}
```

저렇게 두 가지 방법이 있는데, 아래에 접미사 느낌표를 사용한 예제를 보면 코드가 참 간결해 보이겠지만 저 느낌표는 해당 값은 null 이나 undefined 가 절대 들어올 리 없다라는 것을 명시해주는 것이기 때문에 사실상 사용을 권장하지 않는다.