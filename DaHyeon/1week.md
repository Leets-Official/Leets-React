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

# 자바스크립트 개념 정리

**`자료형`**

1. 원시 타입(primitive type) 
    1. number, string, null, undefined, boolean  
    2. symbol, BigInt 
        1. symbol : 코드 내에서 유일한 값을 가진 변수 이름을 만들 때 사용 , 어떤 값과 비교해도 true가 될 수 없는 고유한 변수
        2. BigInt : 아주 큰 정수를 표현할 때 사용
            1. 소수 표현에는 사용할 수 x 
            2. BigInt 타입끼리만 연산 O , 서로 다른 타입끼리의 연산은 명시적으로 타입 변환을 해야함
2. 객체 타입(reference type) 
    1. 배열, 객체 , 함수 

📌 자바스크립트에서 함수는  객체 취급하지만 함수에 typeof 연산자를 사용하면 function이라는 값을 리턴

<aside>
💡 자바스크립트는 연산할 때 상황에 따라 데이터 타입이 유연하게 변한다 !

</aside>

🚩 기본형 값(원시 타입)을 변수에 담아 사용할 때는 값이 그대로 할당된다 

→ 값에 의한 전달

<aside>
💡 서로 다른 메모리 공간에 저장된 별개의 값이기 때문에 어느 한쪽에서 재할당을 통해 값을 변경하더라도 영향을 주지 않는다

</aside>

🚩 참조형 값을 변수에 담아 사용할 때는 해당 객체를 가리키는 주소값이 할당된다 

→ 참조에 의한 전달

참조형(객체 타입)의 경우 변수를 통해 다른 변수에 할당하면 값 자체가 복사되는 것이 아니라 주소값이 복사되기 때문에 결국 같은 객체를 가리키게 되고 한쪽을 수정하면 다른 한쪽도 같이 수정이 된다 → 두 개의 식별자가 하나의 객체를 공유한다

<aside>
💡 저장된 메모리 주소는 다르지만 동일한 객체 값을 가지므로 어느 한쪽에서 객체를 변경하면 서로 영향을 주고 받는다

</aside>

[추가 문법 (모던 자바스크립트)](https://www.notion.so/640ea09282d24df9b9e35e88887b9759?pvs=21) spread 문법 활용 시 쉽게 복사 가능 

```jsx
let x = ['Kim', 'Na', 'Park', 'Lee'];
let y = x;  // y =  ['Kim', 'Na', 'Park', 'Lee'];

y.push('Lim');  //  ['Kim', 'Na', 'Park', 'Lee','Lim'];
x[4] = 'Sung';  // x = ['Kim', 'Na', 'Park', 'Lee','Lim']; 
								// x = ['Kim', 'Na', 'Park', 'Lee','Sung'];
console.log(y);
```

```jsx
let x = {
  numbers: [1, 2, 3, 4],
  title: 'Codeit',
};
let y = x.numbers;  // y = [1,2,3,4]
let z = x.title;    // z = 'Codeit'
 
x.numbers.unshift(5); // x.numbers = [5,1,2,3,4] ===y
x.title = 'Hello';     // x.title = 'Hello' 문자열

console.log(y);
console.log(z);
```

---

```jsx
let team1 = ['Drum', 'Bass', 'Saxophone'];
const team2 = team1;
// 배열은 참조형 값이기 때문에 주소 값이 복사되어 team1과 
// team2가 서로 같은 배열을 가리키고 있음 

team1.splice(2, 1, 'Trumpet');
// team1 = ['Drum', 'Bass', 'Trumpet'];
// team2 = ['Drum', 'Bass', 'Trumpet'];

team2.splice(2, 1, 'Piano');

console.log(team1);  //['Drum', 'Bass', 'Piano'];
console.log(team2);  //['Drum', 'Bass', 'Piano'];
```

- const는 무조건 재할당이 안된다?
    - const 키워드로 변수를 선언하게 되면 값을 재할당할 수 없지만, 할당된 값이 객체나 배열일 경우 메소드를 통해 그 값을 변경할 수 있다

 **`형 변환`** 

1. Boolean 형변환 
    1. 불린형으로 변환할 때는 보통 true가 나오지만 
        
        빈문자(’ ’),0, NaN, null , undefined는 false로 변환된다 
        
        ex) Boolean(”false”)  ⇒ true
        
        Boolean(6%2) ⇒ false 
        
        Boolean(NaN) || Boolean(’0’) ⇒ false || true ⇒ true 
        
        Boolean(typeof false) ⇒ Boolean(’boolean’) ⇒ true
        

