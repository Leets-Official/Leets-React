# 2주차 스터디

- Props (5-4)
    
    부모 컴포넌트가 자식 컴포넌트에게 함수에 인수를 전달하듯 원하는 값을 전달할 수 있는데, 이때의 값을 말함.
    

1. 버튼 컴포넌트 만들기

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/3556d1e2-d2af-4345-b2d2-8cfff9a6c553/Untitled.png)

```jsx
const Button = () => {
    return <button>클릭</button>
};

export default Button;
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/3ab73cd9-4248-4b0b-ba7e-14a3cfc82fd4/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/05c8f59b-ab33-40a0-8c4e-5d1cc1d35049/Untitled.png)

결과

![IMG_1904.jpeg](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/eab8b51a-31a3-4d3f-bcd9-bf9eae0a3d5d/deedf5fa-71fa-4546-9d02-81e3a3fa229a.png)

- 더 쉽게 사용하는 법
    
    ![객체로 만들](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/244d2f59-e850-4df4-b8c6-75c1cf8430e7/Untitled.png)
    
    객체로 만들
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/feed74bd-2c2a-48a7-b0b9-ebae23911824/Untitled.png)
    

- 이벤트 핸들링
    - 이벤트: 웹 내부에서 발생하는 사용자의 행동
        
        ex) 버튼 클릭, 메세지 입력, 스크롤 등
        
    
    이벤트가 발생했을 때 그것을 처리하는 것
    
    ex) 버튼 클릭시 경고창 노출
    
- 이벤트 핸들러
    
    ![onClick과 같은 이벤트를 발생시키는 화살표 함수를 이벤트 핸들러라고 함](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/394c258c-7997-450b-ba1e-cb06985cd068/Untitled.png)
    
    onClick과 같은 이벤트를 발생시키는 화살표 함수를 이벤트 핸들러라고 함
    
    ![이렇게 해도 됨](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/3f896c6b-3b7f-4d0f-aa93-f5e5989134ea/Untitled.png)
    
    이렇게 해도 됨
    
- State
    - 사물이 현재 가지고 있는 상태. 변화할 수 있는 동적인 값
    - 리액트의 모든 컴포넌트는 모두 state를 가질 수 있음
    - 리 렌더(리 렌더링): 컴포넌트가 다시 렌더링 되는 것
    - state 만들기 (App.jsx)
        
        ```jsx
        export default App;import './App.css'
        import { useState } from "react"; //리액트에서 state 생성
        
        function App() {
          const [state, setSate] = useState(0); // state에는 useState(0)값을, setState에는 함수를
          console.log(state);
        
          return (
            <>
        	    <h1>{state}</h1> //값을 호출
            </>
          );
        }
        
        export default App;
        
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
        

