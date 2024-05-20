### Truthy & Falsy

: 참이나 거짓을 의미하지 않는 값도, 조건문 내에서 참이나 거짓으로 평가하는 특징

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/b75230a7-3395-48ba-9181-88bba5e9cc1a/Untitled.png)

```jsx
// 1. Falsy한 값
let f1 = undefined;
let f2 = null;
let f3 = 0;
let f4 = -0;
let f5 = NaN;
let f6 = "";
let f7 = 0n; //무한대 같은~

// 2. Truthy 한 값
// -> 7가지 Falsy 한 값들 제외한 나머지 모든 값
let t1 = "hello";
let t2 = 123;
let t3 = [];
let t4 = {};
let t5 = () => {};

// 3. 활용 사례
//비효율적인 조건문을 개선할 수 있다.
function printName(person) {
  if (!person) { 
    console.log("person의 값이 없음");
    return;
  }
  console.log(person.name);
}

let person = { name: "이유진" };
printName(person);
```

### 단락 평가

**단락 평가(Short-Circuit Evaluation)**

: 논리 연산에서 첫 번째 피연산자의 값만으로 해당 식의 결과가 확실할 때, 두 번째 값은 평가하지 않는 것

```jsx
// 단락 평가
function returnFalse(){
    console.log("False");
    return false;
}

function returnTrue(){
    console.log("True");
    return true;
}

// 이 경우 첫 피연산자 값이 false이므로 결과는 false니까 returnTrue()함수 실행 안 함.
console.log(returnFalse() && returnTrue()); //콘솔에 False 출력
console.log(returnTrue() && returnFalse()); //콘솔에 True, False 둘 다 출력

// 이 경우 첫 피연산자 값이 true면 결과는 true니까 returnFalse() 함수 실행 안 함. 
console.log(returnTrue() || returnFalse());//콘솔에 True 출력 
console.log(returnFalse() || returnTrue()); //콘솔에 False, True 둘 다 출력

// 단락 평가 활용 사례

function printName(person) {
    // truthy || truthy => 첫번째 값이 들어감
    // truthy && truthy => 두번째 값이 들어감 
    const name = person && person.name;
    console.log(name || "person의 값이 없음");
  }
  
  printName(); // "person의 값이 없음" 출력됨
  printName({ name: "이유진" }); //이유진 출력 됨
```

### 구조 분해 할당

**구조 분해 할당 (Destructuring assignment)**

: 구조 분해 할당 구문은 배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 JavaScript 표현식

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/01fa93d1-7203-45b5-b7f5-8a671dd157e9/Untitled.png)

```jsx
// 1. 배열의 구조 분해 할당
let arr = [1, 2, 3];

// let [one, two, three, four] = arr; // 1, 2, 3, undefined
let [one, two, three, four = 4] = arr; // 1, 2, 3, 4
 
// 2. 객체의 구조 분해 할당
let person = {
  name: "이유진",
  age: 24,
  hobby: "독서",
};

// let{name, age, hobby} = person; //이유진, 24, 독서

// { 객체 프로퍼티: 목표 변수 }
let {
  age: myAge, //myAge에 person.age 값이 담김 
  hobby,
  name,
  extra = "hello",
} = person;

// 3. 객체 구조 분해 할당을 이용해서 함수의 매개변수를 받는 방법
const func = ({ name, age, hobby, extra }) => { // 여기 func에서 구조분해 할당을 하며 인자로 값을 받아올 수 있음 
  console.log(name, age, hobby, extra);
};

func(person); //이런식으로 객체를 넘겼을 떄
```

### Spread 연산자 & Rest 매개변수

**Spread Operator (Spread 연산자)**

: 배열이나 문자열과 같이 여러개의 요소를 가져올 때 사용된다.

**Rest parameter (나머지 매개변수)**

앞서 살펴본 **Spread** 연산자와 사용 방법은 동일하다.

다만 rest 파라미터는 함수에서 사용하는 `...매개변수`를 의미한다.

rest 파라미터로 전달된 값들은 배열의 형태가 된다.

