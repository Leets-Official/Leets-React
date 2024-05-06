# 1주차

**강의**
[인프런] - 한입 크기로 잘라머는 리액트(React.js) : 기초부터 실전까지
(https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8)

### 범위

섹션 0 ~ 섹션 5

- [ ] 0.  들어가며
- [ ] 1.  Javascript 기본
- [ ] 2.  Javascript 심화

---

</br>

### 학습 내용

# JavaScript 기본

- 변수와 상수
1. 변수

```jsx
let age;

age = 21;
```

1. 상수

```jsx
const birth = "2004.05.31";
```

1. 변수 명명 규칙
    
    3-1. $, _ 제외한 기호는 사용할 수 없다.
    
    ```jsx
    let $_name;
    ```
    
    3-2. 숫자로 시작할 수 없다.
    
    ```jsx
    let name1;
    let $2name;
    ```
    
    3-3. 예약어를 사용할 수 없다.
    
2. 변수 명명 가이드

```jsx
let saleCount = 1;
let refundCount = 1;
let totalSalesCount = salesCount - refundCount;
```

- 자료형
1. Number Type

```jsx
let num1 = 27;
let num2 = 1.5;
let num3 = -20;

let inf = Infinity;
let mInf = -Infinity;

let nan = NaN;
```

1. String Type

```jsx
let myName = "김지원";
let myLocation = "대구";
let introduce = myName + myLocation;

let introduceText = `${name}은 ${myLocation}에 거주합니다.`;
```

1. Boolean Type

```jsx
let isSwitchOn = true;
let isEmpty = false;
```

1. Null Type (아무것도 없다)

```jsx
let empty = null;
```

1. Undefined Type

```jsx
let none;
console.log(none);
```

- 형 변환
1. 묵시적 형 변환
- 자바스크립트 엔진이 알아서 형 변환 하는 것

```jsx
let num = 10;
let str = "20";

const result = num + str;
```

1. 명시적 형 변환 
- 프로그래머 내장함수 등을 이용해서 직접 형 변환을 명시
- 문자열 → 숫자

```jsx
let str1 = "10";
let strToNum1 = Number(str1);

let str2 = "10개";
let strToNum2 = parseInt(str2);
```

- 숫자 → 문자열

```jsx
let num1 = 20;
let numToStr1 = String(num1);

console.log(numToStr1 + "입니다.");
```

- 연산자1
1. 대입 연산자

```jsx
let var1 = 1;
```

1. 산술 연산자

```jsx
let num1 = 3 + 2;
let num2 = 3 - 2;
let num3 = 3 * 2;
let num4 = 3 / 2;
let num5 = 3 % 2;

let num6 = (1 + 2) * 10;
```

1. 복합 대입 연산자

```jsx
let num7 = 10;
num7 += 20;
num7 -= 20;
num7 *= 20;
num7 /= 20;
num7 %= 10;
```

1. 증감 연산자

```jsx
let num8 = 10;
++num8;
num8++;
```

1. 논리 연산자

```jsx
let or = true || false;

let and = true && false;

let not = !true;
```

1. 논리 연산자

```jsx
let comp1 = 1 === "1";
let comp2 = 1 !== 2;

let comp3 = 2 > 1;
let comp4 = 2 < 1;

let comp5 = 2 >= 2;
let comp6 = 2 <= 2;
```

- 연산자2
1. null 병합 연산자
- 존재하는 값을 추려내는 기능
- null, undefined가 아닌 값을 찾아내는 연산

```jsx
let var1;
let var2 = 10;
let var3 = 20;

let var4 = var1 ?? var2;
let var5 = var1 ?? var3;
let var6 = var3 ?? var2;

let userName;
let userNickName = "woneeeee";

let displayName = userName ?? userNickName;
```

1. typeof 연산자
- 값의 타입을 문자열로 반환하는 기능을 하는 연산자

```jsx
let var7 = 1;
var7 = "hello";
var7 = true;

let t1 = typeof var7;
console.log(t1);
```

1. 삼항 연산자
- 항을 3개 사용하는 연산자
- 조건식을 이용해서 참, 거짓일 때의 값을 다르게 반환

```jsx
let var8 = 10;
```

- 요구사항 : 변수 res에 var8의 값이 짝수 → “짝”, 홀수 → “홀”

