# 3주차

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

# section8. 프로젝트2 : 투두리스트

## App.jsx

```jsx
import "./App.css";
import Header from "./components/Header";
import Editor from "./components/Editor";
import List from "./components/List";

import { useState, useRef } from "react";

const mockData = [
  {
    id: 0,
    isDone: false,
    content: "React 공부하기",
    date: new Date().getTime(),
  },
  {
    id: 1,
    isDone: false,
    content: "빨래하기",
    date: new Date().getTime(),
  },
  {
    id: 2,
    isDone: false,
    content: "노래 연습하기",
    date: new Date().getTime(),
  },
];

function App() {
  const [todos, setTodos] = useState(mockData);
  const idRef = useRef(3);

  const onCreate = (content) => {
    const newTodo = {
      id: idRef.current++,
      isDone: false,
      content: content,
      date: new Date().getTime(),
    };

    setTodos([newTodo, ...todos]);
  };

  return (
    <div className="App">
      <Header />
      <Editor onCreate={onCreate} />
      <List />
    </div>
  );
}

export default App;
```

- mockData
  함수가 제대로 작동하는지 확인하기 위한 임의의 값을 설정
- useState
  todos : 상태 / 투두가 저장되어있는 배열
  setTodos : todos를 변경하기 위한 함수
- idRef
  😂😂😂😂
