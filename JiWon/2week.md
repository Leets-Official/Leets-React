# 섹션 3. Node.js 기초

3.1) Node.js를 소개합니다

Node.js는 JavaScript의 실행 환경 (Run Time) = 구동기

3.2) Node.js 설치하기

npm = node package manager

3.3) Node.js 사용하기

프로젝트 = 특정 목적을 갖는 프로그램의 단위

패키지 = Node.js에서 사용하는 프로그램의 단위

```jsx
{
  "name": "section03",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start" : "node src/index.js"
  },
  "author": "",
  "license": "ISC"
}
```

```jsx
console.log("안녕 Node.js");
```

3.4) Node.js 모듈 시스템 이해하기

모듈 시스템 = 모듈을 다루는 시스템

기능 별로 파일을 나눠서 다룸

모듈을 생성하고, 불러오고, 사용하는 등의 모듈을 다루는 다양한 기능을 제공하는 시스템 (CJS, ESM)

```jsx
//math 모듈
function add (a,b) {
    return a+b;
}

function sub(a,b){
    return a-b;
}

module.exports = {
    add : add,
    sub: sub,
}
```

```jsx
const moudleData = require("./math");

console.log(moudleData.add(1,2));
console.log(moudleData.sub(1,2));
```

```jsx
{
  "name": "section03",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start" : "node src/index.js"
  },
  "author": "",
  "license": "ISC",
  "type": "module"
}
```

```jsx
//math 모듈
export function add(a,b) {
    return a + b;
}

export function sub(a,b){
    return a - b;
}

export default function multiply(a,b){
    return a * b;
}
```

```jsx
import mul from "./math.js";
import {add, sub} from "./math.js";

console.log(add(1,2));
console.log(sub(1,2));
console.log(mul(2,3));
```

3.5)Node.js 라이브러리 사용하기

라이브러리 = 프로그램을 개발할 때 필요한 다양한 기능들을 미리 만들어 모듈화 해 놓은 것

```jsx
import mul from "./math.js";

import randomColor from "randomcolor";

const color = randomColor();
console.log(color);
```

```jsx
{
  "name": "section03",
  "version": "1.0.0",
  "lockfileVersion": 3,
  "requires": true,
  "packages": {
    "": {
      "name": "section03",
      "version": "1.0.0",
      "license": "ISC",
      "dependencies": {
        "randomcolor": "^0.6.2"
      }
    },
    "node_modules/randomcolor": {
      "version": "0.6.2",
      "resolved": "https://registry.npmjs.org/randomcolor/-/randomcolor-0.6.2.tgz",
      "integrity": "sha512-Mn6TbyYpFgwFuQ8KJKqf3bqqY9O1y37/0jgSK/61PUxV4QfIMv0+K2ioq8DfOjkBslcjwSzRfIDEXfzA9aCx7A=="
    }
  }
}
```

```jsx
{
  "name": "section03",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node src/index.js"
  },
  "author": "",
  "license": "ISC",
  "type": "module",
  "dependencies": {
    "randomcolor": "^0.6.2"
  }
}
```

# 섹션 4. React.js 개론

4.1) React.js를 소개합니다

React.js =  Meta(facebook)이 개발한 오픈소스 JavaScript 라이브러리

대규모 웹 서비스의 UI를 더 편하게 개발하기 위해 만들어진 기술 (넷플릭스, 페이스북, 인스타)

1. 컴포넌트 (구성 요소)를 기반으로 UI를 표현한다
2. 화면 업데이트(사용자의 행동(클릭, 드래그)에 따라 웹페이지가 스스로 모습을 바꿔 상호작용 하는 것) 구현이 쉽다.

선언형 프로그래밍: 과정은 생략하고 목적만 간결히 명시하는 방법

- 목적만 깔끔하게 명시, 코드가 간결함

명령형 프로그래밍: 목적을 이루기 위한 모든 일련의 과정을 설명하는 방식

- 모든 과정을 하나 하나 다 설명, 코드가 길고 복잡함

선언형 프로그래밍 = 업데이트를 위한 복잡한 동작을 직접 정의할 필요 없이 특정 변수의 값을 바꾸는 것 만으로도 화면을 업데이트 시킬 수 있다.

