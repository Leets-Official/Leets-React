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

# React.js 입문

## component

html태그를 반환하는 함수

컴포넌트 함수의 첫글자는 무조건 대문자여야함!

```jsx
import "./App.css";

const Header = () => {
  return (
    <header>
      <h1>header</h1>
    </header>
  );
};

function App() {
  return (
    <>
      <Header />
      <h1>안녕 리액트!</h1>
    </>
  );
}

export default App;
```

App : root component

## jsx

1. 중괄호 내에는 js 표현식만 넣을 수 있다
2. 숫자, 문자열, 배열 값만 렌더링 된다
3. 모든 태그는 닫혀있어야 한다
4. 최상위 태그는 반드시 하나여야 한다 - 묶을만한 태그가 없다면 빈 태그로 묶어도

```jsx
const Main = () => {
    const number = 9;
    const obj = { a: 1};

    return (
        <main>
            <h1>main</h1>
            <h2>{number % 2 === 0 ? "짝수" : "홀수"}</h2>

            {10}
            {number}
            {[1,2,3]}

            //오류는 발생하지 않지만, 화면에 렌더링 되지 않음
            {true}
            {undefined}
            {null}

            //오류 발생
            {if(){}}
            {for(){}}

            //오브젝트의 경우에는 렌더링 불가능
            //점표기법 등을 이용하여 문자열/숫자 값을 렌더링하도록 해야
            {obj}
        </main>
    )
};

export default Main;
```

### 값에 따라 UI를 다르게 설정하기

```jsx
const Main = () => {
  const user = {
    name: "이정환",
    isLogin: true,
  };

  return <>{user.isLogin ? <div>로그아웃</div> : <div>로그인</div>}</>;
};

export default Main;
```

### 스타일 설정하기 - css파일을 만들어서 import하는 방식도 가능!

```jsx
const Main = () => {
  const user = {
    name: "이정환",
    isLogin: true,
  };

  if (user.isLogin) {
    return (
      <div
        style={{
          backgroundColor: "red",
          borderBottom: "5px soild blue",
        }}
      >
        로그아웃
      </div>
    );
  }
};

export default Main;
```

## Props

props 이용하기

```jsx
import './App.css';
import Header from './components/Header';
import Main from './components/Main';
import Footer from './components/Footer';
import Button from './components/Button';

function App() {
  return (
    <>
      <Button text={"메일"} color={"red"}/>
      <Button text={"카페"}/>
      <Button text={"블로그"}>
    </>
  );
}

export default App;
```

```jsx
const Button = (props) => {
  console.log(props);
  return (
    <button style={{ color: props.color }}>
      {props.text} - {props.color.toUpperCase()}
    </button>
  );
};

Button.defaultProps = {
  color: "black",
};

export default Button;
```

defaultProps를 사용하면 props.color의 값이 없는 경우에도 오류가 발생하지 않음!

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
    a: 1,
    b: 2,
    c: 3,
  };
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

## 이벤트 핸들링

```jsx
<button
  onClick={() => {
    console.log(text);
  }}
  style={{ color: color }}
>
  {text} - {color.toUpperCase()}
  {children}
</button>
```

onClick : 클릭하면

onMouseEnter : 마우스를 가져다대면

합성 이벤트 : 모든 웹 브라우저의 이벤트 객체를 하나로 통일한 형태

## state

state의 값에 따라서 렌더링 되는 UI가 결정된다!

```jsx
import { useState } from "react";
```

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

+버튼을 누르면 리액트가 App 컴포넌트의 state가 변경되었다고 감지 → 컴포넌트를 리렌더링

그냥 변수를 쓰면 될 것 같은데 state를 쓰는 이유?

→ 변수는 값이 변해도 리렌더링이 일어나지 않기 때문!

```jsx
import "./App.css";
import { useState } from "react";

const Bulb = ({ light }) => {
  return (
    <div>
      {light === "ON" ? (
        <h1 style={{ backgroundColor: "orange" }}>ON</h1>
      ) : (
        <h1 style={{ backgroundColor: "gray" }}>OFF</h1>
      )}
    </div>
  );
};

function App() {
  const [count, setCount] = useState(0);
  const [light, setLight] = useState("OFF");

  return (
    <>
      <div>
        <Bulb light={light} />
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

자식 컴포넌트는 부모로부터 받는 props의 값이 바뀌면 리렌더링이 일어남

리렌더링이 일어나는 경우

1. 자신이 가진 state가 변경
2. 자신이 받는 props의 값이 변경
3. 부모 컴포넌트가 리렌더링 된 경우 자식 컴포넌트도 리렌더링 발생

→ 위의 코드처럼 작성하면 불필요한 리렌더링이 계속 발생하기 때문에 비효율적임.

따라서 아래와 같이 수정하는 편이 👍🏻

```jsx
import "./App.css";
import { useState } from "react";

