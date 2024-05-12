# ch04.React.js 개론

## 04. React.js 소개

Reat.js = Meta(facebook)이 개발한 오픈소스 js 라이브러리

대규모 웹 서비스의 UI를 더 편하게 개발하기 위해 만들어진 기술

+아주 인기 있음

### 특징

1. **컴포넌트를 기반으로 UI를 표현함**
    - 컴포넌트 = 화면 구성 요소, UI 구성 요소
    - 여러 페이지에서 공통되는 요소가 필요할 때,
        
        컴포넌트를 만든 후 여러 페이지에서 불러와서 사용되게 함. → 유지 보수 b
        
    
2. **화면 업데이트 구현이 쉽다**
    - 업데이트 = 사용자의 행동에 따라 웹 페이지가 스스로 모습을 바꿔 사용자와 상호작용
    - **선언형 프로그래밍** = 과정은 생략, 목적만 간결히 명시!(코드 간결)
        
        ( ↔ 명령형 프로그래밍 = 목적을 이루기 위한 모든 일련의 과정을 설명하는 방식)
        
        → 바뀐 state값에 따라 각각 다른 UI를 화면에 랜더링하도록 함
        
        랜더링 = UI 요소를 화면에 그려내는 것
        
        ![Untitled](ch04%20React%20js%20%E1%84%80%E1%85%A2%E1%84%85%E1%85%A9%E1%86%AB%20b2f496775b664aaa888b167b90d9b3a2/Untitled.png)
        
        → 업데이트를 위한 복잡한 동작을 직접 정의할 필요 없이 
        
        특정 변수의 값을 바꾸는 것 만으로도 화면을 업데이트 시킬 수 있음
        
3. **화면 업데이트가 빠르게 처리됨**
    
    Q, 선수 지식
    
    1. 브라우저는 어떻게 동작?
    2. HTML, CSS로 만든 페이지 어떻게 랜더링?
    3. 화면 업데이트 어떻게 처리?
    - 브라우저의 렌더링 과정(Critical Rendering Path)
        
        ![Untitled](ch04%20React%20js%20%E1%84%80%E1%85%A2%E1%84%85%E1%85%A9%E1%86%AB%20b2f496775b664aaa888b167b90d9b3a2/Untitled%201.png)
        
        ![Untitled](ch04%20React%20js%20%E1%84%80%E1%85%A2%E1%84%85%E1%85%A9%E1%86%AB%20b2f496775b664aaa888b167b90d9b3a2/Untitled%202.png)
        
        ex)
        
        ![Untitled](ch04%20React%20js%20%E1%84%80%E1%85%A2%E1%84%85%E1%85%A9%E1%86%AB%20b2f496775b664aaa888b167b90d9b3a2/Untitled%203.png)
        
        ![Untitled](ch04%20React%20js%20%E1%84%80%E1%85%A2%E1%84%85%E1%85%A9%E1%86%AB%20b2f496775b664aaa888b167b90d9b3a2/Untitled%204.png)
        
        ![Untitled](ch04%20React%20js%20%E1%84%80%E1%85%A2%E1%84%85%E1%85%A9%E1%86%AB%20b2f496775b664aaa888b167b90d9b3a2/Untitled%205.png)
        
    - Virtual DOM
        
        = DOM을 js 객체로 흉내낸 것, 일종의 복제판
        
        → React는 업데이트가 발생하면 실제 DOM 수정하기 전에 이 가상의 복제판 DOM에 
        
            먼저 반영해본다. (연습 스윙)
        
        → 동시에 업데이트가 발생한 경우, 순서대로 반영해 Virsual DOM에서 다 모이게 해서
        
            업데이트들을 한번에 반영(DOM 1회 반영)
        

## 02. React app 생성하기

1. Node.js 패키지 생성
2. React 라이브러리 설치
3. 기타 도구 설치 및 설정(어려움)

[구조]

public : 정적인 파일 저장(사진, 동영상)

src : react, js 코드 저장, 정적 파일 보관도 가능!

html : React 코드의 기본 틀

vite.config.js 

## 03. React App 구동원리

1. React App 생성(With Vite)
    
    npm create vite@latest
    
2. React App 가동
    
    package.json - devDependencies 안에 있는 dev,…, … → npm run dev(React App 가동시켜라) 
    