**`null과 undefined`**

 1.null : 의도적으로 표현할 때 사용하는 값 

⇒ 의도적인 없음!

1. undefined: 값이 없다는 것을 확인하는 값
    
    ⇒ 처음부터 없음!
    

```jsx
console.log( null == undefined)   //true 
console.log( null === undefined)  // false
```

```jsx
let x;
console.log(x);   // undefined
let y = x;        // y= undefined, x= undefined
x = null;        
console.log(y);  // undefined
console.log(x);  // null
x = y;
console.log(x);  // undefined
```

```jsx
let x;
let y = null;

console.log(x === y);     // false
console.log(x == y);      // true
console.log(x == null);   // true
console.log(y === undefined);   // false
```

- 상수
    - 상수는 let이 아닌 const로 표현 가능
        - 보통 대문자와 _를 사용하여 선언
            - ex) const MY_NUMBER

`**7장. 연산자**`

1. 삼항 조건 연산자와 if…else문 
    1. if문은 표현식이 아닌 문이기 때문에 값을 사용할 수 없다 
    2. 삼항 조건 연산자 표현식은 값으로 평가할 수 있는 문이다. 
    
    ⇒ 조건에 따라 어떤 값을 결정하여 변수에 할당하는 경우  if…else문보다 삼항 조건 연산자 표현식을 사용하는 편이 유리하다. 하지만 조건에 따라 수행해야 할 문이 하나가 아니라 여러 개라면 if…else문의 가독성이 더 좋다.
    
    c. 경우의 수가 세가지라면 
    
    ```jsx
    let num = 2;
    
    let kind = num ? ( num > 0 ? '양수':'음수') :'영';
    ```
    

- 직접적으로 작성되는 값은 변수로 추상화하는 것이 가독성과 유지 보수 측면에서 더 좋다 .
    
    ex) 
    
    ```jsx
    function checkHeight(height) {
      const LIMIT = 140;
      let passMessage = '탑승이 가능합니다.';
      let failMessage = '탑승이 불가능합니다.';
    
      if (height >= LIMIT) {
        console.log(passMessage);
      } else {
        console.log(failMessage);
      }
    }
    ```
    
1. 지수 연산자
    1. 지수 연산자가 도입되기 이전에는 Math.pow 메서드를 사용
    2. 지수 연산자의 결합 순서는 우항에서 좌항이다
    
    ```jsx
    // 지수 연산자
    2 ** 2; //4
    2 ** 0; // 1
    2 ** -2 // 0.25
    
    2 ** ( 3 ** 2 ) // 512
    ```
    

**`8장. 제어문`**

1. switch 문 
    1. switch문의 표현식은 불리언 값보다 문자열이나 숫자 값인 경우가 많다. 
    2. switch문은 값들을 비교할 때 자료형을 엄격하게 구분한다
        1. if…else문은 논리적 참,거짓으로 실행할 코드 블록 결정, 
            
            switch문은 다양한 상황(case)에 따라 실행할 코드 블록 결정
            
            if문으로 대체할 때는 반드시 등호 세 개를 사용해 일치 비교를 해야한다
            

