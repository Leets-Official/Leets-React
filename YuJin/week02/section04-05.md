### React.js란?

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/f19ff150-32dd-49fb-8877-2110b34ce9aa/Untitled.png)

### React의 기술적인 특징

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/9e91f242-6026-4fa9-8f58-f63f129f8639/Untitled.png)

**컴포넌트(Component)**

: 화면이나 UI를 구성하는 요소

**업데이트**

: 사용자의 행동(클릭,드래그)에 따라 웹 페이지가 스스로 모습을 바꿔 상호작용 하는 것

### JSX로 UI 표현하기

**JSX(javaScript Extensions)**

: 확장된 자바스크립트의 문법을 말함 JS+HTML

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/84829d3d-ae36-4539-a6ad-c529d2a9430e/Untitled.png)

**Main 컴포넌트**

```jsx

import './Main.css'
//JSX 주의사항
// 1. 중괄호 내부에는 자바스크립트 표현식만 넣을 수 있다.
// 2. 숫자, 문자열, 배열 값만 랜더링 된다.
// 3. 모든 태그는 닫혀 있어야 한다.
// 4. 최상위 태그는 반드시 하나여야 한다. 

const Main=()=>{
    const user={
        name:" 이유진",
        isLogin:true
       };

    if(user.isLogin){
        return <div className="logout"> 로그아웃</div>
    }else{ 
        return <div>로그인</div>
    }
    // return(
    //   <>
    //   {user.isLogin?(<div> 로그아웃</div>):(<div> 로그인</div>)}
    //   </>
    // )
}

export default Main;
```

**Main CSS**

```css
.logout{
    background-color: red;
}
```

## State와 Props

### 1. Props로 데이터 표현하기

**props**

: property의 약자로, 부모에게 받아온 데이터
- 리액트의 Data Flow는 단방향 형식으로 부모에서부터 자식으로 이동하기 때문에 거꾸로 올라갈 수 없음 
- 따라서 props에 있는 데이터들은 수정이 불가능하며 오직 안에있는 값을 꺼내서 사용할수만 있음

**App.jsx**

```
import "./App.css";
import Header from "./components/Header";
import Main from "./components/Main";
import Footer from "./components/Footer";
import Button from "./components/Button";

function App() {
  const buttonProps = {
    text: "메일",
    color: "red",
    a: 1,
    b: 2,
    c: 3,
  };
  return (
    <>
      <Button {...buttonProps} />
      <Button text={"카페"} />
      <Button text={"블로그"}>
        <Header /> //블로그 버튼의 자식요
      </Button>
    </>
  );
}

export default App;
```

**Button.jsx**

```jsx
const Button = ({ text, color, children }) => {
    return (
      <button style={{ color: color }}>
        {text} - {color.toUpperCase()}
        {children}
      </button>
    );
  };
  
  Button.defaultProps = {
    color: "black",
  };
  
  export default Button;
```

### 2. 이벤트 처리하기

**Event Handling**

: 이벤트가 발생했을 때 그것을 처리하는 것
ex) 버튼 클릭시 경고창 노출

**Button.jsx**

```jsx
const Button = ({ text, color, children }) => {
    // 이벤트 객체 :  발생한 이벤트의 정보들을 담아둠
    const onClickButton = (e) => {
      console.log(e);
      console.log(text);
    };
  
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
  };
  
  Button.defaultProps = {
    color: "black",
  };
  
  export default Button;
```

### 3. State로 상태 관리하기

**State**

: 현재 가지고 있는 형태나 모양을 정의, 변화할 수 있는 동적인 값

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/84c3fed8-20e9-485c-8ef9-cc851c74d315/Untitled.png)

**App.jsx**

```jsx
import "./App.css";
import { useState } from "react";

function App() {
  // count = userState()를 통해 생성한 값
  // setState = state의 값을 변경하는 함수 
  const [count, setCount] = useState(0);
  // let이나  const를 사용하면 rerendering이 되지 않아서 화면에 변화가 나타나지 않음
  const [light, setLight] = useState("OFF");

  return (
    <>
      <div>
        <h1>{light}</h1>
        <button
          onClick={() => {
            setLight(light === "ON" ? "OFF" : "ON");
          }}
        >
          {light === "ON" ? "끄기" : "켜기"}
        </button>
      </div>

      <div>
        <h1>{count}</h1>
        <button
          onClick={() => {
            setCount(count + 1);
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

### 4. State와 Props

**rerendering 조건**

- State 변경
- Props 변경
- 부모 컴포넌트가 리렌더링 될때

함수마다 컴포넌트를 따로 만들어서 관리해주자!

### 5. (1) State로 사용자 입력 관리

**Register.jsx**

```jsx
import { useState } from "react";

// 간단한 회원가입 폼
// 1. 이름
// 2. 생년월일
// 3. 국적
// 4. 자기소개

