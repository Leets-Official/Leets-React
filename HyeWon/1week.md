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
# ch01_js basic

- html 기반으로 실시간으로 페이지 변화 확인 하는 법 : html에서 ctrl + shipt + p → open server → console 창 보기 ( 여기서 console 창 열어서 보는 법 : F12 )
- console 창 여는 법

## 1. 변수, 상수

= 값을 저장하는 박스

```jsx
//1. 변수
let age = 27; //age라는 변수 선언, 초기화
console.log(age);

age = 30;     // 값을 바꿀 수 있음
console.log(age);
```

```jsx
//2. 상수
const bith = "1997.01.07"; // 초기화 반드시 필요
birth = "123" //변수처럼 변할 수 없음
```

```jsx
//3. 변수 명명규칙(네이밍 규칙)
//3-1. $, _ 제외한 기호는 사용할 수 없다.
let $_name;

//3-2. 숫자로 시작할 수 없다.
let name1;
let $2name;

//3-3. 예약어를 사용할 수 없다.

// 4. 변수 명명 가이드
let salesCount =1;
let refundCount =1;
let totalSalesCount =salesCount-refundCount;
```

## 2. 집합 ( 자료형type)

= 동일한 속성 묶은 거!

![Untitled](ch01_js%20basic%206df9da77a6304c92be38770dd3a846b6/Untitled.png)

## 3. 자료형

```jsx
// 1. Number Type
let num1 = 27;
let num2 = 1.5;
let num3 = -20;
// console.log(num1%num2); // 모듈러 연산

let inf = Infinity;
let mInt = -Infinity;

let nan = NaN;

// 2. String Type
let myName = "양혜원";
let myLocation = "안산";
let introduce = myName + myLocation;

let introduceText = `${myName}은 ${myLocation}에 거주합니다.`; // 변수값을 동적으로 할당 ( 템플릿 리터럴 문법)

// 3. Boolean Type
let isSwitch = true; // 상태 나타냄
let isEmpty = false;

// 4. Null Type (아무것도 없음) -> 명시적으로 표현하는 거
let empty = null;

// 5. Undefined Type (아무것도 x, 존재 x일 때, 자동으로 할당되는 값)
let none; 
console.log(none);
```

## 형 변환

= type casting

- 묵시적 형 변환 (암묵적 형변환)
    
    개발자가 직접 설정 안 해도 알아서 js 엔진이 형 변환
    
- 명시적 형 변환 (시켜야만 변하는 거)
    
    개발자가 직접 함수 등을 이용해 형 변환을 일으킴
    

```jsx
// 1. 묵시적 형 변환
// -> 자바 스크립트 엔진이 알아서 형 변환 하는 것

let num = 10;
let str = "20";

const result = num + str;
console.log(result);

// 2. 명시적 형 변환
// -> 프로그래머 내장함수 등을 이용해서 직접 형 변환을 명시

// -> 문자열 -> 숫자
let str1 = "10";
let strToNum1 = Number(str1);
console.log(10+strToNum1);

// 숫자형, 문자형 섞여있을 때 (parse)
let str2 = "10개";
let strToNum2 = parseInt(str2);
console.log(strToNum2);

// -> 숫자 -> 문자열
let num1 = 20;
let numToStr1 = String(num1);

console.log(numTostr1 + "입니다"); // 20입니다
```

## 4. 연산자(1)

```jsx
// 1. 대입 연산자
let var1 = 1;

// 2. 산술 연산자(우선순위 있음)
let num1 = 3+2;
let num2 = 3-2;
let num3 = 3*2;
let num4 = 3/2;
let num5 = 3%2;

// 3. 복합 대입 연산자 ( 복합 = 산술 + 대입)
let num7 = 10;
num7 += 20;
num7 -= 20;
num7 *= 20;
num7 /= 20;
num7 %= 20;

// 4. 증감 연산자
let num6 = 10;
++num6; //전위연산
num6++; //후위연산

// 5. 논리 연산자
let or = true || false;
let and = true && false;
let not = !true;
console.log(or, and, not); //true false false

// 5. 비교 연산자
let comp1 = 1=== "1"; // =를 두번만 쓰면 값의 자료형까지 같은지는 비교X.
let comp2 = 1!==2;

let comp3 = 2 > 1;
let comp4 = 2 < 1;

let comp5 = 2 >= 2;
let comp6 = 2 <= 2;
```

