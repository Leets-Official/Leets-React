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