- onCreate
  content를 매개변수로 받아 newTodo라는 객체를 생성
  newTodo{
  id : idRef의 current값으로 설정, 설정한 후 값을 증가시킨다isDone : 투두가 완료되었는지 여부를 설정, default값은 false
  content : 매개변수로 받은 content의 값으로 설정
  date : 오늘 날짜로 설정
  Editor에 props로 전
- setTodos
  어떻게하면 안된다고했는데…
  [newTodo, …todos]
  todos배열을 spread하고, newTodo를 배열의 가장 앞에 추가

## Header.jsx

```jsx
import "./Header.css";

const Header = () => {
  return (
    <div className="Header">
      <h3>오늘은🫡</h3>
      <h1>{new Date().toDateString()}</h1>
    </div>
  );
};

export default Header;
```

## Editor.jsx

```jsx
import "./Editor.css";
import { useState, useRef } from "react";

const Editor = ({ onCreate }) => {
  const [content, setContent] = useState("");
  const contentRef = useRef();

  const onChangeContent = (e) => {
    setContent(e.target.value);
  };

  const onKeydown = (e) => {
    if (e.keyCode === 13) {
      onSubmit();
    }
  };

  const onSubmit = () => {
    if (content === "") {
      contentRef.current.focus();
      return;
    }
    onCreate(content);
    setContent("");
  };

  return (
    <div className="Editor">
      <input
        ref={contentRef}
        value={content}
        onChange={onChangeContent}
        onKeyDown={onKeydown}
        placeholder="새로운 Todo..."
      />
      <button onClick={onSubmit}>추가</button>
    </div>
  );
};

export default Editor;
```

onCreate를 props로 받음

- useState
  content : 상태 / 투두의 내용이 저장된 문자열
  setContent : todos를 변경하기 위한 함수
- onChangeContent
  이벤트 객체 e를 매개변수로 받아와서 setContent 호출
- onKeydown
  엔터를 눌렀을 때 (e.KeyCode === 13)
  입력이 되도록 설정 (onSubmit 호출)
- onSubmit
  입력란이 비어있다면 submit을 하지 않게 설정
  onCreate를 호출하여 새로운 투두를 생성
  생성 후 입력란 비우기
- contentRef
  입력란이 비어있을 때 ,input창에 focus를 하기 위해 생성

## List.jsx

```jsx
import "./List.css";
import TodoItem from "./TodoItem";
import { useState } from "react";

const List = ({ todos }) => {
  const [search, setSearch] = useState("");

  const onChangeSearch = (e) => {
    setSearch(e.target.value);
  };

  const getFilteredData = () => {
    if (search === "") return todos;
    return todos.filter((todo) =>
      todo.content.toLowerCase().includes(search.toLowerCase())
    );
  };

  const filteredTodos = getFilteredData();

  return (
    <div className="List">
      <h4>할 일 목록🌱</h4>
      <input
        value={search}
        onChange={onChangeSearch}
        placeholder="검색어를 입력하세요"
      />
      <div className="todos_wrapper">
        {filteredTodos.map((todo) => {
          return <TodoItem key={todo.id} {...todo} />;
        })}
      </div>
    </div>
  );
};

export default List;
```

- onChangeSearch
  이벤트 객체를 매개변수로 받아 setSearch 호출
- getFilteredData
  검색결과를 반환하는 함수
  검색창에 입력된 값이 없다면 return(=함수실행안함)
  todos를 필터링 → todo.content가 search를 포함하고 있는가?
  💡toLowerCase()를 통해 todo.content와 search를 모두 소문자로 하여 대소문자 구분없이 검색할 수 있도록 함
- filteredTodos.map - 배열
  리스트 형태로 렌더링 된 컴포넌트나 요소들을 구분할 때 key라는 props를 통해서 구분함
  → 리스트 형태로 렌더링 하기 위해서는 반드시 key라는 props를 고유값으로 전달해줘야함 - 이 프로젝트에서는 id 값 전달

## TodoItem.jsx

```jsx
import "./TodoItem.css";

const TodoItem = () => {
  return (
    <div className="TodoItem">
      <input type="checkbox" />
      <div className="content">Todo..</div>
      <div className="Date">Date</div>
      <button>삭제</button>
    </div>
  );
};
export default TodoItem;
```

# section9. useReducer

컴포넌트 내부에 새로운 State를 생성하는 React Hook

모든 useState는 useReducer로 대체 가능

<aside>
✨ 상태 관리 코드를 컴포넌트 외부로 분리할 수 있음

</aside>

복잡한 건 useReducer를 쓰는 게 좋음

간단한거라면 useState를 써도 좋음! 골라서 쓰면 돼,,

```jsx
import { useReducer } from "react";

function reducer(state, action) {
  switch (action.type) {
    case "CREATE":
      return [action.data, ...state];
    case "UPDATE":
      return state.map((item) =>
        item.id === action.targetId ? { ...item, isDone: !item.isDone } : item
      );
    case "DELETE":
      return state.filter((item) => item.id !== action.targetId);
    default:
      return state;
  }
}

function App() {
  const [todos, dispatch] = useReducer(reducer, mockData);
  const idRef = useRef(3);

  const onCreate = (content) => {
    dispatch({
      type: "CREATE",
      data: {
        id: idRef.current++,
        isDone: false,
        content: content,
        date: new Date().getTime(),
      },
    });
  };

  const onUpdate = (targetId) => {
    dispatch({
      type: "UPDATE",
      targetId: targetId,
    });
  };

  const onDelete = (targetId) => {
    dispatch({
      type: "DELETE",
      targetId: targetId,
    });
  };

  //...후 략
}
```

dispatch : reducer 함수에 정의된 액션을 보내는 역할을 함

reducer : state(상태)와 action을 인자로 받아서 상태를 어떻게 업데이트 할지 결정 → reducer가 반환한 새로운 상태가 todos에 반영, 컴포넌트 리렌더

# section10. 최적화

### 최적화란? 웹 서비스의 성능을 개선하는 모든 행위

ex)

**일반적인 웹 서비스** : 서버 응답 속도 개선 / 이미지, 폰트, 코드 파일 등의 정적 파일 로딩 개선 / 불필요한 네트워크 요청 줄임

**리액트 앱 내부** : 컴포넌트 내부의 불필요한 연산 방지 / 컴포넌트 내부의 불필요한 함수 재생성 방지 / 컴포넌트의 불필요한 리렌더링 방지

## useMemo

메모이제이션(\*기억해두기) 기법을 기반으로 불필요한 연산을 최적화하는 리액트 훅

```jsx
const getAnalyzedData = () => {
  const totalCount = todos.length;
  const doneCount = todos.filter((todo) => todo.isDone).length;
  const notDoneCount = totalCount - doneCount;

  return {
    totalCount,
    doneCount,
    notDoneCount,
  };
};

const { totalCount, doneCount, notDoneCount } = getAnalyzedData();
```

❗filter는 배열 내 전체 요소를 순회하는 메서드 → todos state에 저장된 값이 증가할수록 함수가 오래 걸림

list component에서 state를 관리하는 검색바에 react를 검색하면, getAnalyzedData함수는 5번 호출됨 → 값을 입력할 때마다 함수를 새롭게 호출