## 4. 연산자(2)

```jsx
// 1. null 병합 연산자 ( ?? )
// -> 존재하는 값을 추려내는 기능
// -> null, undefined가 아닌 값을 찾아내는 연산자

let var1;
let var2 = 10;
let var3 = 20;

let var4 = var1 ?? var2; // undefined 아닌 걸 찾아내는 것! : 10
let var5 = var1 ?? var3; // 20
let var6 = var2 ?? var3; // 둘 다 undefined가 아닐 때, 앞에 쓰인 게 출력됨

// example)
let userName = "양혜원";
let userNiceName = "winderLood";

let displayName = userName ?? userNiceName; // 유저 네임이 없으면 후자, 유저 네임이 있으면 유저 네임이 나오도록

// 2. typeof 연산자
// -> 값의 타입을 문자열로 변환하는 기능을 하는 연산자

let var7 = 1;
var7 ="hello"; // 타입 자주 바뀔 수 있음

let t1 = typeof var7; // String

// 3. 삼항 연산자
// -> 항을 3개 사용하는 연산자
// -> 조건식 이용해서 참, 거짓일 때의 값을 다르게 변환
let var8 = 10;

//요구사항 : 변수 res에 var8의 값이 짝수 -> "짝", 홀수 -> "홀"
let res = var8 % 2 ===0 ? "짝수" : "홀수";
```

## 5. 조건문

```jsx
// 1. if 조건문 (if문)
// 조건이 아닐 때 추가하고 싶은 사항이 있다면 else, 없으면 X.
// if로 시작해서 else로 끝나야 함.(or else없이)
let num=10;

if (num >= 10) {
    console.log("참입니다.");
}
else if (num>=9) {
    console.log("9이상입니다.");
}
else if (num>=3) {
    console.log("3이상입니다.");
}
else {
    console.log("값이 없습니다.");
}

// 2. Switch 문
// -> if문과 기능 자체는 동일
// -> 다수의 조건을 처리할 때 if보다 더 직관적이다.

let animal = "cat";

switch(animal) { // 비교하고 싶은 변수
    case "cat": {
        console.log("고양이");
        break; // break 안 쓰면 이 밑의 경우까지 다 출력됨 
    }
    case "dog": {
        console.log("개");
        break;
    }    
    case "bear": {
        console.log("곰");
        break;
    }
    default: {
        console.log("난 몰라");
    }
        
}
```

## 6. 반복문

```jsx
// for문
for(let idx = 0; idx<5; idx++){ // 초기식 = count식(몇번)
    console.log("반복!");

    if (idx%2===0) {
        continue;
    }

    // 조건식 손 안 대고 idx=3 이상일 때 멈추는 법
    // -> 중간에 강제로 멈추는
    if (idx>=3) {
        break;
    }
}
```

## 7. 함수

→ 중복으로 작성된 유사한 기능을 하는 코드를 해결하기 위해

```jsx
// 함수선언(함수를 새롭게 만드는 거)
function greeting() {
    console.log("Hello"); // 출력 안 됨. 함수 호출해야 함.
}
console.log("호출전");
greeting(); // 함수 호출
console.log("호출후");     // 호출 전 Hello 호출후

// 함수 (직사각형의 넓이 구하는)
function getArea(width, height) { // width, height = 매개변수
    let area = width *height;

    console.log(area);
}

getArea(10,20); // 10,20 = 인수!
getArea(30,20); //바꿔가면서 넘길 수 있음

//return(반환)
function getArea2(width2, height2) { 
    let area2 = width2 *height2;

    return area; 
    // 어떤 값 반환 후 바로 종료! return 문 밑에 뭐 써도 안 나옴.
}
let area1 = getArea2(20.10);
console.log(area1);

let area3 = getArea2(30.20);
console.log(area3);

//함수 안에 함수
function getArea(width, height) { 
    function another() {   //중첩 함수
        console.lot("another");
    }
    let area = width *height;

    console.log(area);
}

getArea(10,20); 
getArea(30,20); 

// 호이스팅 = 끌어올리다 (js만의 특징)
// 선언문을 호출문보다 아래에 둬도 위로 끌어올려져서 실행됨.
```