```jsx
let res = var8 % 2 === 0 ? "짝수" : "홀수";
console.log(res);
```

- 조건문
1. if 조건문 (if문)

```jsx
let num = 4;

if (num >= 10) {
  //   console.log("num은 10 이상입니다");
  //   console.log("조건이 참 입니다!");
} else if (num >= 5) {
  //   console.log("num은 5 이상입니다");
} else if (num >= 3) {
  //   console.log("num은 3 이상입니다");
} else {
  //   console.log("조건이 거짓입니다!");
}
```

1. Switch 문
- if문과 기능 자체는 동일
- 다수의 조건을 처리할 때 if보다 더 직관적

```jsx
let animal = "owl";

switch (animal) {
  case "cat": {
    console.log("고양이");
    break;
  }
  case "dog": {
    console.log("강아지");
    break;
  }
  case "bear": {
    console.log("곰");
    break;
  }
  case "snake": {
    console.log("뱀");
    break;
  }
  case "tiger": {
    console.log("호랑이");
    break;
  }
  default: {
    console.log("그런 동물은 전 모릅니다");
  }
}
```

- 반복문

```jsx
for (let idx = 1; idx <= 10; idx++) {
  if (idx % 2 === 0) {
    continue;
  }
  console.log(idx);

  if (idx >= 5) {
    break;
  }
}
```

- 함수
- 함수

```jsx
let area1 = getArea(10, 20);
console.log(area1);

let area2 = getArea(30, 20);
console.log(area2);

getArea(120, 200);
```

- 호이스팅 → 끌어올리다 라는 뜻

```jsx
function getArea(width, height) {
  function another() {
    // 중첩 함수
    console.log("another");
  }

  another();
  let area = width * height;

  return area;
}
```

- 함수 표현식과 화살표 함수
1. 함수 표현식

```jsx
function funcA() {
  //   console.log("funcA");
}

let varA = funcA;
varA();

let varB = function () {
  //   console.log("funcB");
};

varB();
```

1. 화살표 함수

```jsx
let varC = (value) => {
  console.log(value);
  return value + 1;
};

console.log(varC(10));
```

- 콜백함수
1. 콜백함수

```jsx
function main(value) {
  value();
}

main(() => {
  //   console.log("i am sub");
});

```

1. 콜백함수의 활용

```jsx
function repeat(count, callback) {
  for (let idx = 1; idx <= count; idx++) {
    callback(idx);
  }
}

repeat(5, (idx) => {
  console.log(idx);
});

repeat(5, (idx) => {
  console.log(idx * 2);
});

repeat(5, (idx) => {
  console.log(idx * 3);
});
```

- 스코프
1. 스코프
- 전역(전체 영역) 스코프 / 지역(특정 영역) 스코프
- 전역 스코프 : 전체 영역에서 접근 가능
- 지역 스코프 : 특정 영역에서만 접근 가

```jsx
let a = 1; // 전역 스코프

function funcA() {
  let b = 2; // 지역 스코프
  console.log(a);
}

funcA();

if (true) {
  let c = 1;
}

for (let i = 0; i < 10; i++) {
  let d = 1;
}

funcB();
```

- 객체 1
1. 객체 생성

```jsx
let obj1 = new Object(); // 객체 생성자
let obj2 = {}; // 객체 리터럴 (대부분 사용)
```

1. 객체 프로퍼티 (객체 속성)

```jsx
let person = {
  name: "김지원",
  age: 21,
  hobby: "음악 감상",
  job: "FE Developer",
  extra: {},
  10: 20,
  "like dog": true,
};
```

1. 객체 프로퍼티를 다루는 방법
    
    3-1. 특정 프로퍼티에 접근 (점 표기법, 괄호 표기법)
    
    ```jsx
    let name = person.name;
    let age = person["age2"];
    
    let property = "hobby";
    let hobby = person[property];
    ```
    
    3-2. 새로운 프로퍼티를 추가하는 방법
    
    ```jsx
    person.job = "fe developer";
    person["favoriteFood"] = "떡볶이";
    ```
    
    3-3. 프로퍼티를 수정하는 법
    
    ```jsx
    person.job = "student";
    person["favoriteFood"] = "초콜릿";
    ```
    
    3-4. 프로퍼티를 삭제하는 방법
    
    ```jsx
    delete person.job;
    delete person["favoriteFood"];
    ```
    
    3-5. 프로퍼티의 존재 유무를 확인하는 방법 (in 연산자)
    
    ```jsx
    let result1 = "name" in person;
    let result2 = "cat" in person;
    console.log(result2);
    ```
    