1. for 문 
    1. 초기화 부분에서 생성한 변수는 for문의 로컬 변수이다 
    2. 초기화 부분을 반드시 채울 필요는 없다
        1. 단, 세미콜론은 생략할 수 없다
            1. ex) for ( ; i =10; i++ ) 
    3. 추가 동작 부분도 꼭 채울 필요는 없다
    4. 무한루프
        
        ```jsx
        for(;;) { ... }
        ```
        
    5. 중첩 for문
        
        ex) 두 개의 주사위를 던졌을 때 두 눈의 합이 6이 되는 모든 경우의 수 출력하기
        
        ```jsx
        // [1,5] , [2,4] , [3,3,] , [4,2] , [5,1]
        
        for(let i = 1; i<=6; i++){
        	for(let j=1; j<=6; j++){
        		if(i+j === 6) console.log(`[${i},${j}`);
        	}
        }
        ```
        

1. while문 
    1. 주어진 조건식의 평가 결과가 참이면 코드 블록을 계속해서 반복 실행
        1. while문은 조건식이 true일때만 실행 !!
    2. for문은 반복 횟수가 명확할 때 주로 사용하고 
        
        while문은 반복 횟수가 불명확할 때 주로 사용
        
    3. 무한루프 
        
        ```jsx
        while(true){ ... }
        ```
        

**`break와 continue`**

1. break
    1. 현재 실행 중인 반복문을 완전히 종료한다
2. continue 
    1. 현재 실행 중인 반복문의 루프를 멈추고 다음 루프를 실행한다
    2. 반복문을 완전히 종료하는 것이 아니라 for문이라면 for문이라면 추가 동작 부분(업데이트 표현식)으로 넘어가고 while문의 경우 다시 조건으로 넘어간다

```jsx
for (let i = 1; i <= 50; i++) {
  if (i % 2 !== 0) {  // 홀수인 경우 continue
    continue;
  }
  console.log(i);
  i++;
}
```

→ 1)반복문이 시작하자마자 if문이 수행되어 continue 실행.  

2) 추가 동작 부분으로 넘어가 i가 1 증가 

3) 현재 i = 2 . if문을 건너뛰고 console.log 출력 후 i++에 의해  i가 1 증가 

4) 추가 동작 부분에서도 i가 증가하면서 for문이 반복할 때마다 2씩 증가하게 된다

5) 결국 i는 계속해서 짝수가 된다. 

**`9장. 타입 변환과 단축 평가`**

1. 단축 평가 (단락 평가)
    1. true || anything  : true
    2. false || anything  : anything 
    3. true && anything : anything
    4. false && anything : false

- 단축 평가는 if문을 대체할 수 있다. 어떤 값이 참일때 무언가를 해야한다면
    
    논리곱(&&)연산자 표현식으로 if문을 대체할 수 있다 
    
    ```jsx
    let done = true;
    let message = '';
    
    //주어진 조건이 true일 때
    if(done) message = '완료';
    
    //done이 true라면 message에 '완료'를 할당 
    message = done && '완료'
    console.log(message);
    
    ```
    

`**10장. 객체 리터럴**` 

1. 객체란? 
    1. 자바스크립트는 객체 기반 프로그래밍 언어, 자바스크립트를 구성하는 거의 “모든 것”이 객체이다.
    2. 객체는 0개 이상의 프로퍼티로 구성된 집합. 프로퍼티는 키와 값으로 구성 
        
         
        
        ```jsx
        let person = {
        	name:'Lee',   // 프로퍼티 
        	age:20//값        // 프로퍼티 
        	//->키
        };
        ```
        

1. 메서드 
    1. 자바스크립트에서 사용할 수 있는 모든 값은 프로퍼티 값으로 사용할 수 있다.
    2. 따라서 함수는 값으로 취급할 수 있기 때문에 프로퍼티 값으로 사용할 수 있다 
        1. 프로퍼티 값이 함수일 경우 일반 함수와 구분하기 위해 메서드라 부른다
