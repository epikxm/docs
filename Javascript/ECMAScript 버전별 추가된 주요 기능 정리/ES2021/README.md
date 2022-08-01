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