todo data의 변화와 관계 없지만, 다시호출하게 되므로 비효율적임

```jsx
const { totalCount, doneCount, notDoneCount } = useMemo(() => {
  const totalCount = todos.length;
  const doneCount = todos.filter((todo) => todo.isDone).length;
  const notDoneCount = totalCount - doneCount;

  return {
    totalCount,
    doneCount,
    notDoneCount,
  };
}, [todos]);
```

- useMemo는 첫번째 콜백함수가 반환하는 값을 그대로 반환해줌 → 구조분해할당 가능
- 콜백함수를 deps를 기준으로 메모이제이션
- deps로 아무것도 전달하지 않은 경우에는 연산 수행 및 값 반환이 컴포넌트가 최초로 렌더링 되었을 때 한 번만 일어남
- 이와 같은 경우에 deps로 아무것도 전달하지 않으면 todos의 state가 변하더라도(todo 추가, 삭제, done 변경) 연산이 실행되지 않음! → **deps로 todos를 전달하여 해결**

## React.memo

컴포넌트를 인수로 받아 최적화된 컴포넌트로 만들어 반환

```jsx
const MEmoizedComponent = memo(Component);
```

memo 메서드가 받는 props가 바뀌지 않으면 리렌더링 하지 않음

TodoItem에 memo 메서드를 사용했는데도 모두 리렌더링 되는 이유?

- todos state를 바꾸게 되면, App 컴포넌트가 리렌더링 됨
- App 컴포넌트 내에 있는 onCreate, onUpdate, onDelete 함수들도 새롭게 만들어짐

💡 함수는 객체 타입이고, 컴포넌트가 리렌더링 되면서 재생성되면 주소값이 변하여 같은 동작을 하더라도 다른 값으로 판단

💡 memo 메서드는 props 값의 변화를 얕은 비교 → object 타입은 항상 다른 값으로 판단

→ memo를 사용해도 리렌더링 발생

객체 타입을 props로 가지고 있는 컴포넌트는 memo 메서드를 사용하여도 최적화가 제대로 진행되지 않음.. **해결방법!**

1. App 컴포넌트 내에서 함수들을 메모이제이션 해서 리렌더링 되더라도 재생성 되지 않도록 방지 - **useCallback**
2. 메모함수에 매개변수로 콜백함수를 추가하여 최적화 기능 커스터마이징

   ```
   export default memo(TodoItem, (prevProps, nextProps) => {
       // 반환값에 따라 Props가 바뀌었는지 판단
       // T -> Props 바뀌지 않음 -> 리렌더링 X
       // F -> Props 바뀜 -> 리렌더링 O

       if(prevProps.id !== nextProps.id) return false;
       if(prevProps.isDone !== nextProps.isDone) return false;
       if(prevProps.content !== nextProps.content) return false;
       if(prevProps.date !== nextProps.date) return false;

       return true;

   });
   ```

## useCallback

- memo는 객체타입의 props를 전달할 때 최적화가 제대로 진행되지 않는 단점을 보완

```jsx
const func = useCallback(() => {}, []);
```

- 첫번째 인수는 최적화하고 싶은 함수를 콜백함수로, 두번째 인수는 deps를 전달
- 첫번째 인수로 전달받은 콜백함수를 그대로 반환해줌
- deps가 변경되었을 때만 재생성하도록 최적화 (=함수 메모이제이션)

```jsx
const onCreate = useCallback((content) => {
  dispatch({
    type: "CREATE",
    data: {
      id: idRef.current++,
      isDone: false,
      content: content,
      date: new Date().getTime(),
    },
  });
}, []);

const onUpdate = useCallback((targetId) => {
  dispatch({
    type: "UPDATE",
    targetId: targetId,
  });
}, []);

const onDelete = useCallback((targetId) => {
  dispatch({
    type: "DELETE",
    targetId: targetId,
  });
}, []);
```

### 최적화는 언제하면 좋을까?

- 기능 구현→ 최적화 진행

### 무엇을 대상으로 최적화를 해야할까?

- 모든 것에x, 꼭 필요할 것 같은 연산, 함수, 컴포넌트에만 적용하는 것이 좋음
  → 최적화하는 것 역시 연산이 필요하기 때문!
