# 1주차

**강의**
[인프런] - 한입 크기로 잘라머는 리액트(React.js) : 기초부터 실전까지
(https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8)

### 범위

섹션 0 ~ 섹션 5

- [ ] 0.  들어가며
- [ ] 1.  Javascript 기본
- [ ] 2.  Javascript 심화
- [ ] 3.  Node.js 기초
- [ ] 4.  React.js 개론
- [ ] 5.  React.js 입문

---

</br>

### 학습 내용

# JS-1

```jsx
const x = 1 / 0;
console.log(x);

const name = "Mike";
const y = name / 2;
console.log(y);
```

값을 0으로 나누면 : Infinity
string을 int로 나누면 (자료형이 맞지 않는 연산) : NaN

```jsx
let age;
console.log(age);

let user = null;
```

값을 할당하지 않으면 : undefined

## Typeof

- 변수의 type을 반환

```jsx
const name = "Mike";

console.log(typeof 3);
console.log(typeof name);
console.log(typeof true);
console.log(typeof "xxx");
console.log(typeof null);
console.log(typeof undefined);
```

```jsx
"number";
"string";
"boolean";
"string";
"object";
"undefined";
```

## 프롬프트

```jsx
alert("삭제되었습니다.");
prompt("예약일을 입력하세요.", "2020-10-");
confirm("구독을 취소 하시겠습니까?");
```

- alert : 그냥 보여주기만
- prompt : 보여주고, 입력받음 → 입력받은 값은 무조건 String
- confirm : 보여주고, 확인/취소

## 형변환

- String() → string으로 변환
- Number() → 숫자로 변환, 변환하려는 값에 문자가 포함되면 NaN이 뜸!
  - true : 1, false : 0
    Number(null) = 0
    Number(undefined) = NaN
    Number(0) = false
    Number(’0’) = true
    Number(’’) = false
    Number(’ ‘) = true
- Boolean()
  false
  - 숫자 0
  - 빈 문자열 ‘’
  - null
  - undefined
  - NaN
  → 그 외는 모두 true

## 비교 연산자

```jsx
const a = 1;
const b = "1";

console.log(a == b);
```

→ true (값이 같은지만 확인)

```jsx
const a = 1;
const b = "1";

console.log(a === b);
```

→ false (값이 같은지 확인하고, type이 같은지도 확인)

## null 병합 연산자

```jsx
let var1;
let var2 = 10;
let var3 = 20;

let var4 = var1 ?? var2;
```

→ null, undefined가 아닌 값을 찾아

만약 ??에 붙은 값이 모두 null이나 undefined가 아니라면 앞에 적힌 값!

## 함수 표현싯

```jsx
function funcA() {
  console.log("funcA");
}

let varA = funcA;
console.log(varA); //함수 내용이 나옴!

varA(); //funcA 호출
```

```jsx
let varB = function () {
  //익명함수
  console.log("funcB");
};

varB();
funcB(); //불가능!
```

## 화살표 함수

- EX1

```jsx
function showError() {
  console.log("error");
}
```

```jsx
let showError = () => {
  console.log("error");
};
```

- EX2

```jsx
const add = functioon (num1, num2) {
	const result = num1 + num2;
	return result;
}
```

```jsx
const add = (num1, num2) =>	return num1 + num2;
```

1. function 지우고 화살표
2. return문 한줄로 정리
3. 함수 내 코드가 한줄이면 괄호 생략 가능

## 콜백 함수

```jsx
function main(value) {
  value();
}

function sub() {
  console.log("i am sub");
}

main(sub);
```

→ 여기서는 sub함수임! 다른 함수에 인수로 전달된 함수!

### 함수 표현식 + 콜백함수 응용하기

```jsx
function main(value) {
  value();
}

//1
main(function sub() {
  console.log("i am sub");
});

//2
main(() => {
  console.log("i am sub");
});
```

### 콜백함수 활용…이거모르겠

```jsx
function repeat(count, callback) {
  for (let idx = 1; idx <= count; idx++) {
    callback(idx);
  }
}

repeat(5, function (idx) {
  console.log(idx);
});

//화살표함수
repeat(5, (idx) => {
  console.log(idx);
});
```

## Object

```jsx
let obj1 = new Object{}; //생성자
let obj2 = {}; //리터럴

let person = {
	name : "이정환",
	age : 27,
	hobby : "테니스",
	job : "FE Developer",
	extra : {},
	10 : 20,
	"like cat" : true
};
```