1. 화면 업데이트가 빠르게 처리된다

4.2) 첫 React App 생성하기

Vite 사용

```jsx
{
  "name": "section04",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "lint": "eslint . --ext js,jsx --report-unused-disable-directives --max-warnings 0",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0"
  },
  "devDependencies": {
    "@types/react": "^18.2.66",
    "@types/react-dom": "^18.2.22",
    "@vitejs/plugin-react": "^4.2.1",
    "eslint": "^8.57.0",
    "eslint-plugin-react": "^7.34.1",
    "eslint-plugin-react-hooks": "^4.6.0",
    "eslint-plugin-react-refresh": "^0.4.6",
    "vite": "^5.2.0"
  }
}
```

4.3) React App 구동원리 살펴보기

[localhost](http://localhost) (포트 번호)= 우리 컴퓨터의 주소를 의미함

```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './index.css'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
)
```

```jsx
import { useState } from 'react'
import reactLogo from './assets/react.svg'
import viteLogo from '/vite.svg'
import './App.css'

function App() {
  const [count, setCount] = useState(0)

  return (
    <>
      <div>
        <a href="https://vitejs.dev" target="_blank">
          <img src={viteLogo} className="logo" alt="Vite logo" />
        </a>
        <a href="https://react.dev" target="_blank">
          <img src={reactLogo} className="logo react" alt="React logo" />
        </a>
      </div>
      <h1>Vite + React</h1>
      <div className="card">
        <button onClick={() => setCount((count) => count + 1)}>
          count is {count}
        </button>
        <p>
          Edit <code>src/App.jsx</code> and save to test HMR
        </p>
      </div>
      <p className="read-the-docs">
        Click on the Vite and React logos to learn more
      </p>
    </>
  )
}

export default App
```

```jsx
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Vite + React</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>

```

# 섹션 5. React.js 입문

5.1) 실습 준비하기

```jsx
module.exports = {
  root: true,
  env: { browser: true, es2020: true },
  extends: [
    'eslint:recommended',
    'plugin:react/recommended',
    'plugin:react/jsx-runtime',
    'plugin:react-hooks/recommended',
  ],
  ignorePatterns: ['dist', '.eslintrc.cjs'],
  parserOptions: { ecmaVersion: 'latest', sourceType: 'module' },
  settings: { react: { version: '18.2' } },
  plugins: ['react-refresh'],
  rules: {
    'react/jsx-no-target-blank': 'off',
    'react-refresh/only-export-components': [
      'warn',
      { allowConstantExport: true },
    ],
    "no-unused-vars": "off",
    "react/prop-types": "off",
  },
}
```

```jsx
import './App.css';

function App() {

  return (
    <>
      <h1>안녕 리액트!</h1>
    </>
  );
}

export default App;
```

5.2) React 컴포넌트

```jsx
import "./App.css";
import Header from "./components/Header";
import Main from "./components/Main";
import Footer from "./components/Footer";

function App() {
  return (
    <>
      <Header />
      <Main />
      <Footer />
    </>
  );
}

export default App;
```

```jsx
const Main = () => {
    return (
        <footer>
            <h1>main</h1>
        </footer>
    )
}

export default Main;
```

```jsx
const Footer = () => {
    return (
        <footer>
            <h1>footer</h1>
        </footer>
    )
}

export default Footer;
```

```jsx
const Header = () => {
    return (
      <header>
        <h1>header</h1>
      </header>
    )
  }
  
  export default Header;
```

5.3) JSX로 UI 표현하기

JSX = 확장된 자바스크립트 문법 (JavaScript Extensions)

JSX 주의 사항

1. 중괄호 내부에는 자바스크립트 표현식만 넣을 수 있다.
2. 숫자, 문자열, 배열 값만 랜더링 된다.
3. 모든 태그는 닫혀있어야 한다.
4. 최상위 태그는 반드시 하나여야만 한다.