- 객체 2
1. 상수 객체

```jsx
const animal = {
  type: "고양이",
  name: "나비",
  color: "black",
};

animal.age = 2; // 추가
animal.name = "까망이"; // 수정
delete animal.color; // 삭제
```

1. 메서드
- 값이 함수의 프로퍼티를 말함

```jsx
const person = {
name: "김지원",
// 메서드 선언
sayHi() {
console.log("안녕!");
},
};

person.sayHi();
person["sayHi"](https://www.notion.so/eb85b4204e5048be9802f559f3ed97e5?pvs=21);
```

- 배열
1. 배열 생성

```jsx
let arrA = new Array(); // 배열 생성자
let arrB = []; // 배열 리터럴 (대부분 사용)

let arrC = [
  1,
  2,
  3,
  true,
  "hello",
  null,
  undefined,
  () => {},
  {},
  [],
];
```

1. 배열 요소 접근

```jsx
let item1 = arrC[0];
let item2 = arrC[1];

arrC[0] = "hello";
console.log(arrC);
```

# JavaScript 심화

- Truthy와 Falsy
1. Falsy한 값

```jsx
let f1 = undefined;
let f2 = null;
let f3 = 0;
let f4 = -0;
let f5 = NaN;
let f6 = "";
let f7 = 0n;
```

1. Truty한 값
- 7가지 Falsy 한 값들 제외한 나머지 모든 값

```jsx
let t1 = "hello";
let t2 = 123;
let t3 = [];
let t4 = {};
let t5 = () => {};
```

1. 활용 사례

```jsx
function printName(person) {
  if (!person) {
    console.log("person의 값이 없음");
    return;
  }
  console.log(person.name);
}

let person = { name: "김지원" };
printName(person);
```

- 단락 평가
1. 단락 평가 활용 사례

```jsx
function printName(person) {
  const name = person && person.name;
  console.log(name || "person의 값이 없음");
}

printName();
printName({ name: "김지원" });
```

- 구조 분해 할당
1. 배열의 구조 분해 할당

```jsx
let arr = [1, 2, 3];

let [one, two, three, four = 4] = arr;
```

1. 객체의 구조 분해 할당

```jsx
let person = {
  name: "김지원",
  age: 21,
  hobby: "음악 감상",
};

let {
  age: myAge,
  hobby,
  name,
  extra = "hello",
} = person;
```

1. 객체 구조 분해 할당을 이용해서 함수의 매개변수를 받는 방법

```jsx
const func = ({ name, age, hobby, extra }) => {
  console.log(name, age, hobby, extra);
};

func(person);
```

- Spread 연산자와 Rest 매개변수
1. Spread 연산자
- Spread : 흩뿌리다, 펼치다 라는 뜻
- 객체나 배열에 저장된 여러 개의 값을 개별로 흩뿌려주는 역할

```jsx
let arr1 = [1, 2, 3];
let arr2 = [4, ...arr1, 5, 6];

let obj1 = {
  a: 1,
  b: 2,
};
let obj2 = {
  ...obj1,
  c: 3,
  d: 4,
};

function funcA(p1, p2, p3) {
  //   console.log(p1, p2, p3);
}

funcA(...arr1);
```

1. Rest 매개 변수
- Rest는 나머지, 나머지 매개변수

```jsx
function funcB(one, two, ...ds) {
  console.log(ds);
}

funcB(...arr1);
```

- 반복문으로 배열과 객체 순회하기
1. 배열 순회

```jsx
let arr = [1, 2, 3];
```

1-1 배열 인덱스

```jsx
for (let i = 0; i < arr.length; i++) {
  //   console.log(arr[i]);
}

let arr2 = [4, 5, 6, 7, 8];
for (let i = 0; i < arr2.length; i++) {
  //   console.log(arr2[i]);
}
```

1-2. for of 반복문

```jsx
for (let item of arr) {
  //   console.log(item);
}
```

1. 객체 순회

```jsx
let person = {
  name: "김지원",
  age: 21,
  hobby: "음악 감상",
};
```

2-1. Object.keys 사용

- 객체에서 key 값들만 뽑아서 새로운 배열로 반환