3. React 앱 접속
    
    console 안에 있는 링크(현재 가동중인 리액트 웹 서버에 접속할 수 있는 주소)
    
    [http://localhost:5173](http://localhost:5173) (5173→리액트 서버로 접속 가능), (3344→PHP 서버)
    
    http://내 컴퓨터:포트번호 
    
    → localhost는 내 컴퓨터이기 때문에 다른 컴퓨터에서 똑같이 [localhost:5173](http://localhost:5173) 치는 건 X

    
    
# ch05.React.js 입문

## 1. React 컴포넌트

컴포넌트 = js 코드가 html 태그를 반환하게하는 것

→ 함수 이용해서 컴포넌트 만드는 게 일반적!

→ 주의: component 생성시 첫 글자는 꼭 대문자!

ex)

![Untitled](ch05%20React%20js%20%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%86%E1%85%AE%E1%86%AB%20c03b86c334c0461bb4a9b944d623940a/Untitled.png)

![Untitled](ch05%20React%20js%20%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%86%E1%85%AE%E1%86%AB%20c03b86c334c0461bb4a9b944d623940a/Untitled%201.png)

- React 컴포넌트는 위의 모습처럼 하나의 파일에 다 모아서 작성X
    
    → 모듈화를 위해 컴포넌트별로 각각 나눠서 작성하는 게 일반적
    

React 예시]

![Untitled](ch05%20React%20js%20%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%86%E1%85%AE%E1%86%AB%20c03b86c334c0461bb4a9b944d623940a/Untitled%202.png)

![Untitled](ch05%20React%20js%20%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%86%E1%85%AE%E1%86%AB%20c03b86c334c0461bb4a9b944d623940a/Untitled%203.png)

## 2. JSX-UI 표현

JSX = 확장된 자바스크립트의 문법

→ js랑 html 같이 쓸 수 있음

```jsx
// JSX 주의사항
// 1. 중괄호 내부에는 js 표현식만 넣을 수 있다. (한줄로서 값으로 나오는 값)
// e.g., 10, number, (for문, if문 = X)
// 2. 숫자, 문자열, 배열 값만 랜더링 됨 (boolean X)
// 3. 모든 태그는 닫혀있어야 한다. <main/> or <main></main>
// 4. 최상위 태그는 반드시 하나여야만 한다  여기선 <main>
const Main = () => {
const number = 10;
const obj = { a: 1 };

    return (
        <main>
        <h1>main</h1>
        <h2>{number % 2 === 0 ? "짝수" : "홀수"}</h2>
        {obj.a}
        </main>
    );
};

export default Main;
```

- Main component가 조건에 따라 각각 다른 UI 나타나게 하기

```jsx
const Main = () => {
    const user = {
        name : "이정환",
        isLogin: true,
    }

    return <>
    {user.isLogin ? <div>로그아웃</div> : <div>로그인</div>}
    </>;
};

export default Main;
```

- DOM 요소 스타일 적용하는 법
    - 변수 쓸 때, - 쓰면 안 됨
    1. 첫번째 방법
        
        → return문 안에 스타일 코드 많아지면 가독성 떨어짐 → 두번째
        
    
    ```jsx
    const Main = () => {
        const user = {
            name : "이정환",
            isLogin: true,
        };
    
        if (user.isLogin){
            return (
            <div 
            style={{
                backgroundColor : "red",
                borderBottom: "5px solid blue", // 카멜표기법
            }}
            >로그아웃</div>
        );
        } else {
            return <div>로그인</div>;
        }
    
        // return <>
        // {user.isLogin ? <div>로그아웃</div> : <div>로그인</div>}
        // </>;
    };
    ```
    
    1. 두 번째 방법
    
    ```jsx
    //Main.jsx
    
    const Main = () => {
        const user = {
            name : "이정환",
            isLogin: true,
        };
    
        if (user.isLogin){
            return (
            <div className = "logOut"> // thml에선 class지만 여기선 합치는 거니까 className
            로그아웃</div>
        );
        } else {
            return <div>로그인</div>;
        }
    
        // return <>
        // {user.isLogin ? <div>로그아웃</div> : <div>로그인</div>}
        // </>;
    };
    
    export default Main;
    ```
    
    ```css
    //Main.css
    
    .logout{
        background-color: red;
        border-bottom: 5px solid green;
    
    }
    ```
    

## 4. Props로 데이터 전달

![Untitled](ch05%20React%20js%20%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%86%E1%85%AE%E1%86%AB%20c03b86c334c0461bb4a9b944d623940a/Untitled%204.png)