```jsx
const Main = () => {
    const number = 9;
    const obj = { a: 1};

    return (
        <main>
            <h1>main</h1>
            <h2>{number % 2 === 0 ?"짝수" : "홀수"}</h2>
            {10}
            {number}
            {[1, 2, 3]}
            {true}
            {undefined}
            {null}
            {obj.a}
        </main>
    )
}

export default Main;
```

```jsx
import "./Main.css";

const Main = () => {
    const user = {
        name: "김지원",
        isLogin: true,
    }

    if (user.isLogin){
        return <div className="logout">로그아웃</div>;
    } else {
        return <div>로그인</div>;
    }

    // return (
    //     <>
    //         {user.isLogin ? (
    //             <div>로그아웃</div>
    //         ) : (
    //             <div>로그인</div>
    //         )}
    //     </>
    // )
}

export default Main;
```

```jsx
.logout{
    background-color: red;
    border-bottom: 5px solid green;
}
```

5.4) Props로 데이터 전달하기

```jsx
import "./App.css";
import Header from "./components/Header";
import Main from "./components/Main";
import Footer from "./components/Footer";
import Button from "./components/Button";

function App() {
  const buttonProps = {
    text: "메일",
    color: "red",
    a:1,
    b:2,
    c:3,
  }
  return (
    <>
      <Button {...buttonProps} />
      <Button text={"카페"} />
      <Button text={"블로그"}>
        <Header />
      </Button>
    </>
  );
}

export default App;
```

```jsx
const Button = ({text, color,children}) => {
    return (
        <button style={{ color: color }}>
            {text} - {color.toUpperCase()}
            {children}
        </button>
    );
}

Button.defaultProps = {
    color: "black",
}
export default Button;
```

5.5) 이벤트 처리하기

Event = 웹 내부에서 발생하는 사용자의 행동 (버튼 클릭, 메시지 입력, 스크롤 등)

Handling = 다루다, 취급하다, 처리하다

Event Handling = 이벤트가 발생했을 때 그것을 처리하는 것 (버튼 클릭시 경고창 노출)

```jsx
const Button = ({text, color,children}) => {
    //이벤트 객체
    const onClickButton = (e) => {
        console.log(e);
        console.log(text);
    }
    return (
        <button 
            onClick={onClickButton}
            // onMouseEnter={onClickButton}
            style={{ color: color }}
        >
            {text} - {color.toUpperCase()}
            {children}
        </button>
    );
}

Button.defaultProps = {
    color: "black",
}
export default Button;
```

합성 이벤트 = 모든 웹 브라우저의 이벤트 객체를 하나로 통일한 형태

5.6) State로 상태관리하기

State = 현재 가지고 있는 형태나 모양을 정의, 변화할 수 있는 동적인 값

State의 값에 따라 랜더링 되는 UI가 달라진다.

```jsx
import "./App.css";
import { useState } from "react";

function App() {
  const [count, setCount] = useState(0);
  const [light, setLight] = useState("OFF");

  return (
    <>
    <div>
      <h1>{light}</h1>
      <button onClick={()=>{
        setLight(light === 'ON' ? "OFF" : "ON");
      }}
      >
        {light === "ON" ? "끄기" : "켜기"}
      </button>
    </div>
      <h1>{count}</h1>
      <button 
        onClick ={()=>{
          setCount(count +1);
        }}
      >
        +
        </button>
    </>
  );
}

export default App;
```

5.7) State와 Props

```jsx
import "./App.css";
import { useState } from "react";

import Bulb from "./components/Bulb";
import Counter from "./components/Counter";

function App() {
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
import { useState } from "react";
const Bulb= ()=>{

    const [light, setLight] = useState("OFF");
  
    console.log(light);
    return (
      <div>
        {light === 'ON' ? (<h1 style={{backgroundColor: "orange" }}>ON</h1> 
      ) : (
        <h1 style={{backgroundColor: "gray" }}>OFF</h1>
      )}
      <button onClick={()=>{
          setLight(light === 'ON' ? "OFF" : "ON");
        }}
        >
          {light === "ON" ? "끄기" : "켜기"}
        </button>
    </div>
    )
  }

  export default Bulb;
```