## 8. 함수 표현식과 화살표 함수

```jsx
function funcA(){ // 함수 선언문
    console.log("funcA");
}

let varA = funcA; //함수 자체를 변수에 담게 됨
varA(); // 따라서 이 함수를 변수를 이용해 호출 가능!

let varB = function funcB(){ // 함수 표현식
    console.log("funcB"); // 선언식X, 값으로서 함수가 생성된 것!, 호이스팅 X
};

varB(); 
funcB(); // 호출 불가! 값으로서 생성된 함수니까! funcA 형태여야 함!

// 2. 화살표 함수 
let varC = () => 1; //10             // 1을 반환하는 함수라는 뜻

varC = (Value) => Value + 1; // 11   // 매개변수 필요하면 괄호 안에 넣기
console.log(varC(10));

varC = (value) => {
    console.log(value); // 10
    return value+1;     // 11
};

console.log(varC(10));
```

## 9. 콜백 함수

= 자신이 아닌 다른 함수에 인수로서 전달된 함수

![Untitled](ch01_js%20basic%206df9da77a6304c92be38770dd3a846b6/Untitled%201.png)

```jsx
// 1. 콜백 함수 (main 함수가 원하는 언제든 실행 가능!), 자주 쓰임!!!!
function main(value) {
    console.log(1);
    console.log(2);
    value();
    console.log("end");
}

main(function sub(){ 
    console.log("I am sub");
}); // I am sub // main이 호출한 후 뒤에 자기가 자동으로 호출하는 거니까 '콜백'

// ===
main( () => {
    console.log("I am sub");
})

// 2. 콜백 함수의 활용
function repeat(count, callback){
    for (let idx=1; idx<=count; idx++) {
        callback(idx);
    }
}

repeat(5, (idx) => {
    console.log(idx);
})
repeat(5, (idx) => {
    console.log(idx*2);
})
repeat(5, (idx) => {
    console.log(idx*3);
})
```

## 10. 스코프(scope)

= 범위 

= 변수나 함수에 접근하거나 호출할 수 있는 범위

![Untitled](ch01_js%20basic%206df9da77a6304c92be38770dd3a846b6/Untitled%202.png)

```jsx
// 스코프
// -> 전역(전체 영역) 스코프 / 지역 스코프
// -> 전역 스코프 : 전체 영역에서 접근 가능
// -> 지역 스코프 : 특정 영역에서만 접근 가능

let a=1;        // 전역 스코프

function funcA(){
    let b=2;    // 지역 스코프
    console.log(a);
    function funcB() {} // 함수선언(지역스코프) -> 밖에서는 호출X, 함수 안에서만 지역스코프 가짐
}

funcA();
//console.log(b); -> 지역스코프는 영역 밖에서는 호출 불가

if (true) {
    let c=1; // 지역 스코프 ( {} 안에 있는 애들 = 지역 스코프)
    function funcC() {} // for문에서는 지역스코프 X
}
```

## 11. 객체 1

= 원시 타입이 아닌 객체 타입의 자료형

= 여러가지 값을 동시에 저장할 수 있는 자료형

- 객체 = 현실 세계에 존재하는 어떤 사물이나 개념 표현하기 쉬

![Untitled](ch01_js%20basic%206df9da77a6304c92be38770dd3a846b6/Untitled.png)

