### 변수와 상수

**let** : 변수, 값 변경 가능

**const** : 상수 값 변경 불가능, 선언과 함께 초기화

### 자료형

**자료형 (type)**

: 동일한 속성이나 특징을 가진 원소들을 묶은 것 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/d8b6f15b-b722-4673-95ab-799ba434fee8/Untitled.png)

원시타입 : 기본형 타입이라고도 불림, 프로그래밍에 있어 가장 기본적인 값들의 타입을 의미

```jsx
// 1. Number type
let num1 = 27;
let num2 = 1.5;
let num3 = -20;

let inf = Infinity;
let mInf = -Infinity;

let nan = NaN;

// 2.String type
let myName = "yujin";
let myLocate = "Icheon";
let introduce = myName+myLocate;

//값을 동적으로 할당 가능
let introduceText = `${myName}은 ${myLocate}에 거주 합닏나.`;

// 3. Boolean type
let isOdd = true;
let isEmpty = false;

// 4. Null type (아무것도 없다)
let empty = null;

// 5. undefined type
let none;
```

### 형변환

**형변환 (Type Casting)**

: 어떤 값의 타입을 다른 타입으로 변경하는 것을 말함

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/41709e04-9254-4f89-bd89-ddc395854684/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/e57df912-ae83-4c2e-9604-d8ee441853d9/Untitled.png)

쉽게 말하면 **묵시적**은 **‘내가 생각하지 못했는데 형이 변환 되는 것’**, **명시적**은 **‘내가 시켜야 형변환이 되는 것’**

```jsx
// 1. 묵시적 형변환
//->자바스크립트 엔진이 알아서 변환 하는 것

let num = 10;
let str = "20";

const result = num + str; //1020 , num을 묵시적으로 string 타입으로 변경

// 2. 명시적 형변환
//->프로그래머 내장함수 등을 이용해서 직접 형 변환을 명시

//->문자열 => 숫자
let str1 = "10";
let strToNum1 = Number(str1);

let str2 = "10개";
let strToNum2 = parseInt(str2); //문자가 포함 된 경우 Number()가 아닌 parseInt()사용

//->숫자 => 문자열
let num1 = 20;
let numToString1 = String(num1);
```

### 연산자

```jsx
// 1. 대입 연산자
let var1 = 1;

//2. 산술 연산자
let num1 = 1+2;
let num2 = 1-2;

// 3. 복합 대입 연산자
let num7 = 10;
num+=7;

// 4. 증감 연산자
let num8 = 3;
num8++; //후위 연산, 나중에 연산 적용
++num8; //전위 연산, 연산 바로 적용

// 5. 논리 연산자
let or = true || false;
let and = true && false;
let not = !true;

// 6. 비교 연산자
let comp1 = 1 === 2; // '==' 자료형까지 비교 불가능, '===' 자료형까지 비교 가능
let comp2 = 1 !==2;

let comp3 = 2>1;
let comp4 = 2>=1;

// 8. Null 병합 연산자
// -> 존재하는 값을 추려내는 기능
// -> 피연산자 중 Null, undefined가 아닌 값을 찾아내는 연산자
let a;
let b=10;
let c=20;

let d = a ?? b; //이 경우 d에는 10이 들어감
let e = b ?? c; //둘 다 존재하는 값이면 앞에 있는 값이 들어감 e==1o

// 9. typeof 연산자
// -> 값의 타입을 문자열로 변환하는 기능을 하는 연산자

let var3 = 1;
var7 = "안녕";
var7 = ture;

let t1 = typeof var7; //boolean

// 10. 삼항 연산자
// -> 항을 3개 사용하는 연산자
// -> 조건식을 이용해서 참, 거짓일 때의 값을 다르게 변환
let var2 = 10;

//요구사항 : 변수 res에 var2의 값이 짝수 -> '짝', 홀수 -> '홀'
//조건 ? 참 : 거짓
 let res = var2%2 === 0 ? '짝수' : '홀수';
```

### 조건문

**조건문**

: 특정 조건을 만족했을 때에만 실행되는 코드를 작성하기 위한 문법

```jsx
// 1. if 조건문
 let num = 10;

 if (num>10){
    console.log("어쩌구");
 }
 else if(num===10){
    console.log("저쩌구");
 }
 else{
    console.log("blabla");
 }

// 2. Switch 문
//->if문과 기능 자체는 동일
//->다수의 조건을 처리할 시 if문 보다 적합

let animal = "cat";

switch(animal){
    case "cat":{
        console.log("고양이");
        break;
    }
    case "dog":{
        console.log("강아지");
        break;
    }
    case "bear":{
        console.log("곰");
        break;
    }
    default:{
        console.log("무슨 동움인지 몰라요.");
    }
}
```

### 반복문

반복문 

