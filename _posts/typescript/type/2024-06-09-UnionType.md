---
layout: post
title: "[TypeScript] 유니온 타입"
date: 2024-06-09
description: TypeScript 유니온 타입
---

유니온 타입 (Union Type) 이란 자바스크립트의 OR 연산자 (`||`) 와 같이 A 이거나 B 이다라는 의미의 타입이다.
```typescript
function logText(text: string | number) {
    // ...
}
```
위 함수의 파리미터인 `text` 에는 문자형 타입 또는 숫자형 타입이 모두 올 수 있는데, 이처럼 `|` 연산자를 이용하여 타입을 여러개 연결하는 방식을 유니온 타입의 정의 방식이라 부른다.
<br>

#### 인터섹션 타입 (Intersection Type)
인터섹션 타입 (Intersection Type) 은 여러 타입을 모두 만족하는 하나의 타입을 의미한다.
```typescript
interface Person {
    name: string;
    age: number;
}
interface Developer {
    name: string;
    skill: string;
}

type Capt = Person & Developer;
```
`Persion` 인터페이스의 타입 정의와 `Developer` 인터페이스의 타입 정의를 `&` 연산자를 이용하여 합친 후 `Capt` 이라는 타입에 할당한 코드로 `Capt` 의 타입은 아래와 같이 정의된다.
```typescript
{
    name: string;
    age: number;
    skill: string;
}
```
이처럼 `&` 연산자를 이용해 여러 개의 타입 정의를 하나로 합치는 방식을 인터섹션 타입 정의 방식이라 한다.
<br>

#### 유니온 타입의 장점
`any` 를 사용하는 경우 자바스크립트로 작성하는 것처럼 동작을 하고, 유니온 타입을 사용하면 타입스크립트의 이점을 살려서 코딩할 수 있다.
```typescript
// any 를 사용하는 경우
function getAge(age: any) {
    age.toFixed(); // Error, age 의 타입이 `any` 로 추론되기 때문에 숫자 관련된 API 를 작성할 때 코드가 자동 완성되지 않는다.
    return age;
}

// 유니온 타입을 사용하는 경우
function getAge(age: number | string) {
    if (typeof age === 'number') {
        age.toFixed(); // age 의 타입이 `number` 로 추론되기 때문에 숫자 관련된 API 를 쉽게 자동 완성할 수 있다.
        return age;
    }

    if (typeof age === 'string') {
        return age;
    }

    return new TypeError('age must be number or string');
}
```
<br>

#### 유니온 타입 사용 시 주의할 점
```typescript
interface Person {
    name: string;
    age: number;
}
interface Developer {
    name: string;
    skill: string;
}

function introduce(someone: Person | Developer) {
    someone.name; // O 정상 동작
    someone.age; // X 타입 오류
    someone.skill; // X 타입 오류
}
```
타입스크립트 관점에서 `introduce()` 함수를 호출하는 시점에 `Person` 타입이 올지 `Developer` 타입이 올지 알 수 없기 때문에 어느 타입이 들어오던지 오류가 안나는 방향으로 타입을 추론한다.
<br>
결과적으로 `introduce()` 함수 안에서는 별도의 타입 가드 (Type Guard) 를 이용하여 타입의 범위를 좁히지 않는 이상 기본적으로는 `Person` 과 `Developer` 두 타입에 공통적으로 들어있는 `name` 속성만 접근 가능하다.