```jsx
// 1. Spread 연산자
// -> Spread : 흩뿌리다, 펼치다 라는 뜻
// -> 객체나 배열에 저장된 여러개의 값을 개별로 흩뿌려주는 역할

let arr1 = [1, 2, 3];
let arr2 = [4, ...arr1, 5, 6]; //4, 1, 2, 3, 5, 6

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
  //   console.log(p1, p2, p3); //1, 2, 3
}

funcA(...arr1);

// 2. Rest 매개변수
// -> Rest는 나머지 , 나머지 매개변수

// rest 변수 뒤에 다른 변수 추가 불가능
//...만 붙이면 rest가 아니라 다른 이름으로 적어도 괜찮다
function funcB(one, two, ...rest) {  
    //몇 개의 변수만 특정 변수에 담고 나머지는 rest에 담는 경우
  console.log(rest);
}

funcB(...arr1);
```

### 원시타입 VS 객체타입

: 원시타입과 객체타입은 값이 저장되거나 복사 되는 과정이 서로 다름 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/749802e6-d81a-4f7e-97e3-abc433aa1074/Untitled.png)

객체 타입을 복사하여 사용할 경우 주의 사항 1 (복사)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/446176f9-8b52-442c-a091-0ed4ecca454f/Untitled.png)

객체 타입을 복사하여 사용할 경우 주의 사항 2 (비교)

- 숫자, 문자열 등 원시 자료형(**Primitive Type**)은 값을 비교한다.
- 배열, 객체 등 참조 자료형(**Reference Type)**은 값 혹은 속성을 비교하지 않고, 참조되는 위치를 비교한다.
- 얕은 비교와 달리 깊은 비교는 객체의 경우에도 값으로 비교한다. 깊은 비교 방법은 아래와 같다.
    1. Object depth 가 깊지 않은 경우 : JSON.stringify() 사용
    2. Object depth 가 깊은 경우 : lodash 라이브러리의 isEqual() 사용

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/790a586d-9a18-42c0-b1c1-e5d513648ce2/Untitled.png)

배열과 함수도 객체다!

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/1845ca82-391f-491f-a9e8-f8796c8af7c2/Untitled.png)

### 반복문으로 배열과 객체 순회하기

**순회(Iteration)**

: 배열, 객체에 저장된 여러 개의 값에 순서대로 하나씩 접근하는 것을 말함 

```jsx
// 1. 배열 순회
let arr = [1, 2, 3];

// 1.1 배열 인덱스
for (let i = 0; i < arr.length; i++) {
  //   console.log(arr[i]); //1, 2, 3
}

let arr2 = [4, 5, 6, 7, 8];
for (let i = 0; i < arr2.length; i++) {
  //   console.log(arr2[i]); // 4, 5, 6, 7, 8
}

// 1.2 for of 반복문
for (let item of arr) { //arr 배열의 값을 하나씩 item에 저장함 
  //   console.log(item); // 1, 2, 3
}

// 2. 객체 순회
let person = {
  name: "이유진",
  age: 24,
  hobby: "독서",
};

// 2.1 Object.keys 사용
// -> 객체에서 key 값들만 뽑아서 새로운 배열로 반환
let keys = Object.keys(person);

for (let key of keys) {
  const value = person[key];
   //   console.log(key); //name, age, hobby
  //   console.log(key, value); //name 이유진, age 24, hobby 독서
}

// 2.2 Object.values
// -> 객체에서 value 값들만 뽑아서 새로운 배열로 반환
let values = Object.values(person);

for (let value of values) {
  //   console.log(value); // 이유진, 24, 독서
}

// 2.3 for in
// -> 객체만을 위한 반복문 
for (let key in person) { //person 객체의 key값을 변수 key에 넣어줌 
  const value = person[key];
  console.log(key, value); //name 이유진, age 24, hobby 독서
}
```

## 배열 메서드

### 1. 요소 조작

