# ES2022 What's New?

## 1. Top level await operator

> async 없이 await 사용 가능.  
> 최상위 모듈에서도 사용 가능.  

```javascript
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
```

## 2. Private fields and method declaration

> 해시('#') 접두사를 붙여 private 필드/메소드로 사용.  
> Typescript 에서는 선언과 동시에 사용시 초기화 필요.

```javascript
class MyClass {
	#field1: number; // Property '#field1' has no initializer and is not definitely assigned in the constructor.
	#field2: number = 10;
	#method = () => {
		return this.#field2;
	};
}
```

## 3. Static class field & private static methods

> 해시('#') 접두사를 붙여 private 필드/메소드로 사용.  
> static 필드는 선언후 초기화 하지 않아도 됨 (초기값: undefined)  
> 인스턴스는 static 필드/메소드를 억세스 할 수 없음.  

```javascript
class MyClass {
	static field1: number;
	static field2: number = 10;
	static #method = () => {
		return this.#field2;
	};
}
```
## 4. Method .at() for indexing

## 5. Object.hasOwn()

## 6. error.cause