→ key : value

key - 숫자, 문자 가능(띄어쓰기가 포함되어있다면 따옴표로 묶어!)

- 접근

```jsx
person.name;
person["age"];
```

→ 존재하지 않는 property에 접근하면 undefined

- 추가

```jsx
person.job = "fe developer";
person["favoritefood"] = "떡볶이";
```

- 수정

```jsx
person.job = "fe developer";
person["favoritefood"] = "떡볶이";
```

- 삭제

```jsx
delete person.job;
```

- 존재유무 확인

```jsx
let result1 = "name" in person;
```

→ boolean값으로 반환

- 상수 객체

```jsx
const animal = {
	type : "고양이"
	name : "나비"
	color : "black",
};

animal.age = 2;
animal.name = "까망이";
delete animal.color;
```

상수객체는 새로운 값을 할당하는 것이 안됨.

기존에 있던 property 추가, 수정, 삭제는 가능!

## 배열

type 제한x, 길이 제한x

# JS-2

## Truthy & Falsy

true/false값이 아니지만 true/false값으로~

- Falsy
  ```jsx
  let f1 = undefined;
  let f2 = null;
  let f3 = 0;
  let f4 = -0;
  let f5 = NaN;
  let f6 = "";
  let f7 = 0n;
  ```
- Truthy

  → falsy를 제외한 모든 값!

    <br>

```jsx
if (!person) {
  console.log("person의 값이 없음");
  return;
}
console.log(person.name);
```

person의 값이 null이나 undefined로 들어왔을 때 조건문이 실행됨

**!person** means **person === null || person === undefined**

## 단락평가

첫번째 피연산자만으로 결과를 확정지을 수 있다면 두번째 피연산자의 값에는 접근조차 하지 않는!

```jsx
function returnFalse() {
  console.log("False 함수");
  return false;
}

function returnTrue() {
  console.log("True 함수");
  return true;
}

console.log(returnFalse() && returnTrue());
```

→ return값이 true/false가 아니라 truthy/falsy 값이어도 가능

```jsx
fucntion printName(person) {
	const name = person && person.name;
	console.log(name || "person의 값이 없음");
}

printName();
printName({name : "이정환"});
```

perrson의 값이 undefined라면 person.name에 접근하지x

→ name이 undefined이므로 “person의 값이 없음”이 출력됨

person의 값이 truthy하기 때문에 person.name에 접근

→ name의 값이 “이정환”이 됨, 피연산자 모두 truthy한 값이기 때문에 첫번째 피연산자인 name의 값이 출력됨

```jsx
T || T → 첫번째

T && T → 두번째
```

## 구조분해할당

없는 값에 할당하려고하면 → undefined

- 배열

```jsx
let arr = [1, 2, 3];

let [one, two, three] = arr;
```

- 객체

```jsx
let parson = {
	name : "이정환",
	age : 27,
	hobby : "테니스",
};

let {name, age, hobby} = person;

//객체 구조 분해 할당을 이용해서 함수의 매개변수를 받는 방법
const func = {{name, age, hobby, extra}} => {
	console.log(name, age, hobby, extra};
};

func(person);
```

## Spread

흩뿌리는 거,,

```jsx
let arr1 = [1, 2, 3];
let arr2 = [4, ...arr1, 5, 6];
```

```jsx
let obj1 = {
  a: 1,
  b: 2,
};

let obj2 = {
  ...obj1,
  c: 3,
  d: 4,
};
```

```jsx
function funcA(p1, p2, p3) {}

funcA(...arr1);
```

→ 배열의 값을 흩뿌려서 3개의 변수로

## Rest

```jsx
function funcB(one, ...rest) {}

funcB(...arr1);
```

→ 여러개의 매개변수를 하나의 배열로 받아옴! 만약 꼭 다른 이름으로 받고싶다..변수 설정해주면 됨!

## 원시타입 객체타입

![Untitled](JS-2%20177383adece84eaeaac2cd66bdb14b4c/Untitled.png)

![Untitled](JS-2%20177383adece84eaeaac2cd66bdb14b4c/Untitled%201.png)

객체타입 특성상 의도치 않게 원본 데이터의 값이 변경될 수 있으므로 다른 객체의 값을 가져올 때는 property만 복사해오는 방법을 사용해야!

