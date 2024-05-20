# 3주차

**강의**
[인프런] - 한입 크기로 잘라머는 리액트(React.js) : 기초부터 실전까지
(https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8)

### 범위

섹션 8 ~ 섹션 12.5

- [x] 8.  프로젝트2. 투두리스트
- [x] 9.  useReducer
- [x] 10.  최적화
- [x] 11.  Context
- [ ] 12.  프로젝트3. 감정 일기장 5강

---

</br>

### 학습 내용

# Ch.08 프로젝트2.투두리스트

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/22ed8513-5274-4c89-a760-32fdeead3885/Untitled.png)

### Todo 검색

List.jsx

```jsx
import './List.css'
import TodoItem from './TodoItem';
import { useState } from 'react';

const List = ({todos,onUpdate,onDelete}) =>{

    const [search,setSearch]= useState("");
    const onChangeSearch = (e) =>{
        setSearch(e.target.value);
    };

    const getFilteredData=()=>{
        if(search === ""){
            return todos;
        }
        //search 값이 존재하는 todo만 필터링
        //toLowerCase() 적용해서 대소문자 구분 없이 검색 되도록 함
        return todos.filter((todo)=>
            todo.content.toLowerCase().includes(search.toLowerCase()));
    }
    const filteredTodos = getFilteredData();
    return (
        <div className='List'>
            <h4>Todo List🌱</h4>
            <input
            value={search} 
            onChange={onChangeSearch} 
            placeholder='검색어를 입력하새요'/>
            <div className='todos_wrapper'>
                {filteredTodos.map((todo)=>{
                    return <TodoItem key={todo.id}{...todo} onDelete={onDelete} onUpdate={onUpdate}/>;
                })}
            </div>
        </div>
    )
}

export default List;
```

### Todo List 추가

Editor.jsx

```jsx
import './Editor.css'
import { useState,useRef } from 'react'

const Editor = ({onCreate}) =>{
    const [content,setContent] = useState("");
    const contentRef = useRef();
    const onChangeComponent = (e) =>{
        setContent(e.target.value);
    };

    const onSubmit = () =>{
        if(content===""){
            contentRef.current.focus();
            return;
        }
        onCreate(content);
        //todo 입력후 input 폼 초기화
        setContent("");
    };

    const onKeydownn = (e) =>{
        if(e.keyCode===13){
            onSubmit();
        }
    }

    return (
        <div className="Editor">
            <input
                ref={contentRef}
                value={content} 
                onKeyDown={onKeydownn}
                onChange={onChangeComponent}
                placeholder="새로운 Todo..."
            />
            <button onClick={onSubmit}>추가</button>
        </div>
    )
}

export default Editor;
```

### Todo 체크박스

App.jsx

```jsx
  const onUpdate = (targetId) => {
    // todos State의 값들 중에
    // targetId와 일치하는 id를 갖는 투두 아이템의 isDone 변경

    // 인수: todos 배열에서 targetId와 일치하는 id를 갖는 요소의 데이터만 딱 바꾼 새로운 배열
    setTodos(
      todos.map((todo) =>
        todo.id === targetId
          ? { ...todo, isDone: !todo.isDone }
          : todo
      )
    );
  };
```

TodoItem.jsx

```jsx
  const onChangeCheckbox = () => {
    onUpdate(id);
  };
```

```jsx
<input
        onChange={onChangeCheckbox}
        readOnly
        checked={isDone}
        type="checkbox"
      />
```

### Todo 삭제

App.jsx

```jsx
  const onDelete = (targetId) =>{
    // 인수 : todos 배열에서 targetId와 일치하는 id를 갖는 요소만 삭제한 새로운 배열
    setTodos(todos.filter((todo)=>todo.id!==targetId));
  }
```

TodoItem.jsx
```jsx
  const onChangeCheckbox = () => {
    onUpdate(id);
  };
```

```jsx
 <button onClick={onClickDeleteButton}>삭제</button>
```

# Ch.09 useReducer

### useReducer

useReducer

: 컴포넌트 내부에 새로운 State를 생성하는 React Hook

모든 useState는 useReducer로 대체 가능

**상태 관리 코드를 컴포넌트 외부로 분리할 수 있음**

**useState**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/d8a3be99-74ca-4195-8259-2f30d45ee5a4/Untitled.png)

**useReducer**

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/85d1546d-ecf1-4ce4-80a7-10f278668f60/Untitled.png)

```jsx
import { useReducer } from "react";

// reducer : 변환기
// -> 상태를 실제로 변화시키는 변환기 역할
function reducer(state, action) {
  switch (action.type) {
    case "INCREASE":
      return state + action.data;
    case "DECREASE":
      return state - action.data;
    default:
      return state;
  }
}

const Exam = () => {
  // dispatch : 발송하다, 급송하다
  // -> 상태 변화가 있어야 한다는 사실을 알리는, 발송하는 함수
  const [state, dispatch] = useReducer(reducer, 0);

  const onClickPlus = () => {
    // 인수: 상태가 어떻게 변화되길 원하는지
    // -> 액션 객체
    dispatch({
      type: "INCREASE",
      data: 1,
    });
  };

  const onClickMinus = () => {
    dispatch({
      type: "DECREASE",
      data: 1,
    });
  };

  return (
    <div>
      <h1>{state}</h1>
      <button onClick={onClickPlus}>+</button>
      <button onClick={onClickMinus}>-</button>
    </div>
  );
};

export default Exam;
```