- 사용자의 입력 처리하기
    1. 레지스터 컴포넌트 만들기
    
    ```jsx
    const Register = () => {
        return <div>register</div>
    };
    
    export default Register;
    ```
    
    1. 
    
    ```
    import "./App.css";
    import { useState } from "react";
    
    import Register from "./components/Register";
    
    function App() {
    
      return (
        <>
          <Register />
        </>
      );
    }
    
    export default App;
    ```
    
    여기서부터
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/0bc85c37-4c3b-4ecf-a268-a12e0d362957/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/2813d1a0-e262-436f-8029-7967743d0930/Untitled.png)
    
    # 06. 카운터 앱
    
    만들어야 하는 프로젝트는 다음과 같음
    
    ![IMG_1905.jpeg](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/66996c17-bd66-4950-815c-ea0959330e1c/IMG_1905.jpeg)
    
    1. 뷰어 컴포넌트 
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/9c983b45-5a21-4882-b220-bfa40411d1c7/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/81cabc9a-6052-4b42-ae5f-0ac5eb2890b9/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/985b5d31-289e-40f4-8112-5c4f1e660a30/Untitled.png)
    
    1. 컨트롤러 컴포넌트
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/5e1a7d92-75b0-41fc-a8fc-44b41176a83b/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/40aa0dcc-5d0d-4f87-baab-924a104800bb/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/f7ea9a2d-ca9b-4169-9252-6dee7fffb830/Untitled.png)
    
    1. css 설정하기
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/eb0ad767-81f3-4127-94f1-93c1df9068ee/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/875694b2-b8b8-4fd0-a8cc-665d77295312/Untitled.png)
    
    ![App.css](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/c1db4419-7ab2-484b-a130-81ee131f7b83/Untitled.png)
    
    App.css
    
    margin-bottom은 중간 간격을 말함
    
    ![IMG_1907.jpeg](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/e7c196ca-0ea2-4e3f-a6ae-05726be338d2/IMG_1907.jpeg)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/d2307b44-84c9-4305-acbc-16c3f62eeba2/Untitled.png)
    
    margin을 0 auto로 설정하면 화면상의 남는 여백을 자동으로 마진을 설정. 요소를 가운데로 배치되도록 함.
    
    ![IMG_1908.jpeg](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/34fe2d97-a307-4bcc-b5f9-a642c1320325/IMG_1908.jpeg)
    
1. 기능 구현하기 (6.3)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/ab78dd30-e2d1-4921-bc4f-328a9fdfd28b/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/f82a8df9-108e-4d90-9686-6dec6eafb2ba/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/6ca1117b-fcd6-449a-a69b-0857fe5cc71a/Untitled.png)
    

# 07. 라이프사이클

라이프사이클(LifeCycle) = 생애 주기

리액트로 생애 주기가 있음. 

![IMG_1909.jpeg](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/310facd4-81c0-4880-931f-ccbe6d030eb1/IMG_1909.jpeg)

- Mount
    - Like. 탄생
    - 컴포넌트가 탄생하는 순간
    - 화면에 처음 렌더링 되는 순간
        
        “A 컴포넌트가 Mount 되었다” → A 컴포넌트가 화면에 처음으로 렌더링 되었다
        
- Update
    - Like. 변화
    - 컴포넌트가 다시 렌더링 되는 순간
    - 리렌더링 될 때를 의미
        
        “A 컴포넌트가 업데이트 되었다” → A 컴포넌트가 리렌더링 되었다
        
- UnMount
    - Like. 죽음
    - 컴포넌트가 화면에서 사라지는 순간
    - 렌더링에서 제외 되는 순간을 의미
        
        “A 컴포넌트가 언마운트 되었다” → A 컴포넌트가 화면에서 사라졌다
        

- useEffect
    
    리액트 컴포넌트의 사이드 이펙트를 제어하는 새로운 React Hook
    
    - 사이드 이펙트: (부작용) 리액트에서는 “부수적인 효과”, “파생되는 효과”
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/25f33456-ab08-4fdb-a7e3-2d94dddb1c5c/Untitled.png)
    
    setCount 함수는 비동기로 작동. (함수를 호출한 곳보다 뒤늦게 호출됨)
    
    → 변경된 값을 바로 사용하려면 useEffect를 사용해야 함
    
- useEffect로 라이프사이클 제어하기
    
    ```jsx
    //1. 마운트: 탄생
      useEffect(() => {
        console.log("mount");
      }, []);
    
    ```
    
    ```jsx
    //2. 업데이트 : 변화, 리렌더링
      useEffect(() => {
        if (!isMount.current){
          isMount.current =true;
          return;
        }
        console.log("update");
      });
    ```
    
    ```jsx
    //3. 언마운트: 죽음
      const onClickButton = (value)=> {
        setCount(count + value);
      };
      
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/dc68473f-8bae-4c80-940e-6a8a8441d963/c2b45826-3633-4f6e-8383-0bb64706614f/Untitled.png)
    
- 리액트 개발자 도구 사용하기