```jsx
// 1. 객체 생성
let obj1 = new Object() // 객체 생성자
let obj2 = {}; // 객체 리터럴 (대부분 사용)

// 2. 객체 프로퍼티 (객체 속성)
let person = {
    name : "양혜원", // key : value
    age : 22,
    hobby : "테니스",
    extra : {},
    "Like her":true, // 띄어쓰기 포함 문자열을 할 때는 "" 사용
};

// 3. 객체 프로퍼티를 다루는 방법
// 3.1. 특정 프로퍼티에 접근(점 표기법, 괄호 표기법)

// 점 표기법
let name = person.name;
// let name = person.name2; -> undefined

// 괄호 표기법
let age = person["age"] // 22 (큰 따옴표로 해야 함!)

let property = "hobby";
let hobby = person[property];

// 3.2 새로운 프로퍼티를 추가하는 법
person.job = "fe developer";
person["favoriteFood"] = "떡볶이";

// 3.3 프로퍼티 수정하는 법
person.job = "educator";
person["favoriteFood"] = "우동";

// 3.4 프로퍼티를 삭제하는 법
delete person.job;
delete["favoriteFood"];

//3.5 프로퍼티의 존재 유무를 확인하는 법 (in 연산자)
let result1 = "name" in person; //name이라는 key가 person에 있는가? -> 있으면 true, 없으면 false
let result2 = "cat" in person;

```

## 객체 2

```jsx
// 1. 상수 객체
const animal = {
    type: "고양이",
    name: "나비",
    color: "black",
};

// 프로퍼티 수정은 문제가 되지 않음
animal.age = 2; // 추가
animal.name = "까망이"; // 수정
delete animal.color; // 삭제

animal = 123; // 불가능

// 2. 메서드
// -> 값이 함수인 프로퍼티를 말함
// -> 객체의 동작을 정의함

const person = {
    name:"양혜원",
    // 메서드 선언
    sayHi() {
        console.log("안녕");
    }
};

person.sayHi();
person["sayHi"]();
```

## 12. 배열

= 여러개의 값을 순차적으로 담을 수 있는 자료

→ 중간에 값 바꿔가려고 쓰는 거!

```jsx
// 1. 배열 생성
let arrA = new Array(); // 배열 생성자
let arrB = []; // 배열 리터럴 (대부분 사용)

let arrC = [1,2,3, true, "hello", null, ()=>{}, {}, []]; // 어떤 거든 들어갈 수 있고, 길이 한계 X

// 2. 배열 요소 접근
let item1 = arrC[0];
let item2 = arrC[1];
console.log(item1, item2);

arrC[0] = "hello";
console.log(arrC);
```


##

# ch02. js basic(2)

## 1. Truthy & Falsy

js 에선 참, 거짓이 아닌 값도 참, 거짓으로 평가함

- truthy = 참 같은 값
- falsy = 거짓 같은 값

```jsx
// 1. Falsy한 값
let f1 = undefined;
let f2 = null;
let f3 = 0;
let f4 = -0;
let f5 = NaN;
let f6 = "";
let f7 = 0n; // (big integer라는 특수한 값)

if (!f1){
    console.log("falsy");  // falsy -> 참이니까 이렇게 출력
}

// 2. Truthy한 값
// -> 7가지 falsy한 값 제외 나머지 모든 값
let t1 = "hello"; //비어있지 않은 문자열
let t2 = 123; // 0이 아닌 수
let t3 = []; // 배열
let t4 = {}; // 객체
let t5 = () => {}; // 화살표함수 

// 3. 활용 사례1
function printName(person){ // 매개변수가 undefined를 받으면 X
    if (person===undefined || person === null){ // undefined를 받는지 아닌지 확인하도록!
        console.log("person의 값이 없음");
        return; // 밑으로 가지 못하게 여기서 끝냄
    }
    console.log(person.name);
}

let person = {name:"양혜원"};
// let person = null;이면 오류! if문에서 undefined인지만 확인하니까!
printName(person);

// if문 너무 복잡 -> sol)
function printName(person){ 
    if (!person){ 
        console.log("person의 값이 없음");
        return; 
    }
    console.log(person.name);
}

person = {name:"양혜원"};
printName(person);
```

## 2. 단락 평가

첫 번째 항만으로도 결과를 도출할 수 있다면, 후자는 고려하지 않음!

ex) 