### useReducer로 TodoList 업그레이드
```jsx
import "./App.css";
import { useRef, useState, useReducer } from "react";
import Header from "./components/Header";
import Editor from "./components/Editor";
import List from "./components/List";

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

function reducer(state,action){
  switch(action.type){
    case 'CREATE': return [action.data, ...state];
    case 'UPDATE' : return state.map((item) =>
      item.id === action.targetId
        ? { ...item, isDone: !item.isDone }
        : item
    )
    case 'DELETE':
      return state.filter((item)=>item.id !==action.targetId);
    default:
      return state;
  }

}

function App() {
  const [todos, dispatch] = useReducer(reducer, mockData);
  const idRef = useRef(3);

  const onCreate = (content) => {
    dispatch({
      type:"CREATE",
      data:{
        id: idRef.current++,
        isDone: false,
        content: content,
        date: new Date().getTime(),
      },
    });
  };

  const onUpdate = (targetId) => {
    // todos State의 값들 중에
    // targetId와 일치하는 id를 갖는 투두 아이템의 isDone 변경

    // 인수: todos 배열에서 targetId와 일치하는 id를 갖는 요소의 데이터만 딱 바꾼 새로운 배열
    dispatch({
      type:"UPDATE",
      targetId:targetId
    })
  };

  const onDelete = (targetId) =>{
    // 인수 : todos 배열에서 targetId와 일치하는 id를 갖는 요소만 삭제한 새로운 배열
    dispatch({
      type:"DELETE",
      targetId:targetId
    })
  }

  return (
    <div className="App">
   
      <Header />
      <Editor onCreate={onCreate} />
      <List todos={todos} onDelete={onDelete}onUpdate={onUpdate} />
   
    </div>
  );
}

export default App;
```


# Ch.10 최적화

### 최적화

최적화(Optimization)

: 웹 서비스의 성능을 개선하는 모든 행위를 일컫음

아주 단순한 것부터 아주 어려운 방법까지 매우 다양함

### useMemo

useMemo

: 메모제이션 기법을 기반으로 불필요한 연산을 최적화 하는 리액트 훅

```jsx
    const { totalCount, doneCount, notDoneCount } =
    useMemo(() => {
      console.log("getAnalyzedData 호출!");
      const totalCount = todos.length;
      const doneCount = todos.filter(
        (todo) => todo.isDone
      ).length;
      const notDoneCount = totalCount - doneCount;

      return {
        totalCount,
        doneCount,
        notDoneCount,
      };
    }, [todos]); //todos의 값이 변경되면 콜백함수를 다시 실행함
  // 의존성배열 : deps
```

```jsx
            <div>
                <div>total: {totalCount}</div>
                <div>done: {doneCount}</div>
                <div>notDone: {notDoneCount}</div>
            </div>
```

### React.memo

React.memo

: 컴포넌트를 인수로 받아, 최적화된 컴포넌트로 만들어 반환

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/96f2de7b-3c46-4c16-9735-d1e42fe5ef38/Untitled.png)

**props에 객체가 없을 때**

```jsx
export default memo(Header);
```

**props에 객체가 있을 때**

```jsx
// 고차 컴포넌트 (HOC)
export default memo(TodoItem, (prevProps, nextProps) => {
  // 반환값에 따라, Props가 바뀌었는지 안바뀌었지 판단
  // T -> Props 바뀌지 않음 -> 리렌더링 X
  // F -> Props 바뀜 -> 리렌더링 O

  if (prevProps.id !== nextProps.id) return false;
  if (prevProps.isDone !== nextProps.isDone) return false;
  if (prevProps.content !== nextProps.content) return false;
  if (prevProps.date !== nextProps.date) return false;

  return true;
});
```

### useCallback

useCallback

:  UseCallback 메모이제이션된 콜백 함수, 즉 이미 생성된 함수를 반환하는 리액트 훅

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

최적화는 가장 마지막에 하는 것이 좋다!

https://goongoguma.github.io/2021/04/26/When-to-useMemo-and-useCallback/


# Ch.11 Context

### Context

React Context

: 컴포넌트간의 데이터를 전달하는 또 다른 방법

기존의 Props가 가지고 있던 단점을 해결할 수 있음

→ props driling을 해결

**Props의 단점이란?**

- Props Driling
    
    : Props는 부모 → 자식으로만 데이터를 전달할 수 있었음
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/4057dbe4-9f87-43ce-99ad-bd7adb9fbd54/Untitled.png)
    

**App.jsx**

```jsx
//Component 외부에 생성 
export const TodoContext = createContext();
```

```jsx
  return (
    <div className="App">
   
      <Header />
      <TodoContext.Provider value={{        
        todos,
        onCreate,
        onUpdate,
        onDelete}
      }>
        <Editor/>
        <List/>
      </TodoContext.Provider>
    </div>
  );

```

**List.jsx**

```jsx
const {todos} = useContext(TodoContext);
```

→ but,, 이렇게 하면 이전 챕터에서 적용한 최적화 실행X

원인 : 객체가 다시 생성되어 계속 리렌더링 됨 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/5a234aeb-8a3b-4bf2-97ba-ee9e15ea1689/Untitled.png)

해결 : context를 2개로 분리

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/c33618a0-98a4-4ddf-831d-6d68e50d0b3d/Untitled.png)

```jsx
//Component 외부에 생성 
export const TodoStateContext = createContext();
export const TodoDispatchContext = createContext();
```

```jsx
      <Header />
      <TodoStateContext.Provider value={todos}>
        <TodoDispatchContext.Provider value={memoizedDispatch}>
          <Editor />
          <List />
        </TodoDispatchContext.Provider>
      </TodoStateContext.Provider>
```

**List.jsx**

todos는 객체가 아니라 배열로 전달되기 때문에 받아서 사용할 때도 배열을 써야함. 

```jsx
  const todos = useContext(TodoStateContext);
```