2. 프로퍼티 접근 
    1. 마침표 표기법
    2. 대괄호 표기법 
    
    ```jsx
    let person = {
    	name:'Lee'
    };
    
    //마침표 표기법에 의한 프로퍼티 접근 
    console.log(person.name)  //Lee
    
    //대괄호 표기법 
    console.log(person['name']);
    ```
    
    ⇒ 대괄호 표기법을 사용하는 경우 대괄호 프로퍼티 접근 연산자 내부에 지정하는 프로퍼티 키는 반드시 따옴표로 감싼 문자열이어야 한다.
    
    ⚠️  파라미터로 다른 변수에 담긴 값을 가져올 때는 대괄호 표기법을 사용해야한다
    
    ```jsx
    let myVoca = {
      // 코드를 작성해 주세요.
      addVoca: function (key, value) {
        myVoca[key] = value;
    		// 점 표기법으로 key값에 접근을 하게 되면 , 
    		// 파라미터 key를 가리키는 것이 아니라,
    		// myVoca에 문자 그대로 key라는 프로퍼티 이름을 가진 
    		// 프로퍼티 값에 접근하는 것과 같은 의미가 된다
      },
    };
    
    // addVoca메소드 테스트 코드
    myVoca.addVoca('parameter', '매개 변수');
    myVoca.addVoca('element', '요소');
    myVoca.addVoca('property', '속성');
    console.log(myVoca);
    
    // deleteVoca메소드 테스트 코드
    myVoca.deleteVoca('parameter');
    myVoca.deleteVoca('element');
    console.log(myVoca);
    
    // printVoca메소드 테스트 코드
    myVoca.printVoca('property');
    ```
    
    ```jsx
    let person = {
    	'last-name':'Lee',
    	 1:10
    };
    
    person.'last-name';  //SyntaxError
    person.last-name;    // 브라우저 환경:NaN 
    										// node.js 환경:undefined
    										// person.last 를 먼저 평가 -> person 객체에는 키가 last인 프로퍼티가 없음.
    										// -> undefined -> 다음으로 name이라는 식별자 찾음 -> node.js 환경에는 현재 어디에도 name이라는 식별자 선언이 없음
    										 // -> undefined -> 그러나 브라우저 환경에서는 name이라는 전역변수가 암묵적으로 존재
    
    person.[last-name];  //undefined
    person.["last-name']  // Lee
    
    // 프로퍼티가 숫자로 이루어진 문자열의 경우 따옴표 생략 가능 
    person.1;  // Error: unexpected number
    person.'1' // Error: unexpected string
    person[1]  // 10
    person['1']  //10
    ```
    
3. 프로퍼티 삭제 
    1. delete 연산자는 객체의 프로퍼티를 삭제한다
        1. 존재하는 프로퍼티만 삭제할수 있다 

1. 프로퍼티 존재 여부 
    1. in을 통해 프로퍼티가 객체에 존재하는지 확인할 수 있다
        1. ex) console.log(’name’ in codeit)