```jsx
let keys = Object.keys(person);

for (let key of keys) {
  const value = person[key];
  //   console.log(key, value);
}
```

2-2. Object.values

- 객체에서 value 값들만 뽑아서 새로운 배열로 반환

```jsx
let values = Object.values(person);

for (let value of values) {
  //   console.log(value);
}
```

2-3. for in

```jsx
for (let key in person) {
  const value = person[key];
  console.log(key, value);
}
```

- 배열 메서드1. 요소 조작

6가지의 요소 조작 메서드

1. push
- 배열의 맨 뒤에 새로운 요소를 추가하는 메서드

```jsx
let arr1 = [1, 2, 3];
const newLength = arr1.push(4, 5, 6, 7);
```

1. pop
- 배열의 맨 뒤에 있는 요소를 제거하고, 반환

```jsx
let arr2 = [1, 2, 3];
const poppedItem = arr2.pop();
```

1. shift
- 배열의 맨 앞에 있는 요소를 제거, 반환

```jsx
let arr3 = [1, 2, 3];
const shiftedItem = arr3.shift();
```

1. unshift
- 배열의 맨 앞에 새로운 요소를 추가하는 메서드

```jsx
let arr4 = [1, 2, 3];
const newLength2 = arr4.unshift(0);
```

1. slice
- 마치 가위처럼, 배열의 특정 범위를 잘라내서 새로운 배열로 반환

```jsx
let arr5 = [1, 2, 3, 4, 5];
let sliced = arr5.slice(2, 5);
let sliced2 = arr5.slice(2);
let sliced3 = arr5.slice(-3);
```

1. concat
- 두개의 서로 다른 배열을 이어 붙여서 새로운 배열을 반환

```jsx
let arr6 = [1, 2];
let arr7 = [3, 4];

let concatedArr = arr6.concat(arr7);
console.log(concatedArr);
```

- 배열 메서드2. 순회와 탐색

5가지 요소 순회 및 탐색 메서드

1. forEach
- 모든 요소를 순회하면서, 각각의 요소에 특정 동작을 수행시키는 메서드

```jsx
let arr1 = [1, 2, 3];

arr1.forEach(function (item, idx, arr) {
  //   console.log(idx, item * 2);
});

let doubledArr = [];

arr1.forEach((item) => {
  doubledArr.push(item * 2);
});

```

1. includes
- 배열에 특정 요소가 있는지 확인하는 그런 메서드

```jsx
let arr2 = [1, 2, 3];
let isInclude = arr2.includes(10);
```

1. indexOf
- 특정 요소의 인덱스(위치)를 찾아서 반환하는 메서드

```jsx
let arr3 = [2, 2, 2];
let index = arr3.indexOf(20);

// let objectArr = [
//   { name: "김지원" },
//   { name: "홍길동" },
// ];

// console.log(
//   objectArr.indexOf({ name: "김지원" })
// );

// console.log(
//   objectArr.findIndex(
//     (item) => item.name === "김지원"
//   )
// );
```

1. findIndex
- 모든 요소를 순회하면서, 콜백함수를 만족하는 그런
- 특정 요소의 인덱스(위치)를 반환하는 메서드

```jsx
let arr4 = [1, 2, 3];
const findedIndex = arr4.findIndex(
  (item) => item === 999
);

console.log(findedIndex);
```

1. find
- 모든 요소를 순회하면서 콜백함수를 만족하는 요소를 찾는데, 요소를 그대로 반환

```jsx
let arr5 = [
  { name: "김지원" },
  { name: "홍길동" },
];

const finded = arr5.find(
  (item) => item.name === "김지원"
);

console.log(finded);
```

- 배열 메서드3. 배열 변형

5가지 배열 변형 메서드

1. filter
- 기존 배열에서 조건을 만족하는 요소들만 필터링하여 새로운 배열로 반환

```jsx
let arr1 = [
  { name: "김지원", hobby: "테니스" },
  { name: "김효빈", hobby: "테니스" },
  { name: "홍길동", hobby: "독서" },
];

const tennisPeople = arr1.filter(
  (item) => item.hobby === "테니스"
);
```

1. map
- 배열의 모든 요소를 순회하면서, 각각 콜백함수를 실행하고 그 결과값들을 모아서 새로운 배열로 반환