![Untitled](ch02%20js%20basic(2)%20cb2877e1c6bb4c20b535a79d40f49735/Untitled.png)

```jsx
function returnFalse(){
    console.log("false 함수");
    return false;
}

function returnTrue(){
    console.log("True 함수");
    return true;
}

// 단락평가O
console.log(returnFalse() && returnTrue()); // False 함수( 두번째 피연산자에 접근할 필요 없어서 전자만!), false
// 단락평가X
console.log(returnTrue() && returnFalse()); // True 함수 False 함수 false
console.log(returnTrue() || returnFalse()); // True 함수 true

// function returnFalse(){
//     console.log("false 함수");
//     return undefined; //Falsy한 값
// }

// function returnTrue(){
//     console.log("True 함수");
//     return 10; 
// }

// console.log(returnFalse() && returnTrue()); // False 함수 undefined

// 단락 평가 활용 사례

function printName(person){
    console.log(person && person.name);
    // person이 undefined면 person만 접근함! (= if문과 같은 역할!)
    console.log(name || "Person의 값이 없음"); // 문자열이 true임
}

printName(); // undefined 입력하면 -> person의 값이 없음
printName({name:"양혜원"}); // 제대로 된 객체 입력하면 -> 양혜원(true || true -> 전자가 나옴!, true && true -> 후자)

```

## 3. 구조분해할당

= 배열이나 객체에 저장된 여러 개의 값들을 분해해서 각각 다른 변수에 할당하는 것

```jsx
// 1. 배열의 구조 분해 할당
let arr = [1,2,3];

let [one, two, three, four] = arr;
console.log(one, two, three, four); // 1, 2, 3, undefined

// 2. 객체의 구조 분해 할당
let person = {
    name: "양혜원",
    age: 22,
    hobby: "피아노",
};

let { name, age, hobby } = person;

let {
    age: myAge, 
    extra = "hello",
} = person;
console.log(name, myAge, hobby); // 변수가 age->myAge 됨!

// 3. 객체 구조 분해 할당을 이용해서 함수의 매개변수를 받는 방법
const func = ({name, age, hoby, extra}) => {
    console.log(name, age, hobby, extra);
};

func(person)
```

## 4. Spread 연산자 & Rest 매개변수

```jsx
// 1. Spread 연산자
// -> Spread = 흩뿌리다, 펼치다
// -> 객체나 배열에 저장된 여라개의 값을 개별로 흩뿌려주는 역할

let arr1 = [1,2,3];
let arr2 = [4, ...arr1, 5,6]; // ... = 사이에 흩뿌려라.. -> 4,1,2,3,5,6

let obj1 = {
    a:1,
    b:2,
};
let obj2 = {
    ...obj1,
    c:3,
    d:4,
};
console.log(obj2);  // a:1, b:2, c:3, d:4

// 함수 호출시에도 사용
function funcA(p1, p2, p3) {
    console.log(p1,p2,p3);
}
func(...arr1);

// 2. Rest 매개변수 (!= Spread)
// -> Rest는 나머지, 나머지 매개변수
function funcB(one, two, ...rest) { // 지정한 애들 빼고 나머지는 다 rest에 
    console.log(rest); // rest 대신에 원하는 이름으로 써도 ...만 붙으면 상관X
}

funcB(...arr1) // [1,2,3] 0:1 1:2 2:3
```

## 5. 원시타입 vs 객체 타입

- 원시 타입 : 값 자체로써 변수에 저장되고 복사된다. ex, Number, String, Boolean 등
    
    = 불변값 = 원본 데이터의 값은 변경되지 않음(메모리 값 수정X)
    
- 객체 타입 : 참조값을 통해 변수에 저장되고 복사된다. ex, Object, Array, Function 등
    
    = 가변값 = 원본 데이터의 값이 수정됨 (메모리 값 수정)
    
    주의사항] 
    
    1. 의도치 않게 값이 수정될 수 있다. → sol (깊은 복사)
    
    ![Untitled](ch02%20js%20basic(2)%20cb2877e1c6bb4c20b535a79d40f49735/Untitled%201.png)
    
    1. 객체 간 비교는 기본적으로 참조값을 기준으로 이루어진다.
    
    ![Untitled](ch02%20js%20basic(2)%20cb2877e1c6bb4c20b535a79d40f49735/Untitled%202.png)
    
    ![Untitled](ch02%20js%20basic(2)%20cb2877e1c6bb4c20b535a79d40f49735/Untitled%203.png)
    
    1. 배열과 함수도 사실 객체다.