```jsx
import { useState } from "react";

const Counter = ()=>{
    const [count, setCount] = useState(0);
  
    return(
      <div>
        <h1>{count}</h1>
        <button 
          onClick ={()=>{
            setCount(count +1);
          }}
        >
          +
          </button>
      </div>
    )
  }

  export default Counter;
```

5.8) State로 사용자 입력 관리하기 1

```jsx
import { useState } from "react";

//간단한 회원가입 폼
//1. 이름
//2. 생년월일
//3. 국적
//4. 자기소개

const Register = () => {
    const [name, setName ] = useState("이름");
    const [birth, setBirth] = useState("");
    const [country, setCountry] = useState("");
    const [bio, setBio] = useState("");

    const onChangeName = (e)=>{
        setName(e.target.value);
    }

    const onChangeBirth = (e) => {
        setBirth(e.target.value);
    }

    const onChangeCountry = (e)=>{
        setCountry(e.target.value);
    }

    const onChangeBio = (e)=>{
        setBio(e.target.value);
    }

    return (
        <div>
            <div>
                <input 
                    value={name}
                    onChange={onChangeName} 
                    placeholder= {"이름"} 
                />
            </div>

            <div>
                <input 
                    value={birth}
                    onChange={onChangeBirth}                
                    type="data" 
                />
            </div>

            <div>
                <select value={country} onChange={onChangeCountry}>
                    <option value=""></option>
                    <option value="kr">한국</option>
                    <option value="us">미국</option>
                    <option value="uk">영국</option>
                </select>
            </div>

            <div>
                <textarea value={bio} onChange={onChangeBio} />
            </div>
        </div>
    )  
}

export default Register;
```

5.9) State로 사용자 입력 관리하기 2

```jsx
import { useState } from "react";

//간단한 회원가입 폼
//1. 이름
//2. 생년월일
//3. 국적
//4. 자기소개

const Register = () => {
    const[input, setInput] = useState({
        name :"",
        birth:"",
        country: "",
        bio: "",
    });

    const onChange = (e) =>{
        console.log(e.target.name, e.target.value);
        setInput({
            ...input,
            [e.target.name]: e.target.value,
        })
    }

    return (
        <div>
            <div>
                <input 
                name="name"
                    value={input.name}
                    onChange={onChange} 
                    placeholder= {"이름"} 
                />
            </div>

            <div>
                <input 
                name="birth"
                    value={input.birth}
                    onChange={onChange}                
                    type="data" 
                />
            </div>

            <div>
                <select 
                name="counrty"
                value={input.country} onChange={onChange}>
                    <option value=""></option>
                    <option value="kr">한국</option>
                    <option value="us">미국</option>
                    <option value="uk">영국</option>
                </select>
            </div>

            <div>
                <textarea
                name = "bio" value={input.bio} onChange={onChange} />
            </div>
        </div>
    )  
}

export default Register;
```

5.10) useRef로 컴포넌트의 변수 생성하기

useRef = 새로운 Reference 객체를 생성하는 기능

```jsx
const refObject = useRef()
```

useRef 

- Reference 객체를 생성
- 컴포넌트 내부의 변수로 활용 가능
- 어떤 경우에도 리렌더링을 유발하지 않음

useState 

- State를 생성
- 컴포넌트 내부의 변수로 활용 가능
- 값이 변경되면 컴포넌트 리렌더링

```jsx
import { useState, useRef } from "react";

//간단한 회원가입 폼
//1. 이름
//2. 생년월일
//3. 국적
//4. 자기소개

let count = 0;

const Register = () => {
    const[input, setInput] = useState({
        name :"",
        birth:"",
        country: "",
        bio: "",
    });

    const countRef = useRef(0);
    const inputRef = useRef();

    const onChange = (e) =>{
        // countRef.current ++;
        count ++;
        console.log(count);
        setInput({
            ...input,
            [e.target.name]: e.target.value,
        })
    }

    const onsubmit = () =>{
        if (input.name === "") {
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
                    value={input.name}
                    onChange={onChange} 
                    placeholder= {"이름"} 
                />
            </div>

            <div>
                <input 
                name="birth"
                    value={input.birth}
                    onChange={onChange}                
                    type="data" 
                />
            </div>

            <div>
                <select 
                name="counrty"
                value={input.country} onChange={onChange}>
                    <option value=""></option>
                    <option value="kr">한국</option>
                    <option value="us">미국</option>
                    <option value="uk">영국</option>
                </select>
            </div>

            <div>
                <textarea
                name = "bio" value={input.bio} onChange={onChange} />
            </div>

            <button onClick={onsubmit}>제출</button>
        </div>
    )  
}

export default Register;
```