```jsx
let arr2 = [1, 2, 3];
const mapResult1 = arr2.map((item, idx, arr) => {
  return item * 2;
});

let names = arr1.map((item) => item.name);
```

1. sort
- 배열을 사전순으로 정렬하는 메서드

```jsx
let arr3 = [10, 3, 5];
arr3.sort((a, b) => {
  if (a > b) {
    // a가 b 앞에 와라
    return -1;
  } else if (a < b) {
    // b가 a 앞에 와라
    return 1;
  } else {
    // 두 값의 자리를 바꾸지 마라
    return 0;
  }
});
```

1. toSorted (가장 최근에 추가된 최신 함수)
- 정렬된 새로운 배열을 반환하는 메서드

```jsx
let arr5 = ["c", "a", "b"];
const sorted = arr5.toSorted();
```

1. join
- 배열의 모든 요소를 하나의 문자열로 합쳐서 반환하는 그런 메서드

```jsx
let arr6 = ["hi", "im", "woneeeee"];
const joined = arr6.join(" ");
console.log(joined);
```

- Date 객체와 날짜
1. Date 객체를 생성하는 방법

```jsx
let date1 = new Date(); // 생성자
let date2 = new Date(1997, 1, 7, 23, 59, 59);
```

1. 타임 스탬프
- 특정 시간이 "1970.01.01 00시 00분 00초"로 부터 몇 ms가 지났는지를 의미하는 숫자값

```jsx
let ts1 = date1.getTime();
let date4 = new Date(ts1);
```

1. 시간 요소들을 추출하는 방법

```jsx
let year = date1.getFullYear();
let month = date1.getMonth() + 1;
let date = date1.getDate();

let hour = date1.getHours();
let minute = date1.getMinutes();
let seconds = date1.getSeconds();
```

1. 시간 수정하기

```jsx
date1.setFullYear(2023);
date1.setMonth(2);
date1.setDate(30);
date1.setHours(23);
date1.setMinutes(59);
date1.setSeconds(59);
```

1. 시간을 여러 포맷으로 출력하기

```jsx
console.log(date1.toDateString());
console.log(date1.toLocaleString());
```

- 동기와 비동기

```jsx
console.log(1);

setTimeout(() => {
  console.log(2);
}, 3000);

console.log(3);
```

- 비동기 작업 처리하기 1. 콜백함수
- 음식을 주문하는 상황

```jsx
function orderFood(callback) {
  setTimeout(() => {
    const food = "떡볶이";
    callback(food);
  }, 3000);
}
```

```jsx
function cooldownFood(food, callback) {
  setTimeout(() => {
    const cooldownedFood = `식은 ${food}`;
    callback(cooldownedFood);
  }, 2000);
}
```

```jsx
function freezeFood(food, callback) {
  setTimeout(() => {
    const freezedFood = `냉동된 ${food}`;
    callback(freezedFood);
  }, 1500);
}

orderFood((food) => {
  console.log(food);

  cooldownFood(food, (cooldownedFood) => {
    console.log(cooldownedFood);

    freezeFood(cooldownedFood, (freezedFood) => {
      console.log(freezedFood);
    });
  });
});
```

- 비동기 작업 처리하기 2. Promise

```jsx
function add10(num) {
  const promise = new Promise((resolve, reject) => {
    // 비동기 작업 실행하는 함수
    // executor

    setTimeout(() => {
      if (typeof num === "number") {
        resolve(num + 10);
      } else {
        reject("num이 숫자가 아닙니다");
      }
    }, 2000);
  });

  return promise;
}

add10(0)
  .then((result) => {
    console.log(result);
    return add10(result);
  })
  .then((result) => {
    console.log(result);
    return add10(undefined);
  })
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.log(error);
  });
```

- 비동기 작업 처리하기 3. Async&amp;Await
1. Async
- 어떤 함수가 비동기 함수로 만들어주는 키워드
- 함수가 프로미스를 반환하도록 변환해주는 그런 키워드

```jsx
async function getData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve({
        name: "김지원",
        id: "woneeeee",
      });
    }, 1500);
  });
}
```

1. await
- async 함수 내부에서만 사용이 가능한 키워드
- 비동기 함수가 다 처리되기를 기다리는 역할

```jsx
async function printData() {
  const data = await getData();
  console.log(data);
}

printData();
```



---

</br>

### 질문
