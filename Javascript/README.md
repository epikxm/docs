# ES2022 What's New?

## Top-level await operations

이제 최상위 모듈에서 async 없이 사용 가능.

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

## Private fields and method declarations

```javascript
enum COLOR { WHITE, BLACK, RED, BLUE };

class Car {
    // '#'키워드를 통해 private 필드를 선언한다.

    #color: COLOR = COLOR.WHITE;
    #power: number = 455;
    #brend: string = '';

    // 변수 선언시 초기화 필수.
    // Property '#model' has no initializer and is not definitely assigned in the constructor.
    #model: string;

    // 더 이상 생성자를 통해 클래스 필드를 생성하지 않아도 된다.
    // constructor () {}

    // '#' 키워드를 통해 private 메소드 선언한다.
    #setBrend = (value: string) => {
        this.#brend = value;
    }

    setModel = (value: string) => {
        this.#model = value;
    }

    getBrean = () => {
        return this.#brend;
    }

    getModel = () => {
        return this.#model;
    }

    getFullName = () => {
        return this.#brend + ' ' + this.#model;
    }
}

const car = new Car();

// private 메소드는 바로 엑세스 불가능하다.
car.setBrend('VOLVO');
car.setModel('XC60 T8 PHEV');

// private 필드는 바로 엑세스 불가능하다.
// Property '#power' is not accessible outside class 'Car' because it has a private identifier.
console.log(car.#power);

console.log(car.getBrean());
console.log(car.getModel());
console.log(car.getFullName());
```