2. 객체 리터럴의 확장 기능 (ES6에서 추가)
    1. 프로퍼티 축약 표현
    2. 계산된 프로퍼티 이름 
    3. 메서드 축약 표현 
        
        ```jsx
        let obj = {
        	name:'Lee',
        sayHi: function(){
        	console.log('Hi! '+ this.name);
        }
        }
        
        obj.sayHi() // Hi! Lee
        ```
        
        ```jsx
        let obj = {
        	name:'Lee',
        	sayHi(){
        	console.log('Hi! '+ this.name);
        }
        }
        
        obj.sayHi() // Hi! Lee
        ```
        
        `**for…in 문**`
        
        - for…in 문은 객체 내부에 있는 모든 프로퍼티들을 하나씩 다룰 수 있다.
        - 배열보다는 객체를 다루는 데 좀 더 최적화되어 있다
            
            → 배열에 사용하지 않는 것을 권장 
            
        
        ⚠️ 예외사항 
        
        - 객체의 프로퍼티 정렬 순서
            - 객체는 정수형 프로퍼티 네임을 오름차순으로 먼저 정렬하고, 나머지 프로퍼티들은 추가한 순서대로 정렬하는 특징이 있다.
            
            ```jsx
            let myObject = {
              3: '정수3',
              name: 'codeit',
              1: '정수1',
              birthDay: '2017.5.17',
              2: '정수2',
            };
            
            for (let key in myObject) {
              console.log(key);
            }
            
            //결과값
            1
            2
            3
            name
            birthDay
            
            let myObj = {
            	1.2:'a',
            	300:'b',
            	2:'c'
            }
            // 2 300 1.2순으로 출력 
            ```
            
            - 숫자형 프로퍼티 네임
                - 숫자형 프로퍼티가 사용될 때는 문자열로 형변환이 되어 사용된다
                - 대괄호 표기법으로만 접근이 가능
                
        
        **`Date 객체`**
        
        - getTime()
            - 1970 년 1 월 1 일 00:00:00 UTC와 주어진 날짜 사이의 경과 시간 (밀리 초)을 나타낸다
        
        < Date 객체 정보 수정하기 >
        
        1. set 으로 시작하는 메서드
            
            (대괄호로 감싸진 요소들은 선택적인 요소) 
            
            1. setFullYear(year,[month],[date])
            2. setMonth(month,[date])
            3. setDate(date)
            4. setHours(hour,[min],[sec],[ms])
            5. setMinutes(min,[sec],[ms])
            6. setSeconds(sec,[ms])
            7. setMiliseconds(ms)
            8. setTime(miliseconds)
                
                → 1970년 1월 1일 00:00:00 UTC부터 밀리초 이후를 나타내는 날짜를 설정 
                
                ```jsx
                let myDate = new Date(2017, 4, 18, 19, 11, 16);
                
                myDate.setFullYear(2002);
                myDate.setMonth(6);
                myDate.setDate(20);
                ```
                
            
            2. 시간 정보 알아내기 
            
            1. toLocaleDateString()
            2. toLocaleTimeString()
            3. toLocaleString()
            
            → 사용자의 브라우저에 설정된 국가의 표기에 맞춰 날짜와 시간을 보여준다 
            
            1. 지금 이 순간 
                1. Date.now()
                
                → 이 메소드가 호출된 시점의 타임스탬프를 반환 
                
                😃 새로운 객체를 만들지 않아도 바로 현 시점의 날짜 값을 얻어낼 수 있다 !
                
            2. Date 객체의 형변환 
                1. Date 객체의 자료형은 object(객체) 
                2. Date 객체를 boolean 타입으로 변환하면 true가 되고, string타입으로 변환하면 날짜값이 그대로 문자열로 변환 
                3. number 타입으로 변환할 경우 getTime() 메소드를 활용한 것과 똑같은 수치의 타임스탬프 값이다 
                
                ```jsx
                let myDate = new Date(2017, 4, 18);
                
                console.log(typeof myDate); // object
                console.log(String(myDate)); // Thu May 18 2017 00:00:00 GMT+0900 (Korean Standard Time)
                console.log(Number(myDate)); // 1495033200000
                console.log(Boolean(myDate)); // true
                ```
                
                → Date 객체끼리 사칙 연산도 가능하다 
                
                ```jsx
                let myDate1 = new Date(2017, 4, 18);
                let myDate2 = new Date(2017, 4, 19);
                
                let timeDiff = myDate2 - myDate1;
                console.log(timeDiff); // 86400000 (ms)
                console.log(timeDiff / 1000); // 86400 (sec)
                console.log(timeDiff / 1000 / 60) // 1440 (min)
                console.log(timeDiff / 1000 / 60 / 60) // 24 (hour)
                console.log(timeDiff / 1000 / 60 / 60 / 24) // 1 (date)
                ```
                
            3. 날짜를 표현하는 문자열 
                
                ```jsx
                let date1 = new Date('12/15/1999 05:25:30');
                let date2 = new Date('December 15, 1999 05:25:30');
                let date3 = new Date('Dec 15 1999 05:25:30');
                ```
                
            
            **`배열`**
            
            1. 배열도 객체이다 
            2. 배열의 메소드/ 내장 함수
                1. splice : 특정 인덱스값 삭제/추가 하기 
                    1. splice(startIndex, deleteCount,item) 
                    
                    ```jsx
                    let members = ['안녕', '야호','딸기',
                    '키위','바나나']
                    
                    members.splice(1,1,'복숭아','수박')
                    // 안녕, 복숭아, 수박, 딸기, 키위, 바나나 
                    
                    member.splice(1,0,'메론','토마토')
                    // 안녕, 메론, 토마토, 야호 ,딸기, 키위 ,바나나  
                    ```
                    
                
                ⚠️ 반복문을 통해 요소를 삭제할 때는 index의 변화에 유의
                
                ex) numbers[0] 이 제거되면 1번 인덱스에 있던 요소가 0번 인덱스로 당겨지고 2번 인덱스가 1번 인덱스로 당겨진다. 
                
                → 일반적으로 반복문에서 계속 i 를 증가시켜주게 되는데 , 요소를 삭제할 때 만큼은 i가 증가하지 않도록 방법을 고민해야 한다
                
                b. pop() : 배열의 마지막 요소를 삭제
                
                c. shift() : 배열의 첫 요소를 삭제
                
                d. unshift() : 배열의 첫 요소로 값 추가 
                
                - shift와 unshift는 pop, push에 비해 비교적 느리게 동작함
                
                e. push() : 배열의 마지막 요소로 값 추가 
                
                - 변환된 배열의 길이 반환
                
                ```jsx
                function range(start, count, step) {
                  let arr = []; // 빈 배열 선언 
                
                  for (let i = 0; i < count; i++) {  // i는 0부터 9까지 10번 
                    arr.push(start + i * step)   // 1 + 0*3 = 1 
                																 // 1 + 1 * 3 = 4 
                																// 1 + 2 * 3 = 7 
                  }
                
                  return arr;
                }
                
                // 테스트 코드
                console.log(range(1, 10, 3));
                
                // 1,4,7,10,13,16,19,22,25,28
                ```
                
                f. indexOf() , lastIndexOf() : 배열에서 특정 값 찾기 
                
                indexOf() 
                
                - 만약 해당 item이 포함되어 있다면 item이 있는 인덱스가 리턴
                - 포함되어 있지 않다면 , -1 리턴
                - 여러 번 포함되어 있으면, 처음 발견된 인덱스가 리턴
                - 얕은 비교로 동작
                    - 객체값들은 참조값을 기준으로 비교하므로 indexOf로는 배열에서 특정 객체값이 존재하는지 사용할 수 없음
                    - → findIndex() 사용
                
                lastIndexOf() 는 indexOf와 반대로 탐색을 뒤에서부터 
                
                g. includes() : 배열에서 특정 값이 있는지 확인하기
                
                - 해당 item이 배열에 있으면 true, 없으면 false를 리턴
                
                h. reverse() : 배열 뒤집기 
                
                i. concat() : 두 개 이상의 배열을 병합할 때 사용, 배열을 합친 복사본 배열을 반환 
                
                j. slice() : 인자로 지정된 배열의 부분을 복사하여 반환, 원본 배열은 삭제되지 않음
                
                → slice(start,end) 
                
                - end는 포함되지 않음
                
                k. join() : 배열 요소 사이에 원하는 문자를 삽입한 문자열을 반환
                
                l. findIndex() : 모든 요소를 순회하면서  콜백함수를 만족하는 , 특정 요소의 인덱스(위치)를 반환하는 메서드
                
            
            **`for…of`** 
            
            - for…of 반복문의 기본 문법
                - for ( 변수 of 배열) {
                    
                    동작 ;
                    
                    }
                    
            
            ```jsx
            let arr = [1, 2, 3];
            
            for (let el of arr) {
              console.log(el);
            }
            // 1 
            // 2 
            // 3 
            ```
            
            `forEach`
            
            [고차함수 ](https://www.notion.so/d4c6797b681b4520b8c44f892deca101?pvs=21) 
            
            - 모든 요소를 순회하면서 , 각각의 요소에 특정 동작을 수행시키는 메서드
            - 배열의 모든 요소를 한번씩 순회하면서 콜백함수로 해당 요소를 이용해서 무언가 동작을 수행하게 할 수 있음
            
            ```jsx
            let arr1 = [1,2,3]
            
            arr1.forEach(function(item,idx,arr){
                console.log(idx,item*2)
            })
            
            let doubledArr = [];
            
            arr1.forEach((item) => {
              doubledArr.push(item * 2);
            });
            console.log(doubledArr);
            ```
            
            **`숫자형 메소드`**
            
            1. toString()  : 파라미터로 전달하는 숫자의 진법으로 숫자를 변환해주는 메소드 
                1. 2를 전달하면 2진수, 8을 전달하면 8진수로 변환
                2. 변환한 다음 문자열로 리턴
                
                ```jsx
                let myNumber = 255;
                
                console.log(myNumber.toString(2));
                console.log(myNumber.toString(8));
                
                // 11111111
                // 377
                ```
                
            2. toFixed()  : 파라미터에 전달된 값만큼의 소수점 자릿수를 고정적으로 표기하는 메소드
                1. 파라미터에 전달된 값보다 소수점 자릿수가 더 많은 경우에는 바로 다음 자릿수에서 반올림
                2. 문자열이 리턴되기 때문에 숫자 값이 필요하면 반드시 숫자형으로 형변환해야 한다
            3. 지수표기법 : 알파벳 e를 활용해서 표기하는 방식 
                1. e의 왼쪽에 있는 숫자에 오른쪽에 있는 수만큼 10의 거듭제곱을 곱하는 의미 
                2. 오른쪽 값이 음수일 경우 이 숫자만큼 10의 거듭제곱으로 나누는 의미
                
                ```jsx
                let myNumber = 2.37e-2
                // 0.0237
                console.log(myNumber.toFixed(2));
                
                // 0.02
                ```
                
            
            **`Math 객체`**
            
            1. Math.abs() :  절댓값 
            2. Math.max() : 최댓값 
                1. 파라미터로 여러 수를 넘겨주면 그중 가장 큰 값이 리턴 
            3. Math.min() : 최솟값 
            4. Math.pow() : 거듭제곱 ( exponentiation) 
                1. Math.pow(2,3) // 8
            5. Math.sqrt() : 제곱근 ( square root)
                1. Math.sqrt(25) //5
            6. Math.round() : 반올림 
                1. Math.round(2.3)  //2
                2. Math.round(2.6) //3
            7. Math.floor() : 버림 
            8. Math.ceil() : 올림 
            9. Math.random() : 난수 
                1. 0 이상 1 미만의 값이 랜덤으로 리턴 
                
            
            📌   **문자열과 배열**
            
            - 문자열도 생각해보면 ‘문자’+’열’ 이기 때문에 배열과 비슷한 부분이 많다 ( 문자열은 유사 배열 객체 )
                - 비슷한 점
                    - 배열과 문자열 모두 length 프로퍼티를 가지고 있고 대괄호 표기법으로 각 요소에 접근할 수 있다.
                    - for …of 문을 문자열에도 활용할 수 있다
                - 다른 점
                    - 자료형이 다르다
                        - string은 string , array는 object
                    - mutable vs immutable
                        - 배열은 mutable(바뀔 수 있는) 자료형인 반면, 문자열은 immutable(바뀔 수 없는) 자료형이다
                            
                            → 배열은 요소에 접근해서 할당 연산자를 통해 요소를 수정할 수 있으나 문자열은 한 번 할당된 값을 수정할 수 없다 
                            
                            → 문자열에는 splice와 같은 메소드들은 사용할 수 없다
                            
            
            **`함수`** 
            
            1. 함수 선언 방식 
                1. 함수 선언식 
                    
                    ```jsx
                    function sayHi(){
                    	console.log("hi!")
                    }
                    ```
                    
                2. 함수 표현식
                    
                    ```jsx
                    let sayHi = function(){
                    	console.log("Hi!")
                    }
                    ```
                    
                3. 함수 선언식과 함수 표현식의 차이 
                    1. 호이스팅
                        - 함수 선언식은 호이스팅으로 인해 함수를 선언하기 이전에 함수를 호출해도 정상적으로 동작한다.
                        - 함수 표현식은 반드시 변수가 선언된 이후에 함수를 호출해야 정상적으로 동작한다.
                    2. 스코프 
                        - 함수 선언식은 함수 스코프를 가진다.
                        - 함수 표현식은 변수에 할당하는 경우에는 할당된 변수의 특성에 따라 스코프가 결정된다.
                            
                            → var 키워드 변수에 할당하면 함수 스코프, let 이나 const 키워드 변수에 할당하면 블록 스코프를 가진다. 
                            
            
            ---
            
            ```jsx
            const x = 5;
            
            if (x < 5) {
              const printHi = function () {
                console.log('Hi!');
              };
            }
            
            printHi();
            
            //에러 발생
            ```
            
            → printHi() 함수는 함수 표현식으로 선언되었다. 그래서 블록 스코프를 가지므로 if문 밖에서 사용할 수 없다. ( 그러나, var 키워드로 선언했다면 함수 스코프를 가진다)
            
            d. 즉시 실행 함수 
            
            ```jsx
            (function () {
              console.log('Hi!');
            })();
            ```
            
            - 함수 선언 부분을 소괄호로 감싼 다음에 바로 뒤에 함수를 실행하는 소괄호를 한번 더 붙여주는 방식
            - 일반 함수처럼 파라미터를 작성하고, 함수를 호출할 때 아규먼트를 전달할 수도 있다.
                
                ex) 
                
                ```jsx
                (function (x, y) {
                  console.log(x + y);
                })(3, 5);
                ```
                
                ❗그러나 , 즉시 실행 함수는 함수에 이름을 지어주더라도 외부에서 재사용할 수 없다. 그래서 일반적으로 이름이 없는 익명 함수를 사용.
                
            - 즉시 실행 함수의 활용
                - 프로그램의 초기화 기능에 많이 활용
                
                ```jsx
                (function init() {
                  // 프로그램이 실행 될 때 기본적으로 동작할 코드들..
                })();
                ```
                
                - 또는 재사용이 필요없는, 일회성 동작을 구성할 때 활용
                
                ```jsx
                const firstName = 'Young';
                const lastName = 'Kang';
                
                const greetingMessage = (function () {
                  const fullName = `${firstName} ${lastName} `;
                
                  return `Hi! My name is ${fullName}`;
                })();
                ```
                
            
            <aside>
            💡 자바스크립트에서 함수는 변수나 다른 데이터 구조 안에 할당될 수 있고 다른 함수의 파라미터로 전달될 수도 있고 다른 함수의 리턴 값이 될 수도 있다. ( “값으로서의 함수”)  → 일급 함수
            
            </aside>
            
            1. Parameter와 argument 
                1. parameter(매개변수) : 함수 선언 부분에서 소괄호 안에 작성되는 것 
                2. argument(인수/인자) : 함수 호출 부분에서 파라미터로 전달하는 값에 해당하는 것
---

</br>

### 질문
