# ES2015(ES6) - ES2022(ES13)

## ES2022 (ES13)

1. [ES2022: Top level await operator](#Top-Level-await-operator)
2. [ES2022: Private fields and method declaration](#Private-fields-and-method-declaration)
3. [ES2022: Static class field & private static methods](#static-class-field--private-static-methods)
4. [ES2022: Method .at() for indexing](<#method-at()-for-indexing>)
5. [ES2022: Object.hasOwn()](<#ObjecthasOwn()>)

# ES2022 What's New?

## Top Level await operator

-   async 없이 await 사용 가능.
-   최상위 모듈에서도 사용 가능.

```javascript
---
// Example 1
const res = await fetch("<https://swapi.dev/api/people/1/>");
const person = res.text();

// Example 2
import { getUser } from "./api/User";
const user = await getUser();

// Example 3
let users;

if (userType === "ADMIN") {
    users = await import("https://example.com/users/1");
} else {
    users = await import("https://example.com/users/2");
}
---
```

## Private fields and method declaration

-   해시('#') 접두사를 붙여 private 필드/메소드로 사용.
-   Typescript 에서는 선언과 동시에 사용시 초기화 필요.

```javascript
---
class MyClass {
    #field1: number; // Property '#field1' has no initializer and is not definitely assigned in the constructor.
    #field2: number = 10;
    #method = () => {
        return this.#field2;
    };
}
---
```

## Static class field & private static methods

-   해시('#') 접두사를 붙여 private 필드/메소드로 사용.
-   static 필드는 선언후 초기화 하지 않아도 됨 (초기값: undefined)
-   인스턴스는 static 필드/메소드를 억세스 할 수 없음.

```javascript
---
class MyClass {
    static field1: number;
    static field2: number = 10;
    static #method = () => {
        return this.#field2;
    };
}
---
```

## Method .at() for indexing

```javascript
---
const list = [1, 2, 3, 4, 5];

console.log(list.at(-6)); // undefined
console.log(list.at(-1)); // 5
console.log(list.at(0)); // 1
console.log(list.at(1)); // 2
---
```

## Object.hasOwn()

-   객체에 속성이 있으면 true

```javascript
---
const student = {
    name: "Mark",
    age: 18,
};
console.log(Object.hasOwn(student, "age")); // true
console.log(Object.hasOwn(student, "grade")); // false
---
```

-   tsconfig.json 설정 필요

```
{
  "compilerOptions": {
    ...
    "lib": ["es2022"], /* Specify a set of bundled library declaration files that describe the target runtime environment. */
    ...
  }
}
```

# ES2021 What's New?

## 1. String.prototype.replaceAll()

-   정규식에 g 옵션을 통해 전역으로 변경했었던 방법에서 replaceAll 사용으로 간단해졌다.

```javascript
---
'hello world'.replace(/l/g, 'L');   // heLLo worLd
'hello world'.replaceAll('l', 'L'); // heLLo worLd
---
```

## 2. Promise.any()

-   Promises를 인자값으로 받고 Promise중 하나라도 성공하면 해당 Promise를 반환한다. (OR 조건)
    > Promise.any([promises])
-   iterable 객체의 Promise가 모두 실패하면 실패한 Promise가 반환된다.
-   Promise.all()은 주어진 Promise가 모두 Resolve 되어야 한다. (AND 조건)

```javascript
---
const promise1 = Promise.reject(0);
const promise2 = new Promise((resolve) => setTimeout(resolve, 500, 'quick'));
const promise3 = new Promise((resolve) => setTimeout(resolve, 100, 'slow'));

const promises = [promise1, promise2, promise3];

Promise.any(promises).then((value) => console.log(value));
---
```

## 3. Logical assignment operators (논리 할당 연산자)

```javascript
---
// before
obj.prop = obj.prop || foo(); // obj.prop이 잘못된 값일 경우 할당
obj.prop = obj.prop && foo(); // obj.prop이 올바른 값일 경우 할당
obj.prop = obj.prop ?? foo(); // obj.prop이 null이나 undefined일 경우 할당

// after
obj.prop ||= foo();
obj.prop &&= foo();
obj.prop ??= foo();
---
```

## 4. Numeric separators (숫자 구분 기호)

```javascript
---
// before
10000000000 // 100억
// after
10_000_000_000 // 100억
console.log(10_000_000_000); // 10000000000
---
```