const Register = () => {
  const [name, setName] = useState("이름");
  const [birth, setBirth] = useState("");
  const [country, setCountry] = useState("");
  const [bio, setBio] = useState("");

  const onChangeName = (e) => {
    setName(e.target.value);
  };

  const onChangeBirth = (e) => {
    setBirth(e.target.value);
  };

  const onChangeCountry = (e) => {
    setCountry(e.target.value);
  };

  const onChangeBio = (e) => {
    setBio(e.target.value);
  };

  return (
    <div>
      <div>
        <input
          value={name}
          onChange={onChangeName}
          placeholder={"이름"}
        />
      </div>

      <div>
        <input
          value={birth}
          onChange={onChangeBirth}
          type="date"
        />
      </div>

      <div>
        <select value={country} onChange={onChangeCountry}>
          <option value=""></option>
          <option value="kr">한국</option>
          <option value="us">미국</option>
          <option value="uk">영국</option>
        </select>
        {country}
      </div>

      <div>
        <textarea value={bio} onChange={onChangeBio} />
      </div>
    </div>
  );
};

export default Register;
```

### 6. (2) State로 사용자 입력 관리

**Register.jsx**

중복 코드 정리

```jsx
import { useState } from "react";
// 간단한 회원가입 폼
// 1. 이름
// 2. 생년월일
// 3. 국적
// 4. 자기소개

const Register = () => {
    
  const [input, setInput] = useState({
    name: "",
    gender: "",
    bio: "",
  });

  const onChange = (e) => {
    console.log(e.target.name + " : " + e.target.value);
    setInput({
      ...input,
      [e.target.name]: e.target.value,
    });
  };

  return (
    <div>
      <div>
        <input
          name="name"
          value={input.name}
          onChange={onChange}
          placeholder={"이름"}
        />
      </div>

      <div>
        <input
          name="birth"
          value={input.birth}
          onChange={onChange}
          type="date"
        />
      </div>

      <div>
        <select
          name="country"
          value={input.country}
          onChange={onChange}
        >
          <option value=""></option>
          <option value="kr">한국</option>
          <option value="us">미국</option>
          <option value="uk">영국</option>
        </select>
      </div>

      <div>
        <textarea
          name="bio"
          value={input.bio}
          onChange={onChange}
        />
      </div>
    </div>
  );
};

export default Register;
```

## useRef로 컴포넌트 변수 생성하기

**userRef**

: 새로운 reference 객체를 생성하는 기능

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/c04e1a14-b441-4af4-9c35-d8d95508530a/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/62668e89-9e25-40c6-9486-9989dfa0b156/Untitled.png)

**Register.jsx**

```jsx
import { useState, useRef } from "react";

// 간단한 회원가입 폼
// 1. 이름
// 2. 생년월일
// 3. 국적
// 4. 자기소개

const Register = () => {
  const [input, setInput] = useState({
    name: "",
    birth: "",
    country: "",
    bio: "",
  });

  // useState나 userRef는 컴포넌트가 리렌더링 되어도 리셋되지 않음 
  // component 뢰부에 변수 선언 하는 건 권장하지 않음
  const countRef = useRef(0);
  const inputRef = useRef();

  const onChange = (e) => {
    countRef.current++;
    setInput({
      ...input,
      [e.target.name]: e.target.value,
    });
  };

  const onSubmit = () => {
    if (input.name === "") {
      // 이름을 입력하는 DOM 요소 포커스(커서가 올라간 상태)
      inputRef.current.focus();
    }
  };

  return (
    <div>
      <div>
        <input
          ref={inputRef}
          name="name"
          value={input.name}
          onChange={onChange}
          placeholder={"이름"}
        />
      </div>

      <div>
        <input
          name="birth"
          value={input.birth}
          onChange={onChange}
          type="date"
        />
      </div>

      <div>
        <select
          name="country"
          value={input.country}
          onChange={onChange}
        >
          <option value=""></option>
          <option value="kr">한국</option>
          <option value="us">미국</option>
          <option value="uk">영국</option>
        </select>
      </div>

      <div>
        <textarea
          name="bio"
          value={input.bio}
          onChange={onChange}
        />
      </div>

      <button onClick={onSubmit}>제출</button>
    </div>
  );
};

export default Register;
```

## React Hooks

React Hooks

: 클래스 컴포넌트에서만 가능했던 상태 관리 및 생명 주기 메서드를 함수형 컴포넌트에서도 사용할 수 있도록 도와주는 기능

함수 컴포넌트 내부에서만 호출 가능

반복문, 조건문 호출 불가능

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/98c0a4d5-03bd-4fb1-935e-326887826ce1/Untitled.png)

**HookExam.js**

```jsx
import useInput from "./../hooks/useInput";

// 3가지 hook 관련된 팁
// 1. 함수 컴포넌트, 커스텀 훅 내부에서만 호출 가능
// 2. 조건부로 호출될 수는 없다
// 3. 나만의 훅(Custom Hook) 직접 만들 수 있다. 함수 이름을 use~로 만들면 됨

const HookExam = () => {
  const [input, onChange] = useInput();
  const [input2, onChange2] = useInput();

  return (
    <div>
      <input value={input} onChange={onChange} />
      <input value={input2} onChange={onChange2} />
    </div>
  );
};

export default HookExam;
```

**useInput.jsx → 커스텀 훅**

```jsx
import { useState } from "react";

function useInput() {
  const [input, setInput] = useState("");

  const onChange = (e) => {
    setInput(e.target.value);
  };

  return [input, onChange];
}

export default useInput;
```