[https://www.notion.so](https://www.notion.so)

```jsx
//App.jsx

import './App.css'
import Button from "./components/Button";

const buttonProps = { //App에 return하고 싶은 값이 많으면 사용(스프레드함수)
  text: "메일",
  color: "red",
  a:1,
  b:2,
  c:3,
};

function App() {
  return (
    <>
    <Button {...buttonProps}/>
    <Button text={"카페"}/>
    <Button text={"블로그"}/>
    </>
  )
}

export default App;
```

```jsx
//Button.jsx

const Button = ({text, color}) => {
    
    return <button style={{color : color}}>{text}-{color.toUpperCase()}</button>;
};  // color를 인수로 받지 않는 상태에서 이렇게 써버리면 undefined의 점 표기니까 문제될 수 있음

Button.defaultProps = { // 위 문제의 Sol)
    color:"black",
}

export default Button;
```

- 자식 → 부모는 X
    
    부모 → 자식은 O
    
    ```jsx
    import './App.css'
    import Button from "./components/Button";
    
    const buttonProps = { //App에 return하고 싶은 값이 많으면 사용(스프레드함수)
      text: "메일",
      color: "red",
      a:1,
      b:2,
      c:3,
    };
    
    function App() {
      return (
        <>
        <Button {...buttonProps}/>
        <Button text={"카페"}/>
        <Button text={"블로그"}>
        <div>자식요소</div>
        </Button>
        </>
      );
    }
    
    export default App;
    ```
    
    ```jsx
    const Button = ({text, color, children}) => {
        
        return (<button style={{color : color}}>
            {text}-{color.toUpperCase()}
            {children}
            </button>
        );
    };  // color를 인수로 받지 않는 상태에서 이렇게 써버리면 
    		// undefined의 점 표기니까 문제될 수 있음
    
    Button.defaultProps = { // 위 문제의 Sol)
        color:"black",
    }
    
    export default Button;
    ```
    

## 5. Event Handling

event = 웹 내부에서 발생하는 사용자의 모든 행동 ( e,g,. 버튼 크릭, 메세지 입력, 스크롤 등등)

handling = 다루다, 취급하다

event handling = 이벤트가 발생했을 때 그것을 처리하는 것 (e,g,. 버튼 클릭시 경고창 노출)

```jsx
const Button = ({text, color, children}) => {
    
    return (
    <button 
    onClick = {()=> {   // 이벤트 핸들러
        console.log(text)
    }}
    style={{color : color}}>
        {text}-{color.toUpperCase()}
        {children}
        </button>
    );
};  
```

- 합성 이벤트 객체
    
    = 모든 웹 브라우저의 이벤트 객체를 하나로 통일한 형태
    
    → 너무 많은 브라우저들은 서로 동작이 조금씩 다름
    
    Cross Browsing Issue = 브라우저 별 스펙이 달라 발생하는 문제
    
    → Synthetic Event(합성 이벤트) = 모든 브라우저에서의 이벤트 객체를 하나로 통일한 형태
    
    ```jsx
    const Button = ({text, color, children}) => {
        //이벤트 객체
        const onClickButton = (e) => { //합성이벤트 SyntheticBaseEvent -> 이벤트 발생한 모든 정보 있음
            console.log(e);
            console.log(text);
        };
    
        return (
        <button 
            onClick={onClickButton} 
            onMouseEnter = {onClickButton}
            style={{color : color}}
        >
            {text}-{color.toUpperCase()}
            {children}
            </button>
        );
    };  
    
    Button.defaultProps = { 
        color:"black",
    }
    
    export default Button;
    ```
    

## 6. State - 상태 관리하기

State = 현재 가지고 있는 상태나 모양을 정의

       변화할 수 있는 동적인 값

→ React component는 state를 가지고 있음 ((지금까진 state 없는 컴포넌트였다!))

→ State값에 따라 랜더링되는 UI가 결정된다.

- Re-Render(리 렌더), Re-Rendering(리 렌더링) = 컴포넌트가 다시 렌더링되는 상황
- 하나의 컴포넌트에 여러 개의 state 넣을 수 있다.
- 가변적인 값을 화면에 랜더링해주고 싶으면 일반 변수가 아닌 state로 처리해야 함!

```jsx
import "./App.css";
import { useState } from "react";

function App() {
	//state 값이 변했을 때만 rerendering..
  const [count, setCount] = useState(0); //초기값 넣어서 시작! 
  // count=초기값(현재값), setCount= 변하게 하는 함수
  const [light, setLight] = useState("OFF");
  
  // 버튼 누를 때마다 1씩 증가함
  return (
    <> 
    <div>
      <h1>{light}</h1>
      <button
       onClick = {()=> {
        setLight(light === "ON" ? "OFF" : "ON");
      }}
      >
        {light === "ON" ? "끄기" : "켜기"}
      </button>
    </div>
    <div>
      <h1>{count}</h1>
        <button
          onClick = {() => {
            setCount(count+1);
          }}
        >
          +
        </button>
    </div>
      
    </>
  );
}

export default App;

```

## 7. State룰 Props로 전달하

React에서 Re rendering 될 때

1. state가 변경되었을 때
2. props가 변경되었을 때
3. 부모 component 렌더링 → 자식도 마찬가지!

- 불필요한 렌더링을 줄일 수 있음

```jsx
import "./App.css";
import { useState } from "react";

const Bulb = ()=>{
  const [light, setLight] = useState("OFF");

  console.log(light);
  return (
    <div>
      {light==='ON'? (
        <h1 style = {{backgroundColor:"orange"}}>ON</h1> 
      )  : (
        <h1 style = {{backgroundColor: "gray"}}>OFF</h1>
        )}

<button
       onClick = {()=> {
        setLight(light === "ON" ? "OFF" : "ON");
      }}
      >
        {light === "ON" ? "끄기" : "켜기"}
      </button>
    </div>
        
  );
};

const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
    <h1>{count}</h1>
      <button
        onClick = {() => {
          setCount(count+1);
        }}
      >
        +
      </button>
  </div>
  );
}

function App() {
 
  // count=초기값(현재값), setCount= 변하게 하는 함수
  
  // 버튼 누를 때마다 1씩 증가함
  return (
    <> 
    <Bulb />
    <Counter />
    </>
  );
}

export default App;

```

```jsx
//App.jsx

import "./App.css";

import Bulb from './components/Bulb';
import Counter from './components/Counter';

function App() {
  // count=초기값(현재값), setCount= 변하게 하는 함수
  
  // 버튼 누를 때마다 1씩 증가함
  return (
    <> 
      <Bulb />
      <Counter />
    </>
  );
}

export default App;
```

```jsx
// Bulb.jsx

import {useState} from "react";

const Bulb = ()=>{
    const [light, setLight] = useState("OFF");
  
    console.log(light);
    return (
      <div>
        {light==='ON'? (
          <h1 style = {{backgroundColor:"orange"}}>ON</h1> 
        )  : (
          <h1 style = {{backgroundColor: "gray"}}>OFF</h1>
          )}
  
        <button
            onClick = {()=> {
                setLight(light === "ON" ? "OFF" : "ON");
            }}
        >
            {light === "ON" ? "끄기" : "켜기"}
        </button>
    </div>            
    );
  };

  export default Bulb;
```

```jsx
//Counter.jsx

import {useState} from "react";

const Counter = () => {
    const [count, setCount] = useState(0);
  
    return (
      <div>
      <h1>{count}</h1>
        <button
          onClick = {() => {
            setCount(count+1);
          }}
        >
          +
        </button>
    </div>
    );
  };

  export default Counter;
```

## 8. State로 사용자 입력 관리하기1

1. 함수의 return 안에 있는 <div>태그에 원하는 속성에 관한 변수 추가
    
    ( 아니면 원하는 태그 사용)
    
2. state 추가 (const [name, setName] = useState("이름");)
3. 이벤트 함수 만들기 (onChangeName = (e) ⇒ { )
4. 1번 과정에서의 태그 안에 설정(<textarea value ={bio} onChange={onChangeBio} />)

e.g.,

1. 이름 입력 받기
    
    → input태그 사용(한줄만 입력받기)
    
    ```jsx
    import {useState} from 'react';
    // 간단한 회원가입 폼
    // 1. 이름, 2. 생년월일 3. 국적 4. 자기소개
    
    const Register = ()=> {
    
        const [name, setName] = useState("이름"); //초기값 설정("이름"을 빈 괄호에 일부러 넣음)
    
        const onChangeName = (e) => {
            setName(e.target.value); // -> input으로 인해 알게된 경로(?)
        } // 이벤트 객체
          
        return (
         <div>
           <input 
           value = {name}
           onChange = {onChangeName} 
           placeholder = {"이름"} 
           />
           {name}
         </div>
        );
    };
    
    export default Register;
    ```
    
2. 생년월일 입력 받기
    
    ```jsx
    import {useState} from 'react';
    // 간단한 회원가입 폼
    // 1. 이름, 2. 생년월일 3. 국적 4. 자기소개
    
    const Register = ()=> {
    
        const [name, setName] = useState("이름"); //state로 보관하기
        const [birth, setBirth] = useState("");
    
        const onChangeName = (e) => {
            setName(e.target.value);
        }
    
        const onChangeBirth = (e) => {
            setBirth(e.target.value);
        }
          
        return (
         <div>
            <div>
                <input 
                   value = {name}
                   onChange = {onChangeName} 
                   placeholder = {"이름"} 
           />
           </div>
    
            <div>
            <input 
            value = {birth}
            onChange={onChangeBirth}
            type = "date" 
            />
            {birth}
            </div>
         </div>
        );
    };
    
    export default Register;
    ```
    
3. 국적 입력 받기
    
    → 국적처럼 사용자가 한정된 선택지 중 선택을 해야하는 상황이면 <select> 이용
    
    → <select> 안에 <option>
    
    → <option value="korea">한국</option>처럼 선택지:한국, 출력값:korea(간결)
    
    ```jsx
    import {useState} from 'react';
    // 간단한 회원가입 폼
    // 1. 이름, 2. 생년월일 3. 국적 4. 자기소개
    
    const Register = ()=> {
    
        const [name, setName] = useState("이름"); //state로 보관하기
        const [birth, setBirth] = useState("");
        const [country, setCountry] = useState("");
    
        const onChangeName = (e) => {
            setName(e.target.value);
        }
    
        const onChangeBirth = (e) => {
            setBirth(e.target.value);
        }
          
        const onChangeCountry = (e) => {
            setCountry(e.target.value);
        }
    
        return (
         <div>
            <div>
                <input 
                   value = {name}
                   onChange = {onChangeName} 
                   placeholder = {"이름"} 
           />
           </div>
    
            <div>
            <input 
            value = {birth}
            onChange={onChangeBirth}
            type = "date" 
            />
            {birth}
            </div>
    
            <div>
                <select value={country} onChange = {onChangeCountry}>
                    <option></option> 
                    <option value="korea">한국</option> 
                    <option value="us">미국</option>
                    <option value="uk">영국</option>
                </select>
                {country}
            </div>
         </div>
        );
    };
    
    export default Register;
    ```
    

1. 자기소개
    
    → <input /> = 사용자가 한 줄 입력
    
    → <textarea /> = 사용자가 여러 줄 입력 가능
    
    ```jsx
    import {useState} from 'react';
    // 간단한 회원가입 폼
    // 1. 이름, 2. 생년월일 3. 국적 4. 자기소개
    
    const Register = ()=> {
    
        const [name, setName] = useState("이름"); //state로 보관하기
        const [birth, setBirth] = useState("");
        const [country, setCountry] = useState("");
        const [bio, setBio] = useState("");
    
        const onChangeName = (e) => {
            setName(e.target.value);
        }
    
        const onChangeBirth = (e) => {
            setBirth(e.target.value);
        }
          
        const onChangeCountry = (e) => {
            setCountry(e.target.value);
        }
    
        const onChangeBio = (e) => {
            setBio(e.target.value);
        }
    
        return (
         <div>
            <div>
                <input 
                   value = {name}
                   onChange = {onChangeName} 
                   placeholder = {"이름"} 
           />
           </div>
    
            <div>
            <input 
            value = {birth}
            onChange={onChangeBirth}
            type = "date" 
            />
            {birth}
            </div>
    
            <div>
                <select value={country} onChange = {onChangeCountry}>
                    <option></option> 
                    <option value="korea">한국</option> 
                    <option value="us">미국</option>
                    <option value="uk">영국</option>
                </select>
                {country}
            </div>
    
            <div>
                <textarea value ={bio} onChange={onChangeBio} />
                {bio}
            </div>
         </div>
        );
    };
    
    export default Register;
    ```
    

## 9. State로 사용자 입력 관리하기2

→ 목적 : 8(위)에서의 중복되는 비효율적인 코드를 수정하기 위함

→ 스프레드 함수(…input) 쓰는 이유=기존에 입력했던 값들도 반영해주려고

```jsx
import {useState} from 'react';
// 간단한 회원가입 폼
// 1. 이름, 2. 생년월일 3. 국적 4. 자기소개

const Register = ()=> {

    const [input, setInput] = useState({
        name : "",
        birth: "",
        country : "",
        bio: "",
    });

    const onChange = (e) => { // 통합이벤트핸들러
        setInput({
            ...input,
            [e.target.name]: e.target.value, //property의 key 설정(e.target.name = birth,...,)
        });
    };

    return (
     <div>
        <div>
        <input
            name="name"
            value = {input.name}
            onChange = {onChange} 
            placeholder = {"이름"} 
       />
       </div>

        <div>
        <input 
            name="birth"
            value = {input.birth}
            onChange={onChange}
            type = "date" 
        />
        </div>

        <div>
            <select 
            name = "country"
            value={input.country} 
            onChange = {onChange}
            >
                <option value=""></option> 
                <option value="korea">한국</option> 
                <option value="us">미국</option>
                <option value="uk">영국</option>
            </select>
        </div>

        <div>
            <textarea 
            name="bio"
            value ={input.bio} 
            onChange={onChange} 
            />
        </div>
     </div>
    );
};

export default Register;
```

## 10. useRef로 컴포넌트의 변수 생성하기

= 새로운 reference 객체를 생성하는 기능

e.g., const refObject = useRef()

           컴포넌트 내부의 변수

- useRef
    
    = Reference 객체 생성
    
    - 컴포넌트 내부 변수로 활용가능
    - 어떤 경우에도 리렌더링 유발 X (새로고침X ?)
    - 원하는 요소 바로바로 조작 가능!
- useState
    
    = State 생성
    
    - 컴포넌트 내부 변수로 활용 가능
    - 값 변경되면 컴포넌트 리렌더링

![Untitled](ch05%20React%20js%20%E1%84%8B%E1%85%B5%E1%86%B8%E1%84%86%E1%85%AE%E1%86%AB%20c03b86c334c0461bb4a9b944d623940a/Untitled%205.png)

→ countRef = 리렌더링 안 해도 됨!

```jsx
import {useRef, useState} from 'react';

// 간단한 회원가입 폼
// 1. 이름, 2. 생년월일 3. 국적 4. 자기소개

const Register = ()=> {

    const [input, setInput] = useState({
        name : "",
        birth: "",
        country : "",
        bio: "",
    });

    const countRef = useRef(0);
    const inputRef = useRef();

    const onChange = (e) => { // 통합이벤트핸들러
        countRef.current++;
        console.log(countRef.current);
        setInput({
            ...input,
            [e.target.name]: e.target.value, //property의 key 설정(e.target.name = birth,...,)
        });
    };

    const onSubmit = () => {
        if(input.name === ""){
            //이름을 입력하는 DOM 요소 포커스
            inputRef.current.focus();
        }
    }

    return (
     <div>
        
        <div>
        <input
            ref={inputRef}
            name="name"
            value = {input.name}
            onChange = {onChange} 
            placeholder = {"이름"} 
       />
       </div>

        <div>
        <input 
            name="birth"
            value = {input.birth}
            onChange={onChange}
            type = "date" 
        />
        </div>

        <div>
            <select 
            name = "country"
            value={input.country} 
            onChange = {onChange}
            >
                <option value=""></option> 
                <option value="korea">한국</option> 
                <option value="us">미국</option>
                <option value="uk">영국</option>
            </select>
        </div>

        <div>
            <textarea 
            name="bio"
            value ={input.bio} 
            onChange={onChange} 
            />
        </div>

        <button onClick={onSubmit}>제출</button>
     </div>
    );
};

export default Register;
```

useref = 

## 11. React Hooks

React Hooks = 클래스 컴포넌트(복잡) 기능을 함수 컴포넌트(간단)에서도 이용할 수 있도록 도움

→ 함수 컴포넌트 내부에서만 호출 가능

→ 조건문, 반복문 내부에서는 호출 불가

→ use를 이용해서 나만의 Hook 만들기 가

- useState = State 기능을 낚아채오는 Hook
- useRef = Reference 기능을 낚아채오는 Hook

```jsx
import {useState} from "react";
//3가지 hook 관련 팁
// 1. 함수 컴포넌트, 커스텀 훅 내부에서만 호출 가능
// 2. 조건부로 호출 X
// 3. 나만의 훅(Custom Hook) 직접 만들 수 있다.

function useInput(){
    const [input, setInput] = useState("");

    const onChange = (e) => {
        setInput(e.target.value);
    }

    return [input, onChange];
}

const HookExam = () => {    

    const [input, onChange] = useInput();

    return (
    <div>
        <input value={input} onChange={onChange} />
        </div>
    );
};

export default HookExam;
```

##