const Bulb = () => {
  const [light, setLight] = useState("OFF");

  return (
    <div>
      {light === "ON" ? (
        <h1 style={{ backgroundColor: "orange" }}>ON</h1>
      ) : (
        <h1 style={{ backgroundColor: "gray" }}>OFF</h1>
      )}

      <button
        onClick={() => {
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
        onClick={() => {
          setCount(count + 1);
        }}
      >
        +
      </button>
    </div>
  );
};

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

### state를 통해 값을 보관하는 방법

```jsx
import { useState } from "react";

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
        <input value={name} onChange={onChangeName} placeholder={"이름"} />
      </div>

      <div>
        <input value={birth} onChange={onChangeBirth} type="date" />
      </div>

      <div>
        <select value={country} onChange={onChangeCountry}>
          <option></option>
          <option value="kr">한국</option>
          <option value="us">미국</option>
          <option value="uk">영국</option>
        </select>
      </div>

      <div>
        <textarea value={bio} onChange={onChangeBio} />
      </div>
    </div>
  );
};

export default Register;
```

```jsx
import { useState } from "react";

const Register = () => {
  const [input, setInput] = useState({
    name: "",
    birth: "",
    country: "",
    bio: "",
  });

  const onChangeName = (e) => {
    setInput({
      ...input,
      name: e.target.value,
    });
  };

  const onChangeBirth = (e) => {
    setInput({
      ...input,
      birth: e.target.value,
    });
  };

  const onChangeCountry = (e) => {
    setInput({
      ...input,
      country: e.target.value,
    });
  };

  const onChangeBio = (e) => {
    setInput({
      ...input,
      bio: e.target.value,
    });
  };

  return (
    <div>
      <div>
        <input
          value={input.name}
          onChange={onChangeName}
          placeholder={"이름"}
        />
      </div>

      <div>
        <input value={input.birth} onChange={onChangeBirth} type="date" />
      </div>

      <div>
        <select value={input.country} onChange={onChangeCountry}>
          <option></option>
          <option value="kr">한국</option>
          <option value="us">미국</option>
          <option value="uk">영국</option>
        </select>
      </div>

      <div>
        <textarea value={input.bio} onChange={onChangeBio} />
      </div>
    </div>
  );
};

export default Register;
```

## → 정리한 코드

```jsx
import { useState } from "react";

const Register = () => {
  const [input, setInput] = useState({
    name: "",
    birth: "",
    country: "",
    bio: "",
  });

  const onChange = (e) => {
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
        <select name="country" value={input.country} onChange={onChange}>
          <option></option>
          <option value="kr">한국</option>
          <option value="us">미국</option>
          <option value="uk">영국</option>
        </select>
      </div>

      <div>
        <textarea name="bio" value={input.bio} onChange={onChange} />
      </div>
    </div>
  );
};

export default Register;
```

## useRef

- refObj.current의 값이 NaN으로 나옴..ㅜㅜ

```jsx
import { useState, useRef } from "react";

const Register = () => {
  const [input, setInput] = useState({
    name: "",
    birth: "",
    country: "",
    bio: "",
  });

  const refObj = useRef(0);
  console.log(refObj);

  const onChange = (e) => {
    setInput({
      ...input,
      [e.target.name]: e.target.value,
    });
  };

  return (
    <div>
      <button
        onClick={() => {
          refObj.current++;
          console.log(refObj.current);
        }}
      >
        ref+1
      </button>

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
        <select name="country" value={input.country} onChange={onChange}>
          <option></option>
          <option value="kr">한국</option>
          <option value="us">미국</option>
          <option value="uk">영국</option>
        </select>
      </div>

      <div>
        <textarea name="bio" value={input.bio} onChange={onChange} />
      </div>
    </div>
  );
};

export default Register;
```

## Hooks

- 이름 앞에 동일한 접두사 use가 붙음
- 함수컴포넌트 내에서만 호출 가능
- 조건문, 반복문 내부에서는 호출 불가
- custom hook 제작 가능 (함수 이름 앞ㅊ에 use만 붙이면 됨!)

</br>

### 질문