## 6. 반복문으로 배열과 객체 순회

순회 = 배열, 객체에 저장된 여러개의 값에 순서대로 하나씩 접근하는 

```jsx
// 1. 배열 순회
let arr = [1,2,3];

// 1.1 배열 인덱스
for(let i=0; i<arr.length; i++){
    console.log(arr[i]);
}

let arr2 = [4,5,6,7,8];
for(let i=0; i<arr2.length; i++){
    console.log(arr2[i]);
}

// 1.2 for of 반복문 (index없이 순서대로 순회)
for(let item of arr){ // arr의 각 요소들을 item에! -> 나열됨
    console.log(item);
}

// 2. 객체 순회
let person = {
    name:"양혜원",
    age:22,
    hobby:"테니스",
};

// 2.1 Object keys 사용
// -> 객체에서 key 값들만 뽑아서 새로운 배열로 반환
let keys = Object.keys(person);

for (let i=0; i<keys.length; i++){
    console.log(keys[i]); // name age hobby
}

for (let key of keys){             // for of 는 배열!
    const value = person[key];
    console.log(key, value); // name 양혜원 age 22 hobby 테니스
}

// 2.2 Object.values
// -> 객체에서 value값들만 뽑아서 새로운 배열로 반환
let values = Object.values(person);
console.log(values);

for(let value of values){
    console.log(value); // 양혜원 22 테니스
}

// 2.3 for in (객체만을 위해 존재하는 특수 반복문)
for(let key in person){            // for in 은 객체!
    console.log(key); // name age hobby
    //console.log(key,value);
}
```

## 7. 배열 메서드

### 1. 요소 조작

```jsx
//6가지의 요소 조작 메서드

// 1. push
// 배열의 맨 뒤에 새로운 요소를 추가하는 메서드
let arr1 = [1,2,3];
const newLength = arr1.push(4,5,6,7); 

console.log(arr1); // 1,2,3,4,5,6,7
console.log(newLength); // 7

// 2. pop
// 배열의 맨 뒤에 있는 요소 제거 후 반환
let arr2 = [1,2,3];
const poppedItem = arr2.pop();

console.log(poppedItem); // 3
console.log(arr2); // [1,2]

// 3. shift  -> pop보단 느리게 동작
// 배열의 맨 앞에 있는 요소 제거 후 반환
let arr3 = [1,2,3];
const shiftItem = arr3.shift();
console.log(shiftItem, arr3); // 1, [2,3]

// 4. unshift  -> push보단 느리게 동작
// 배열의 맨 앞에 새로운 요소 추가하는 메서드
let arr4 = [1,2,3];
const newLength2 = arr4.unshift(0);
console.log(newLength2, arr4); // 4, [0,1,2,3]

// 5. slice
// 마치 가위처럼, 배열의 특정 범위를 잘라내서 새로운 배열로 반환
let arr5 = [1,2,3,4,5];
let sliced = arr5.slice(2,5); // 잘라낼 처음 값, 잘라낼 나중 값 + 1 => 2번에서 5 직전 4까지!
// === arr5.slice(2);
let sliced2 = arr5.slice(-1); // [5] -> 뒤에서부터 몇 개 자를지 쓰는 거!

console.log(sliced); // [3,4,5]
console.log(arr5); // [1,2,3,4,5] -> 원본은 변형X

// 6. concat
// 두 개의 서로 다른 배열을 이어 붙여서 새로운 배열을 반환
let arr6 = [1,2];
let arr7 = [3,4];

let concatedArr = arr6.concat(arr7);
console.log(concatedArr); // [1,2,3,4]
```