```jsx
// 6가지의 요소 조작 메서드

// 1. push
// 배열의 맨 뒤에 새로운 요소를 추가하는 메서드
let arr1 = [1, 2, 3];
const newLength = arr1.push(4, 5, 6, 7);

console.log(arr1); // 1, 2, 3, 4, 5, 6, 7
console.log(newLength); // 7, 요소가 추가된 길이 반환

// 2. pop
// 배열의 맨 뒤에 있는 요소를 제거하고, 반환
let arr2 = [1, 2, 3];
const poppedItem = arr2.pop();

console.log(arr2); // 1, 2
console.log(poppedItem); // 3, 제거된 요소 반환

//shift와 unshift는 push나 pop 보다 비교적 느리게 동작함.

// 3. shift
// 배열의 맨 앞에 있는 요소를 제거, 반환
let arr3 = [1, 2, 3];
const shiftedItem = arr3.shift();

console.log(arr3); // 2, 3
console.log(shiftedItem); // 1, 제거된 요소 반환

// 4. unshift
// 배열의 맨 앞에 새로운 요소를 추가하는 메서드
let arr4 = [1, 2, 3];
const newLength2 = arr4.unshift(0);

console.log(arr3); // 0, 1, 2, 3
console.log(shiftedItem); // 4, 요소가 추가된 길이 반환

// 5. slice
// 마치 가위처럼, 배열의 특정 범위를 잘라내서 새로운 배열로 반환
let arr5 = [1, 2, 3, 4, 5];
let sliced = arr5.slice(2, 5); // 3, 4, 5
let sliced2 = arr5.slice(2); // 3, 4, 5
let sliced3 = arr5.slice(-3); // 3, 4, 5

// 6. concat
// 두개의 서로 다른 배열을 이어 붙여서 새로운 배열을 반환
let arr6 = [1, 2];
let arr7 = [3, 4];

let concatedArr = arr6.concat(arr7);
console.log(concatedArr); //1, 2, 3, 4

```

### 2. 순회와 탐색

```jsx
// 5가지 요소 순회 및 탐색 메서드
// 1. forEach
// 모든 요소를 순회하면서, 각각의 요소에 특정 동작을 수행시키는 메서드

let arr1 = [1, 2, 3];

arr1.forEach(function(item,idx,arr){
    console.log(idx, itme*2);
});

let doubledArr = [];

arr1.forEach((item)=>{
    doubledArr.push(item * 2);
});

// 2. includes
// 배열에 특정 요소가 있는지 확인하는 메서드

let arr2 = [1,2,3];
let isInclude1 = arr2.includes(2); //true
let isInclude2 = arr2.includes(10); //false

// 3. indexOf
// 특정 요소의 인덱스(위치)를 찾아서 반환하는 메서드
let arr3 = [1, 2, 3];
let objArr = [
    {name:"이유진"},
    {name:"홍길동"} 
];

// 같은 요소들이 있으면 앞에 있는 요소의 index 반환
// 존재하지 않는 요소 탐색시 -1 반환
let index = arr3.indexOf(2); //1

// 4. findIndex
// 모든 요소를 순회하면서, 콜백함수를 만족하는 그런
// 특정 요소의 인데스를 반환하는 메서드

let arr4 = [1, 2, 3];
const findedIndex = arr4.findIndex((item) =>{
    if(item % 2 !== 0 ) return true;
}); // 0출력
// 괄호랑 if문 없이도 사용 가능 
// 존재하지 않는 요소 탐색시 -1 반환
const findedIndex2 = arr4.findIndex((item) => item % 2 !== 0 ); // 0출력

// 원시타입에서 사용시 indexOf 사용
// 객체타입에서 사용시 findOf 사용 
console.log(
    objArr.indexOf({name:"이유진"})
); // indexOf는 얕은 비교이기 때문에 -1 반환

console.log(
    objArr.findIndex((item)=>item.name==="이유진")
); // 특정 프로퍼티를 비교하여 반환하기 때문에 객체 탐색 가능, 0 반환

// 5. find
// 모든 요소를 순회하면서 콜백함수를 만족하는 요소를 찾는데, 요소를 그대로 반환

let objArr1 = [
    {name:"이유진"},
    {name:"홍길동"} 
];

const finded = objArr1.find(
    (itme)=>item.name ==="이유진"
); //{name:"이유진"} 객체 반환 
```