- 유저의 행동에 따라 개수가 늘어날 수 있는
- 함수를 많이 가지고 있어서 무거운

</br>

# section11. Context

- props를 대체하여 값을 전달할 수 있는 방식
- props의 단점을 보완
- props는 부모 → 자식으로만 데이터를 전달할 수 있음
  (컴포넌트의 계층 구조가 깊어지면 다이렉트로 전달하지 못하고, 중간 컴포넌트가 데이터를 이중으로 전달해야함)

context : 데이터 보관

```jsx
import { createContext } from "react"

const TodoContext = createContext();

function App{
return(
  <div className='App'>
    <Header/>
    <TodoContext.Provider value={{
      todos, onCreate, onDelete,
    }}>
      <Editor/>
      <List/>
    </TodoContext.Provider>

  </div>
  );
```

- App 컴포넌트가 리렌더링 될 때마다 새 context를 생성하게 되므로, App 컴포넌트 외부에 선언
- return문 안에서 props를 전달받는 컴포넌트들을 감싸도록 provider 컴포넌트 작성
- provider 내에 있는 컴포넌트들은 context 값을 공급받을 수 있게 됨
- provider 컴포넌트에 value라는 props로 전달해주면 됨

![Untitled](section11%20Context%200047892c781a4ec4bfd15b3e128e40f6/Untitled.png)

TodoContext.Provider가 리렌더링되면 자식컴포넌트인 Editor, List, TodoItem이 모두 리렌더링됨

❗TodoItem에는 props가 변하지 않으면 리렌더링 되지 않도록 memo를 사용했는데 리렌더링이 발생하는 이유?

```jsx
return (
  <div className="App">
    <Header />
    <TodoContext.Provider
      value={{
        todos,
        onCreate,
        onDelete, //이게 계속
      }}
    >
      <Editor />
      <List />
    </TodoContext.Provider>
  </div>
);
```

todo를 새로 만들거나 수정하거나 삭제하면 App 컴포넌트가 리렌더링됨

→ value props로 전달한 객체{todos, onCreate, onUpdate, onDelete}가 다시 생성됨

💡해결방법

TodoContext를 변경될 수 있는 값과 변경되지 않는 값으로 구분

![Untitled](section11%20Context%200047892c781a4ec4bfd15b3e128e40f6/Untitled%201.png)

# section12. 프로젝트3 : 감정일기장

# main.jsx

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";
import "./index.css";
import { BrowserRouter } from "react-router-dom";

ReactDOM.createRoot(document.getElementById("root")).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```

- App 컴포넌트를 BrowserRouter로 묶어줘야함!!

# App.jsx

```jsx
import "./App.css";
import { Routes, Route, Link, useNavigate } from "react-router-dom";
import Home from "./pages/Home";
import New from "./pages/New";
import Diary from "./pages/Diary";
import Notfound from "./pages/Notfound";

function App() {
  const nav = useNavigate();

  const onClickButton = () => {
    nav("/new");
  };

  return (
    <>
      <div>
        <Link to={"/"}>Home</Link>
        <Link to={"/new"}>New</Link>
        <Link to={"/diary"}>Diary</Link>
      </div>
      <button onClick={onClickButton}>New 페이지로 이동</button>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/new" element={<New />} />
        <Route path="/diary/:id" element={<Diary />} />
        <Route path="*" element={<Notfound />} />
      </Routes>
    </>
  );
}

export default App;
```

- useNavigate
  경로를 연결해줄 수 있음.
  onClickButton : nav함수를 이용하여 버튼이 클릭되면 현재 페이지의 주소를 변경
- Link to={””} : 링크
- Route path={””} : 라우팅
- path 경로를 “\*”로 하면 설정하지 않은 모든 경로에 대한 것을 설정할 수 있음 (Not found)

# Diary.jsx

```jsx
import { useParams } from "react-router-dom";

const Diary = () => {
  const params = useParams();
  console.log(params);

  return <div>{params}번 일기입니다</div>;
};

export default Diary;
```

-

# Home.jsx

```jsx
import { useSearchParams } from "react-router-dom";

const Home = () => {
  const [params, setParams] = useSearchParams();
  console.log(params.get("value"));

  return <div>Home</div>;
};

export default Home;
```

# New.jsx

```jsx
const New = () => {
  return <div>New</div>;
};

export default New;
```

### 질문