### 2. 순회와 탐색

```jsx
// 5가지 요소 순회 및 탐색 메서드
// 1. forEach
// 모든 요소를 순회하면서, 각각의 요소에 특정 동작을 수행시키는 메서드
let arr1 = [1,2,3];
arr1.forEach(function(item, idx, arr) { // 콜백함수(현재요소의 값, 현재 반복 카운트, 전체 배열)
    console.log(idx, item*2); // 0 2, 1 4, 2 6
}); 

let doubledArr = [];
arr1.forEach((item)=>{
    doubledArr.push(item*2); // [2,4,6]
});
console.log(doubledArr);

// 2. includes
// 배열에 특정 요소가 있는지 확인하는 그런 메서드
let arr2 = [1,2,3];
let isInclude = arr2.includes(10); // 찾으려는 값 괄호안에 넣어서 확인하기
console.log(isInclude); // false(없으면 f)

// 3. indexOf
// 특정 요소의 인덱스(위치)를 찾아서 반환하는 메서드
let arr3 = [1,2,3];
let index = arr3.indexOf(2); // 괄호 안에 찾고자 하는 값을 넣으면, 그 값의 인덱스 찾기 가능!
console.log(index); // 1
// if 찾고자 하는 값이 중복되면, 가장 첫번째로 나온 값의 인덱스 반환
// if 찾고자 하는 값 없으면, -1

let objectArr = [
    {name : "양혜원"},
    {name : "홍길동"},
];

// 간단한 거 찾을 때 (indexOf)
console.log(
    objectArr.indexOf({name:"양혜원"}) // -1 => X , indexOf는 얕은 비교(===)를 해서!
)                                      // -> 객체 비교 X

// 복잡한 거 찾을 때 (findIndex)
console.log(objectArr.findIndex(
    (item) => item.name === "양혜원" // -> 올바른 비교시 객체 비교 가능!
));

// 4. findIndex
// 모든 요소를 순회하면서, 콜백함수를 만족하는 그런(= 콜백함수가 참 반환)
// 특정 요소의 인덱스(위치)를 반환하는 메서드
let arr4 = [1,2,3];
const findedIndex = arr4.findIndex(
    (item)=>item % 2 !== 0 // 0 (만약 안 나오면 -1)
);
console.log(findedIndex);

// 5. find
// 모든 요소 순회하면서 콜백함수를 만족하는 요소 찾는데, 요소 그대로 반환
let arr5 = [
    {name:"양혜원"},
    {name:"홍길동"},
];

const finded = arr5.find(
    (item)=>item.name === "양혜원"
);
console.log(finded); // {name: "양혜원"} -> 객체 그대로 반환!
```

### 3. 변형

```jsx
// 5가지 배열 변형 메서드
// 1. filter
// 기존 배열에서 조건을 만족하는 요소들만 필터링하여 새로운 배열로 반환

let arr1 = [
    {name:"양혜원", hobby : "테니스"},
    {name:"양효원", hobby : "테니스"},
    {name:"오해원", hobby : "독서"},
];

const tennisPeople = arr1.filter((item)=> {
    if(item.hobby === "테니스") return true;
    // === (item) => item.hobby === "테니스"
});

console.log(tennisPeople); // 2개 요소만 나옴!

// 2. map
// 배열의 모든 요소 순회하면서, 각각 콜백함수를 실행하고 그 결과값들을 모아서 새로운 배열로 반환
let arr2 = [1,2,3];
const mapResult1 = arr2.map((item, idx, arr) => {
    return item*2; // 새로운 배열로 반환!
});

let names = arr1.map((item)=> item.name);
console.log(names); // "양혜원", "양효원", "오해원" -> 원하는 프로퍼티만으로 배열 생성!

// 3. sort (원본 배열 자체 변경)
// 배열을 사전 순으로 정렬하는 메서드
let arr3 = ["b","a","c"];
arr3.sort(); // ['a', 'b', 'c']

let arr4 = [10,3,5];
arr4.sort((a,b) => {
    if (a>b){
        //b가 a 앞에 와라
        return 1; // sort에서 양수를 반환-> b가 a 앞으로!
    }
    else if (a<b){
        // a가 b 앞에 와라
        return -1; // 음수면 sort에서 a가 b 앞으로
    }
    else {
        // 두 값의 자리를 바꾸지 마라
        return 0; 
    }
});

// 4. toSorted
// 배열의 모든 요소를 하나의 문자열로 합쳐서 반환하는 그런 메서드
let arr6 = ["hi", "im", "winterlood"];
const joined = arr6.join(" ");
console.log(joined); // hi im winterlood
```