5.11) React Hooks

React Hooks = 클래스 컴포넌트의 기능을 함수 컴포넌트에서도 이용할 수 있도록

```jsx
import useInput from "./../hooks/useInput";

//3가지 hook 관련된 팁
//1. 함수 컴포넌트, 커스텀 훅 내부에서만 호출 가능
//2. 조건부로 호출될 수는 없다.
//3. 나만의 훅(Custom Hook) 직접 만들 수 있다.

const HookExam = () => {
    const [input, onChange] = useInput();
    const [input2, onChange2] = useInput();

    return (
        <div>
            <input value={input} onChange={onChange} />
            <input value={input2} onChange={onChange2} />
        </div>
    )
}

export default HookExam;
```

```jsx
import{useState} from 'react';

function useInput(){
    const [input, setInput] = useState("");

    const onChange=(e)=>{
        setInput(e.target.value);
    }

    return [input, onChange];
}

export default useInput;
```

# 섹션 6. 프로젝트1. 카운터 앱

6.1) 프로젝트 소개 및 준비

```jsx
module.exports = {
  root: true,
  env: { browser: true, es2020: true },
  extends: [
    'eslint:recommended',
    'plugin:react/recommended',
    'plugin:react/jsx-runtime',
    'plugin:react-hooks/recommended',
  ],
  ignorePatterns: ['dist', '.eslintrc.cjs'],
  parserOptions: { ecmaVersion: 'latest', sourceType: 'module' },
  settings: { react: { version: '18.2' } },
  plugins: ['react-refresh'],
  rules: {
    'react/jsx-no-target-blank': 'off',
    'react-refresh/only-export-components': [
      'warn',
      { allowConstantExport: true },
    ],
    "no-unused-vars":"off",
    "react/prop-types": "off",
  },
}
```

```jsx
import './App.css'

function App() {
  return (
    <>
      카운터앱
    </>
  )
}

export default App;
```

```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './index.css'

ReactDOM.createRoot(document.getElementById('root')).render(
    <App />
)
```

6.2) UI 구현하기

```jsx
import './App.css'
import Viewer from './components/Viewer'
import Controller from './components/Controller'

function App() {
  return (
    <div className='App'>
      <h1>Simple Counter</h1>
      <section>
        <Viewer />
      </section>
      <section>
        <Controller />
      </section>
    </div>
  )
}

export default App
```

```jsx
body{
    padding: 20px;
}

.App {
    margin: 0 auto;
    width: 400px;
}
.App > section {
    background-color: rgb(245, 245, 245);
    border: 1px solid rgb(240, 240, 240);
    border-radius: 5px;
    padding: 20px;
    margin-bottom: 10px;
}
```

```jsx
const Viewer =()=>{
    return <div>
        <div>현재 카운트 :</div>
        <h1>0</h1>
    </div>
}

export default Viewer;
```

```jsx
const Controller = () =>{
    return <div>
        <button>-1</button>
        <button>-10</button>
        <button>-100</button>
        <button>+100</button>
        <button>+10</button>
        <button>+1</button>
    </div>
}

export default Controller;
```

6.3) 기능 구현하기

```jsx
import './App.css'
import Viewer from './components/Viewer'
import Controller from './components/Controller'
import { useState } from 'react'

function App() {

  const [count, setCount] = useState(0);

  const onClickButton = (value) => {
    setCount(count + value);
  }

  return (
    <div className='App'>
      <h1>Simple Counter</h1>
      <section>
        <Viewer count = {count} />
      </section>
      <section>
        <Controller onClickButton={onClickButton} />
      </section>
    </div>
  )
}

export default App
```

