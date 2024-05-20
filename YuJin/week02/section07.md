### 라이프 사이클(Life Cycle)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/a24f5033-b9f1-439c-ad3c-fe386ac20c94/Untitled.png)

1. **Mount(탄생)**
: 컴포넌트가 탄생하는 순간
화면에 처음 렌더링 되는 순간
2. **Update(변화)**
: 컴포넌트가 다시 렌더링 되는 순간
리렌더링 될 
3. **UnMount(죽음)**
: 컴포넌트가 화면에서 사라지는 순간
렌더링에서 제외되는 순간

### useEffect

useEffect

: 리액트 컴포넌트의 사이드 이펙트(부수적 효과)를 제어하는 새로운 React Hook

```jsx
import "./App.css";
import Viewer from "./components/Viewer";
import Controller from "./components/Controller";
import { useState,useEffect } from "react";

function App() {
  const [count, setCount] = useState(0);
  const [input, setInput] = useState("");

  useEffect(()=>{

  },[count,input]);
  //의존성 배열
  //dependency array
  //deps

  const onClickButton = (value) => {
    // 비동기로 동작
    setCount(count + value);
  };

  return (
    <div className="App">
      <h1>Simple Counter</h1>
      <section>
        <input
        value={input}
        onChange={(e)=>{
          setInput(e.target.value);
        }}
        />
      </section>
      <section>
        <Viewer count={count} />
      </section>
      <section>
        <Controller onClickButton={onClickButton} />
      </section>
    </div>
  );
}

export default App;
```

### useEffect로 라이프 사이클 제어하기

```jsx
import "./App.css";
import "./components/Even"
import Viewer from "./components/Viewer";
import Controller from "./components/Controller";
import { useState,useEffect,userRef} from "react";

function App() {
  const [count, setCount] = useState(0);
  const [input, setInput] = useState("");

  const isMount = userRef(false);

  // 1. 마운트 : 탄생
  useEffect(()=>{
    console.log("mount");
  },[]);

  // 2. 업데이트 : 변화, 리렌더링
  useEffect(()=>{
    if(!isMount.current){
      isMount.current = true;
      return;
    }
    console.log("update");
  });

  // 3. 언마운트 : 죽음

  //의존성 배열
  //dependency array
  //deps

  const onClickButton = (value) => {
    // 비동기로 동작
    setCount(count + value);
  };

  return (
    <div className="App">
      <h1>Simple Counter</h1>
      <section>
        <input
        value={input}
        onChange={(e)=>{
          setInput(e.target.value);
        }}
        />
      </section>
      <section>
        <Viewer count={count} />
        {count%2===0?<Even/>:null}
      </section>
      <section>
        <Controller onClickButton={onClickButton} />
      </section>
    </div>
  );
}

export default App;
```

```jsx
import { useState,useEffect,userRef} from "react";

const Even = () =>{
    useEffect(()=>{
        //클린업, 정리함수
        return()=>{
            console.log("unmount");
        }

    },[]);

    return <div>짝수 입니다!</div>
};
export default Even;
```