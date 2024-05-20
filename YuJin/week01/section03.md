### 모듈 시스템

**모듈 시스템(Module System)**

: 모듈을 생성하고, 불러오고, 사용하는 등의 모듈을 다루는 다양한 기능을 제공하는 시스템

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/a9c972d9-4bcb-4893-a6f5-f5ab314393de/Untitled.png)

**ES Module(ESM) 사용해 보기**

1. package.json에 코드 추가

```
{
  "name": "section03",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node index.js"
  },
  "author": "",
  "license": "ISC",
  "type" : "module"
}
```

1. 모듈 작성

```jsx
// math 모듈

export function add(a, b) {
    return a + b;
  }
  
export function sub(a, b) {
    return a - b;
  }
  
export default function multiply(a, b) {
    return a * b;
  }
```

1. 사용

```jsx
import mul, { add, sub } from "./math.js";
//default function은 중괄호 없이 불러옴

console.log(add(1, 2));
console.log(sub(1, 2));
console.log(mul(2, 3));
```

### 라이브러리

**라이브러리**

: 프로그램을 개발할 때 다양한 기능들을 미리 만들어 모듈화 해 놓은 것

**라이브러리 모음**

[npm | Home](https://www.npmjs.com/)

예시) randomcolor 라이브러리 설치 

> npm i randomcolor 

```jsx
import mul, { add, sub } from "./math.js";

import randomcolor from "randomcolor";

const color = randomcolor();
console.log(color);

// console.log(add(1, 2));
// console.log(sub(1, 2));
// console.log(mul(2, 3));
```

설치했던 라이브러리 다시 설치 (package.json의 dependency 기준으로 재설치 가능)

> npm i