```jsx
const Viewer =({count})=>{
    return <div>
        <div>현재 카운트 :</div>
        <h1>{count}</h1>
    </div>
}

export default Viewer;
```

```jsx
const Controller = ({onClickButton}) =>{
    return <div>
        <button
            onClick={() => {
                onClickButton(-1);
            }}
        >
            -1
        </button>
        <button
            onClick={() => {
                onClickButton(-10);
            }}
        >-10</button>
        <button
            onClick={() => {
                onClickButton(-100);
            }}
        >-100</button>
        <button
            onClick={() => {
                onClickButton(+100);
            }}
        >+100</button>
        <button
            onClick={() => {
                onClickButton(+10);
            }}
        >+10</button>
        <button
            onClick={() => {
                onClickButton(+1);
            }}
        >+1</button>
    </div>
}

export default Controller;
```

React.js의 데이터 흐름 = 단방향 데이터 흐름

State Lifting (State 끌어 올리기)

# 섹션 7. 라이프사이클

7.1) 라이프사이클이란?

라이프사이클(LifeCycle) = 생애 주기

리액트 컴포넌트의 라이프사이클

Mount → Update → unMount

<Mount>

 - Like. 탄생

- 컴포넌트가 탄생하는 순간
- 화면에 처음 렌더링 되는 순간

<Update>

 - Like. 변화

- 컴포넌트가 다시 렌더링 되는 순간
- 리렌더링 될 때를 의미

<unMount>

 - Like. 죽음

- 컴포넌트가 화면에서 사라지는 순간
- 렌더링에서 제외 되는 순간을 의미

7.2) useEffect 사용하기

useEffect = 리액트 컴포넌트의 사이드 이펙트를 제어하는 새로운 React Hook

사이드 이펙트 = 부수적인 효과, 파생되는 효과

React 컴포넌트의 사이드 이펙트 = 컴포넌트의 동작에 따라 파생되는 여러 효과

```jsx
import './App.css'
import Viewer from './components/Viewer'
import Controller from './components/Controller'
import { useState,useEffect } from 'react'

function App() {

  const [count, setCount] = useState(0);
  const [input, setInput] = useState("");

  useEffect( ()=>{
    console.log(`count: ${count} / input: ${input}`)
  }, [count, input])
  //의존성 배열
  //dependency array
  //deps

  const onClickButton = (value) => {
    setCount(count + value);
  }

  return (
    <div className='App'>
      <h1>Simple Counter</h1>
      <section>
        <input value={input} onChange={(e)=>{
          setInput(e.target.value)
        }} />
      </section>
      <section>
        <Viewer count = {count} />
      </section>
      <section>
        <Controller onClickButton={onClickButton} />
      </section>
    </div>
  )
}

export default App
```

7.3) useEffect로 라이프사이클 제어하기

```jsx
import './App.css'
import Viewer from './components/Viewer'
import Controller from './components/Controller'
import Even from './components/Even'
import { useState,useEffect,useRef } from 'react'

function App() {

  const [count, setCount] = useState(0);
  const [input, setInput] = useState("");

  const isMount = useRef(false);

  //1. 마운트: 탄생
  useEffect(() => {
    console.log("mount");
  }, [])

  //2. 업데이트: 변화, 리렌더링
  useEffect(() => {
    if(!isMount.current){
      isMount.current = true;
      return;
    }
    console.log("update");
  })

  //3. 언마운트: 죽음

  const onClickButton = (value) => {
    setCount(count + value);
  }

  return (
    <div className='App'>
      <h1>Simple Counter</h1>
      <section>
        <input value={input} onChange={(e)=>{
          setInput(e.target.value)
        }} />
      </section>
      <section>
        <Viewer count = {count} />
        {count % 2 === 0 ? <Even /> : null }
      </section>
      <section>
        <Controller onClickButton={onClickButton} />
      </section>
    </div>
  )
}

export default App
```

```jsx
import { useEffect } from "react";

const Even = () => {
    useEffect(() => {
        //클린업, 정리함수
        return () => {
            console.log("unmount");
        }
    }, [])
    return <div>짝수입니다</div>
}

export default Even;
```

7.4) React 개발자 도구 사용하기