![Untitled](JS-2%20177383adece84eaeaac2cd66bdb14b4c/Untitled%202.png)

```jsx
let o1 = { name: "이정ㅇ환" };
let o2 = o1;
let o3 = { ...o1 };

console.log(o1 === o2); //true
console.log(o2 === o3); //false
```

JSON.stringify() : 객체를 문자열로 변환하는 기능

![Untitled](JS-2%20177383adece84eaeaac2cd66bdb14b4c/Untitled%203.png)

### 배열순회

```jsx
for (let i = 0; i < arr.length; i++) {}

for (let item of arr) {
}
```

### 객체순회

```jsx
let keys = Object.keys(person);
```

Object.keys : 객체에서 key값을 뽑아서 새로운 배열로 반환

→ 이후에는 배열을 순회하듯 순회하면 됨

```jsx
let keys = Object.values(person);
```

Object.keys : 객체에서 value값만 뽑아서 새로운 배열로 반환

→ 이후에는 배열을 순회하듯 순회하면 됨

```jsx
for (let item in arr) {
}
```

## 배열메서드

- push : 배열에 요소 추가, length를 반환

```jsx
let arr1 = [1, 2, 3];
const newLength = arr1.push(4, 5, 6, 7);

console.log(newLength); //7
```

- pop : 배열의 맨 뒤에 있는 값 제거, 반환

```jsx
let arr1 = [1, 2, 3];
const poppedItem = arr1.pop;

console.log(poppedItem); //3
```

- shift : 배열의 맨 앞에 있는 요소 제거, 반환

```jsx
let arr1 = [1, 2, 3];
const shiftedItem = arr1.shift;

console.log(shiftedItem); //1
```

- unshift : 배열의 맨 앞에 요소 추가

```jsx
let arr1 = [1, 2, 3];
const newLength = arr1.unshift(0);

console.log(newLength); //4
```

- slice : 특정 범위를 잘라내서 반

```jsx
let arr1 = [1, 2, 3, 4, 5];
let sliced = arr1.slice(2, 5);

console.log(sliced); //3, 4, 5
console.log(arr1); //1, 2, 3, 4, 5 -원본 배열은 그대로 보
```

→ 인수가 1개면 해당 인덱스부터 끝까지, 뒤에서부터 세려면 음수

- concat : 두개의 배열을 연결한 새로운 배열을 반환

```jsx
let arr1 = [1, 2];
let arr2 = [3, 4];

let concatedArr = arr6.concat(arr7);
console.log(concatedArr); //1, 2, 3, 4
```

## 순회 & 탐색

- forEach

```jsx
let arr1 = [1, 2, 3];

arr1.forEach(function (item, index, arr) {
	console.log(idx, item * 2);
});

let doubleArr = [];

arr1.forEach(item) => {
	doubleArr.push(item * 2);
});
```

→ 모든 요소를 순회하면서 각각의 요소에 동작을 수행

- includes

```jsx
let arr1 = [1, 2, 3];

let isInclude = arr2.includes(10);
```

→ 배열에 특정 요소가 있는지 - return boolean

- indexOf

```jsx
let arr1 = [1, 2, 3];

let index = arr1.indexOf(20);
console.log(indeX);
```

→ 특정 요소의 인덱스를 찾아 반환, 없으면 -1

- findIndex

```jsx
let arr1 = [1, 2, 3];

const findedIndex = arr1.findIndex((item) => {
	if (item %== 2) return true;
});

//위에거랑 같
const findedIndex2 = arr1.findIndex((item) => item % 2 !== 0);

console.log(findedIndex);
```

→ 모든 요소를 순회하면서 콜백함수를 만족하는 인덱스를 반환, 만족하는 게 여러개라면 가장 먼저 만족하는 인덱스를 반환, 없으면 -1

**findIndex 쓰는 이유?**

indexOf는 특정 객체값의 위치를 찾을 수 없음 (=== 얕은 비교이기 때문)

- find

```jsx
let arr1 = [{ name: "이정환" }, { name: "홍길동" }];

const finded = arr1.find((item) => item.name === "이정환");

console.log(finded); //{name : "이정환"}
```

→ 모든 요소를 순회하면서 콜백함수를 만족하는 요소를 반환

## 배열 변형

- filter