### 3. 변형

sort

- 비교 함수가 양수를 반환
    
    a와 b 중 b의 위치가 a보다 앞이어야 한다는 것을 의미.
    
- 비교 함수가 음수를 반환
    
    a와 b 중 a의 위치가 b보다 앞이어야 한다는 것을 의미.
    
- 비교 함수가 0을 반환
    
    비교 함수가 0을 반환하면, a와 b는 정렬 순서가 동일하다는 것을 의미.
    

```jsx
// 5가지 배열 변형 메서드
// 1. filter
// 기존 배열에서 조건을 만족하는 요소들만 필터링하여 새로운 배열로 변환

let arr1 = [
    { name: "이유진", hobby: "독서" },
    { name: "김효빈", hobby: "테니스" },
    { name: "홍길동", hobby: "독서" },
  ];

  const readingPeople = arr1.filter((item)=>item.hobby==="독서"); //hobby가 독서인 객체를 배열로 반환

// 2. map
// 배열의 모든 요소를 순회하면서, 각각 콜백함수를 실행하고 그 결과값들ㅇ르 모아서 새로운 배열로 반환
// forEach() 메소드는 반환 값을 가지지 않으며, 기존 배열을 수정
// 반면, map() 메소드는 새로운 배열을 반환하며, 기존 배열을 수정하지 않음

let arr2 = [1, 2, 3];
const mapResult1 = arr2.map((item, idx, arr) => {
  return item * 2;
}); // 2, 4, 6

let names = arr1.map((item)=>item.name); //이유진, 김효빈, 홍길동을 배열로 반환

// 3. sort
// 배열을 사전순으로 정렬하는 메서드
// 원본 배열 변경

let arr3 =[10,3,5];
arr3.sort(); // 숫자는 정렬 안 됨, 대소관계 비교 함수 넣어줘야 함

//오름차순
arr3.sort((a,b)=>{
    if(a>b){
        //b가 a 앞으로 와라
        return 1; // b, a 배치
    }else if(b>a){
        //a가 b 앞으로 와라
        return -1; // a, b 배치 
    }else{
        //두 값의 자리를 바꾸지 마라
        return 0;
    }
})
//내림차순
arr3.sort((a, b) => {
    if (a > b) {
      // a가 b 앞에 와라
      return -1; // a, b 배치 
    } else if (a < b) {
      // b가 a 앞에 와라
      return 1; //b, a 배치 
    } else {
      // 두 값의 자리를 바꾸지 마라
      return 0;
    }
  });

// 4. toSorted 
// 정렬된 새로운 배열을 반환하는 메서드

let arr5 = ["c", "a", "b"];
const sorted = arr5.toSorted(); 

// 5. join
// 배열의 모든 요소를 하나의 문자열로 합쳐서 반환하는 메서드
let arr6 = ["hi", "im", "winterlood"];
//join("") 괄호안에 원하는 seperater 넣으면 됨
const joined = arr6.join(" "); //hi im winterloof
```

### Date 객체와 날짜

```jsx
// 1. Date 객체를 생성하는 방법

let date1 = new Date(); //생성자
console.log(date1); //현재날짜

let date2 = new Date("1970-01-01-10:10:10"); //',', '/', '-'로 구분 가능, 문자 말고 숫자 넣어도 됨
console.log(date2); //위에 설정한 날짜 출력

// 2. 타임 스탬프
// 특정 시간이 "1970.01.01 00시 00분 00초"(UTC)로 부터 몇 ms가 지났는지를 의미하는 숫자값

let ts1=date1.getTime();
let date4 = newDate(ts1); //date1과 같은 시간이 저장됨

// 3. 시간 요소들을 추출하는 방법

let year = date1.getFullYear();
let month = date1.getMonth() + 1; //js의 month는 0부터 시작함
let date = date1.getDate();

let hour = date1.getHours();
let minute = date1.getMinutes();
let seconds = date1.getSeconds();

// 4. 시간 수정하기

date1.setFullYear(2023);
date1.setMonth(2); //3월
date1.setDate(30);
date1.setHours(23);
date1.setMinutes(59);
date1.setSeconds(59);

// 5. 시간을 여러 포맷으로 출력하기

console.log(date1.toDateString()); //문자로 날짜 출력
console.log(date1.toLocaleString()); //숫자로 날짜 출력
```

