---
layout: post
title: "[TypeScript] 리터럴 타입"
date: 2024-06-09
description: TypeScript 리터럴 타입
---

리터럴 타입 (Literal Type) 은 정확한 타입으로 string, number 두 가지가 있으며, 문자열이나 숫자에 정확한 값을 지정할 수 있다.
<br>

#### 문자형 리터럴 타입 (String Literal Type)
```typescript
let string_literal :"hi" | "hello";

console.log(string_literal = "hi");
console.log(string_literal = "hello1"); // Error
```
<br>

#### 숫자형 리터럴 타입 (Numeric Literal Type)
```typescript
type Grade = 1 | 2 | 3;

const student1: Grade = 1;
const student2: Grade = 5;  // Error
```
<br>

#### 리터럴 타입 좁히기 (Literal Narrowing)
`var` 또는 `let` 으로 변수를 선언할 경우 이 변수의 값이 변경될 수 있음을 컴파일러에게 알리는 반면, `const` 로 변수를 선언하게 되면 이 객체는 절대 변경되지 않음을 알린다.
```typescript
// TypeScript는 문자형이 아닌 "Hello World" 로 타입을 정함
const helloWorld = "Hello World";

// 반면, let 은 변경될 수 있으므로 컴파일러는 문자형이라고 선언
let hiWorld = "Hi World";
```
무한한 수의 잠재적 케이스들을 유한한 수의 잠재적 케이스로 줄여나가는 것을 타입 좁히기 (narrowing) 이라 한다.