```jsx
let arr1 = [
	{name : "이정환", hobby: "테니스"},
	{name : "김효빈", hobby: "테니스"},
	{name : "홍길동", hobby: "독서"},
];

const tennisPeople = arr1.filter((iteㅡ) => {
	if (item.hobby === "테니스" return true;
});

const tennisPeople2 = arr1.filter(
	(item) => item.hobby === "테니스"
});

console.log(tennisPeople); //	{name : "이정환", hobby: "테니스"}
													 // {name : "김효빈", hobby: "테니스"}
```

→ 기존 배열에서 조건을 만족하는 요소들만 필터링하여 새로운 배열로 반환

- map

```jsx
let arr1 = [1, 2, 3];

arr1.map((item, index, arr) => {
  console.log(idx, item);
  return item * 2;
});
```

foreEach랑 같은데 return값을 설정해줄 수 있음!!

```jsx
let arr1 = [
  { name: "이정환", hobby: "테니스" },
  { name: "김효빈", hobby: "테니스" },
  { name: "홍길동", hobby: "독서" },
];

let names = arr1.map((item) => item.name);
//arr1에서 name만 모아서 배열
```

- sort

```jsx
let arr1 = ["b", "a", "c"];
arr1.sort();

let arr2 = [10, 3, 5];
arr2.sort();
```

→ 원래의 배열은 수정되지 않음

- toSorted

```jsx
let arr1 = ["b", "a", "c"];
const sorted = arr1.toSorted();
```

- toSorted

```jsx
let arr1 = ["hi", "im", "winterlood"];
const joined = arr1.join();

console.log(joined); //hi, im, winterlood
```

join(””) : 연결할 문자 - 설정하지 않으면 ,

## 날짜와 시간

- Date

```jsx
let date1 = new Date();

let date2 = new Date("1997/01/07/10:10:10");
//Tue Jan 07 1997 10:10:10
//GMT+0900 (한국 표준시)

let date3 = new Date(1997, 1, 7, 23, 59, 59);
```

- 타임스탬프

```jsx
let ts1 = date1.getTime();
console.log(ts1);
```

→ 특정 시간이 1970.01.01 00시 00분 00초(UTC)에서 몇ms가 지났는지

```jsx
let date4 = new Date(ts1);
```

→ 타임스탬프 값으로 Date 객체 생성 가능

- 시간 요소 추출

```jsx
let year = date1.getFullYear();
let month = date1.getMonth();
let date = date1.getDate();

let hour = date1.getHours();
let minute = date1.getMinutes();
let seconds = date1.getSeconds();
```

✨ 1월 : 0

- 시간 수정

```jsx
date1.setFullYear(2023);
date1.setMonth(2);
date1.setDate(30);

date1.getHours(23);
date1.getMinutes(59);
date1.getSeconds(59);
```

- 시간 출력

```jsx
console.log(date1.toDateString()); //Thu Mar 30 2023
console.log(date1.toLocaleString()); //2023. 3. 30. 오후 11:59:59
```

## 동기와 비동기 ..추가 필요

```jsx
console.log("1");

setTimeout(() => {
	console.log(2);
), 3000); //3초 뒤에 콜백함수 실행

console.log("3");
```

setTimeout() :비동기적으로 실행하는 함수

![Untitled](JS-2%20177383adece84eaeaac2cd66bdb14b4c/Untitled%204.png)

# Node.js

javascript 실행환경 (구동기)

javascript를 범용적으로 사용할 수 있게 도와주는..

## 모듈 시스템

**math.js**

```jsx
function add(a, b) {
  return a + b;
}

function sub(a, b) {
  return a - b;
}

module.exports = {
  add: add,
  sub: sub,
};
```

**index.js**

```jsx
const moduleData = require("./math");

console.log(moduleData.add(1, 2));
console.log(moduleData.sub(1, 2));
```

```jsx
const { add, sub } = require("./math");

console.log(add(1, 2));
console.log(sub(1, 2));
```

→ 두가지 방법으로 쓸 수 있음

package.json 파일에 추가하면

```jsx
"type" : "module"
```

**math.js**

```jsx
function add(a, b) {
  return a + b;
}

function sub(a, b) {
  return a - b;
}

module.exports = {
  add: add,
  sub: sub,
};
```

**index.js**

```jsx
import { add, sub } from "./math.js";

console.log(add(1, 2));
console.log(sub(1, 2));
```

## → 이렇게 쓸 수 있음!

</br>

### 질문