## 동기와 비동기

**동기** : 여러개의 작업을 순서대로, 하나씩 처리하는 방식

JS는 “동기”적으로 코드를 실행한다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/8ef48920-c839-4208-9205-3047f49d435f/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/921f1998-1c45-4fc8-950b-847f023e65d1/Untitled.png)

**비동기** : 작업을 순서대로 처리하지 않음

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/7bf6439e-bf5a-4658-a8e4-58c2ae49a806/Untitled.png)

```jsx
console.log(1);

setTimeout(() => {
  console.log(2);
}, 3000);

console.log(3);

//1 ,3 , 2 순서로 출력 됨

```

Q. JS는 쓰레드가 1개인데 어떻게 setTimeout이랑 console.log(3)을 동시에 처리 하는 거야?

A. 비동기 작업들은 JS 엔진이 아닌 Web APIs에서 실행하니까!

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/d20a088b-11a4-4f76-b542-56af74e0946f/Untitled.png)

### 1. 콜백함수 - 비동기 작업 처리하기

**콜백함수(Callback Function)**

: **파라미터로 함수를 전달**받아, 함수의 내부에서 실행하는 함수

```
// function add(a,b,callback){
//     setTimeout(()=>{
//         const sum = a+b;
//         callback(sum);
//     },3000);
// }

// add(1,2,(value)=>{
//     console.log(value);
// });

// 음식을 주문하는 상황
function orderFood(callback) {
    setTimeout(() => {
      const food = "떡볶이";
      callback(food);
    }, 3000);
  }
  
  function cooldownFood(food, callback) {
    setTimeout(() => {
      const cooldownedFood = `식은 ${food}`;
      callback(cooldownedFood);
    }, 2000);
  }
  
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
  }); //3초 후 떡볶이, 2초 후 식은 떡볶이, 1.5초 후 냉동된 떡볶이 출

```

### 2. Promise - 비동기 작업 처리하기

**Promise**

: 비동기 작업을 효율적으로 처리할 수 있도록 도와주는 자바스크립트의 내장 객체

**Promise는 비동기 작업을 감싸는 객체이다!** 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/f329d934-bc55-46dd-b445-a711f1f445e5/Untitled.png)

**Promise의 3가지 상태**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/d121536b-124e-4baa-9161-bac5c812462d/Untitled.png)

```jsx
function add10(num) {
    const promise = new Promise((resolve, reject) => { //resolve 성공, reject 실패
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
  // then 메서드, promise 작업이 성공해야 실행
  // catch 메서드, promise 작업이 실패하면 실행
  
  add10(0)
    .then((result) => {
      console.log(result); //10
      return add10(result); 
    })
    .then((result) => {
      console.log(result); //20
      return add10(undefined); //이 경우 catch 메서드에서 num이 숫자가 아닙니다 출력
    })
    .then((result) => {
      console.log(result); //30
    })
    .catch((error) => {
      console.log(error); 
    });
```

### 3. Async&apm;Await - 비동기 작업 처리하기

```jsx
// async
// 어떤 함수를 비동기 함수로 만들어주는 키워드
// 함수가 프로미스를 반환하도록 변환해주는 그런 키워드

async function getData() {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve({
          name: "이정환",
          id: "winterlood",
        });
      }, 1500);
    });
  }
  
  // await
  // async 함수 내부에서만 사용이 가능 한 키워드
  // 비동기 함수가 다 처리되기를 기다리는 역할
  
  async function printData() {
    const data = await getData();
    console.log(data);
  }
  
  printData();
```