: 어떤 동작을 반복해서 수행할 수 있도록 만들어 주는 문법

```jsx
for(let i = 0; i<5; i++){
    if(i%2===0){
        continue;
    }
    if(i>=4){
        break;
    }
    console.log("dd");
}
```

### 함수

**함수**

: 중복으로 작성되는 코드들을 묶어서 이름을 붙여주는 문법

```jsx
// 함수
let area1 = getArea(10, 20);
console.log(area1);

let area2 = getArea(30, 20);
console.log(area2);

getArea(120, 200);

// 호이스팅
// -> 끌어올리다 라는 뜻
// 선언문을 호출문 보다 먼저 나오지 않아도 괜찮
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

**함수 표현식과 화살표 함수** 

```jsx
// 1. 함수 표현식
function funcA() {
       console.log("funcA");
  }
  
  let varA = funcA;
  varA();
  
  let varB = function () { //값으로 함수가 생성된 경우 따로 선언 불가능, 따라서 익명함수로 만든다.
       console.log("funcB");
  };
  
  varB(); //선언문과 다르게 호이스팅 불가능
  
  // 2. 화살표 함수
  let varC = (value) => {
    console.log(value);
    return value + 1;
  };
  
  console.log(varC(10)); //11 출력
```

**콜백 함수**

: 자신이 아닌 다른 함수에, 인수로써 전달된 함수를 의미

```jsx
// 1. 콜백함수
//메인 함수가 원할 때 언제든지 실행할 수 있음
function main(value){
    console.log(value);
    value();
}

function sub(){
    console.log("haha");
}

main(sub);

main(()=>{
    console.log("haha");
});

// 2. 콜백함수 활용
function repeat(count, callback) {
    for (let idx = 1; idx <= count; idx++) {
      callback(idx);
    }
  }
  
repeat(5, (idx) =>{
    console.log(idx*2);
});

  
repeat(5, (idx) =>{
    console.log(idx*3);
});
```

### 스코프

**스코프(Scope)**

: “범위”, 변수나 함수에 접근하거나 호출할 수 있는 범위를 말 함

```jsx
// 스코프
// -> 전역(전체 영역) 스코프 / 지역(특정 영역) 스코프
// -> 전역 스코프 : 전체 영역에서 접근 가능
// -> 지역 스코프 : 특정 영역에서만 접근 가능

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
```

### 객체

객체(Object)

: 원시 타입이 아닌 객체 타입의 자료형, 여러가지 값을 동시에 저장할 수 있는 자료형을 의미

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/40ec8533-4199-4c0e-828d-761eebe47c33/Untitled.png)

```jsx
// 1. 객체 생성
let obj1 = new Object(); // 객체 생성자
let obj2 = {}; // 객체 리터럴 (대부분 사용)

// 2. 객체 프로퍼티 (객체 속성)
let person = { // key : value
  name: "이유진",
  age: 24,
  hobby: "독서",
  job: "FE Developer",
  extra: {},
  10: 20,
  "like cat": true, //key에 띄어쓰기 넣으려면 ""로 감싸줘야 함
};

// 3. 객체 프로퍼티를 다루는 방법
// 3.1 특정 프로퍼티에 접근 (점 표기법, 괄호 표기법)
let name = person.name;
let age = person["age2"];

let property = "hobby";
let hobby = person[property];

// 3.2 새로운 프로퍼티를 추가하는 방법
person.job = "fe developer";
person["favoriteFood"] = "떡볶이";

// 3.3 프로퍼티를 수정하는 방법
person.job = "educator";
person["favoriteFood"] = "초콜릿";

// 3.4 프로퍼티를 삭제하는 방법
delete person.job;
delete person["favoriteFood"];

// 3.5 프로퍼티의 존재 유무를 확인하는 방법 (in 연산자)
//존재하면 true, 아니면 false 반환
let result1 = "name" in person; // true
let result2 = "cat" in person; //false
console.log(result2);
```

```jsx
// 1. 상수 객체
const animal = {
    type: "고양이",
    name: "나비",
    color: "black",
  };
  
  animal.age = 2; // 추가
  animal.name = "까망이"; // 수정
  delete animal.color; // 삭제
  
  // 2. 메서드
  // -> 값이 함수인 프로퍼티를 말함
  const person = {
    name: "이유진",

    // sayHi : function(){
    //     console.log("안녕!");
    // },
    // 메서드 선언
    sayHi() { 
      console.log("안녕!");
    },
  };
  
  person.sayHi();
  person["sayHi"]();
```

### 배열

**배열(Array)**

: 여러개의 값을 순차적으로 담을 수 있는 자료형 

```jsx
// 1. 배열 생성
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

// 2. 배열 요소 접근
let item1 = arrC[0];
let item2 = arrC[1];

arrC[0] = "hello";
console.log(arrC);
```