## 10. Date 객체와 날짜

```jsx
// 1. Date 객체를 생성하는 법
let date1 = new Date(); // 생성자 -> 비어있는 건 현재시간 출력!

let date2 = new Date("1997/01/07/10:00:10"); // -, ., / 로 날짜 구분 가능!
// 1997, 1, 7, 23, 59, 59 도 가능!

// 2. 타임 스탬프
// 특정 시간이 "1970.01.01 00시 00분 00초"로부터 몇 ms가 지났는지를 의미하는 숫자값
let ts1 = date1.getTime();
//console.log(ts1); // 1705411155293ms가 지난 시간이 저장되어있다!

let date4 = new Date(ts1); // date4에는 date1과 동일한 시간이 저장되어있음
//console.log(date1, date4);

// 3. 시간 요소들을 추출하는 방법
let year = date1.getFullYear();
let month = date1.getMonth() + 1;  // 1월:0, 2월:1, 3월:2
let date = date1.getDate();

let hour = date1.getHours();
let minute = date1.getMinutes();
let seconds = date1.getSeconds();

console.log(
    year,
    month,
    date,
    hour,
    minute,
    seconds
);

// 4. 시간 수정하기
date1.setFullYear(2023);
date1.setMonth(2); // js에서 월은 0부터 시작! -> 실제로는 3월
date1.setDate(30);
date1.setHours(23);
date1.setMinutes(59);
date1.setSeconds(59); 

console.log(date1); // Thu Mar 30 2023 23:59:59

// 5. 시간을 여러 포맷으로 출력하기
console.log(date1.toDateString()); // 시간 제외 날짜 출력! -> Thu Mar 30 2023
console.log(date1.toLocaleString()); // 우리나라 현지 형식으로 출력 -> 2023. 3. 30 오후 11:59:59
```

## 11. 동기와 비동기

- 동기 = 여러개의 작업을 순서대로 한번에 하나씩만 처리하는 방식
    
    → 쓰레드 = 작업을 직접 처리하고, 실행하는 거
    
    → 동기적으로 처리한다.
    
    → 기본적으로 js는 동기적으로 코드를 실행한다.
    
---

# ch03.Node.js

## 1. Node.js

Node.js = Js 실행 환경(Run time) = 구동기 (게임기처럼)

→ 웹 서버, 모바일 앱, 데스크톱 앱 만들기 가능!!

→ React.js, Next.js, Vue.js, Svelte → Node.js 기반

- 패키지 = Node.js에서 사용하는 프로그램의 단위
- tip : VS code 자체 터미널 여는 법 = ctrl + J
    
    → 작업 경로는 현재 섹션의 내부가 됨!
    
- npm init = 새로운 패키지 생성해달라
- npm run 지정한 이름 : 복잡한 경로를 간단하게 노드로 실행 가능

## 2. Node.js 모듈 시스템 이해하기

- **모듈 시스템** = 모듈을 다루는 시스템
    
    =  모듈을 생성하고, 불러오고, 사용하는 등의 모듈을 다루는 다양한 기능을 제공하는 시스템
    
    → js의 모듈 시스템
    
    1. Common JS(CJS) / 2. ES Module(ESM) / 3. AMD / 4. UMD / …
- **모듈** =
    
    ex, 온라인 쇼핑몰 홈페이지
    
    회원 관리 기능 - user.js (user 모듈)
    
    장바구니 기능 - cart.js (cart 모듈)
    
    결제 기능 - payment.js (payment 모듈)
    
-

</br>

### 질문
