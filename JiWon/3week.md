# 섹션 8. 프로젝트2. 투두리스트

8.1) 프로젝트 소개 및 준비

```jsx
import './App.css'

function App() {
  return <>TodoList</>
}

export default App
```

8.2) UI 구현하기

```jsx
import './App.css'
import Header from './components/Header'
import Editor from './components/Editor'
import List from './components/List'

function App() {
  return <div className='App'>
    <Header />
    <Editor />
    <List />
  </div>
}

export default App
```

```jsx
import "./Header.css"

const Header = () =>{
    return <div className="Header">
        <h3>오늘은 📆</h3>
        <h1>{new Date().toDateString()}</h1>
    </div>
}

export default Header
```

```jsx
.Header > h1{
    color: rgb(37, 147, 255);
}
```

```jsx
import "./Editor.css"

const Editor = () =>{
    return <div className="Editor">
        <input placeholder="새로운 Todo..." />
        <button>추가</button>
    </div>
}

export default Editor
```

```jsx
.Editor{
    display: flex;
    gap: 10px;
}

.Editor input {
    flex: 1;
    padding: 15px;
    border: 1px solid rgb(220, 220, 220);
    border-radius: 5px;
}

.Editor button {
    cursor: pointer;
    width: 80px;
    border: none;
    background-color: rgb(37, 147, 255);
    color: white;
    border-radius: 5px;
}
```

```jsx
import "./List.css"
import TodoItem from "./TodoItem"

const List = () =>{
    return <div className="List">
        <h4>Todo List 🌱</h4>
        <input placeholder="검색어를 입력하세요" />
        <div className="todos_wrapper">
            <TodoItem />
            <TodoItem />
            <TodoItem />
        </div>
    </div>
}

export default List
```

```jsx
.List {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.List > input {
    width: 100%;
    border: none;
    border-bottom: 1px solid rgb(220, 220, 220);
    padding: 15px 0px;
}

.List > input:focus {
    outline: none;
    border-bottom: 1px solid rgb(37, 147, 255);
}

.List .todos_wrapper {
    display: flex;
    flex-direction: column;
    gap: 20px;
}
```

```jsx
import './TodoItem.css'

const TodoItem = () => {
    return <div className="TodoItem">
        <input type="checkbox" />
        <div className="content">Todo...</div>
        <div className="date">Date</div>
        <button>삭제</button>
    </div>
}

export default TodoItem
```

```jsx
.TodoItem {
    display: flex;
    align-items: center;
    gap: 20px;
    padding-bottom: 20px;
    border-bottom: 1px solid rgb(240, 240, 240);
}

.TodoItem input{
    width: 20px;
}

.TodoItem .content{
    flex: 1;
}

.TodoItem .date {
    font-size: 14px;
    color: gray;
}

.TodoItem button {
    cursor: pointer;
    color: gray;
    font-size: 14px;
    border: none;
    border-radius: 5px;
    padding: 5px;
}
```

```jsx
.App {
  width: 500px;
  margin: 0 auto;
  
  display: flex;
  flex-direction: column;
  gap: 10px;
}
```

8.3) 기능 구현 준비하기

```jsx
import './App.css'
import { useState } from 'react'
import Header from './components/Header'
import Editor from './components/Editor'
import List from './components/List'

const mockData =[
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
]

function App() {
  const [todos, setTodos] = useState([mockData]);
  return <div className='App'>
    <Header />
    <Editor />
    <List />
  </div>
}

export default App
```

8.4) Create - 투두 추가하기

```jsx
import './App.css'
import { useState,useRef } from 'react'
import Header from './components/Header'
import Editor from './components/Editor'
import List from './components/List'

const mockData =[
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
]

function App() {
  const [todos, setTodos] = useState([mockData]);
  const idRef = useRef(3)

  const onCreate = (content) => {
    const newTodo = {
      id : idRef.current++,
      isDone: false,
      content: content,
      date: new Date().getTime()
    }

    setTodos([newTodo, ...todos])
  }
  return <div className='App'>
    <Header />
    <Editor onCreate={onCreate} />
    <List />
  </div>
}

export default App
```

```jsx
import "./Editor.css"
import { useState,useRef } from "react"

const Editor = ({onCreate}) => {
    const [content, setContent] = useState("");
    const contentRef = useRef();

    const onChangeContent = (e) => {
        setContent(e.target.value);
    }

    const onKeydown = (e) => {
        if(e.keyCode === 13){
            onsubmit();
        }
    }

    const onsubmit = () => {
        if (content === "") {
            contentRef.current.focus();
            return;
        }
        onCreate(content)
        setContent("")
    }

    return <div className="Editor">
        <input 
            ref={contentRef}
            value={content}
            onKeyDown={onkeydown}
            onChange={onChangeContent}
            placeholder="새로운 Todo..." 
        />
        <button onClick={onsubmit}>추가</button>
    </div>
}

export default Editor
```

8.5) Read - 투두리스트 렌더링하기

```jsx
import './App.css'
import { useState,useRef } from 'react'
import Header from './components/Header'
import Editor from './components/Editor'
import List from './components/List'

const mockData =[
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
]

function App() {
  const [todos, setTodos] = useState([mockData]);
  const idRef = useRef(3)

  const onCreate = (content) => {
    const newTodo = {
      id : idRef.current++,
      isDone: false,
      content: content,
      date: new Date().getTime()
    }

    setTodos([newTodo, ...todos])
  }
  return <div className='App'>
    <Header />
    <Editor onCreate={onCreate} />
    <List todos={todos} />
  </div>
}

export default App
```

```jsx
import "./List.css"
import TodoItem from "./TodoItem"
import { useState } from "react"

const List = ({todos}) =>{
    const [search, setSearch] = useState("")

    const onChangeSearch = (e) => {
        setSearch(e.target.value);
    }

    const getFilteredData = () => {
        if (search === ""){
            return todos;
        }
        return todos.filter((todo) =>
            todo.content.toLowerCase().includes(search.toLowerCase())
        )
    }

    const filteredTodos = getFilteredData();

    return(
        <div className="List">
        <h4>Todo List 🌱</h4>
        <input 
            value={search}
            onChange={onChangeSearch}
            placeholder="검색어를 입력하세요" 
        />
        <div className="todos_wrapper">
            {filteredTodos.map((todo)=>{
                return <TodoItem key={todo.id} {...todo} />;
            })}
        </div>
    </div>
    )
}

export default List
```

```jsx
import './TodoItem.css'

const TodoItem = ({id, isDone, content, date}) => {
    return <div className="TodoItem">
        <input checked={isDone} type="checkbox" />
        <div className="content">{content}</div>
        <div className="date">
            {new Date(date).toLocaleDateString()}
        </div>
        <button>삭제</button>
    </div>
}

export default TodoItem
```

8.6) Update - 투두 수정하기

```jsx
import './App.css'
import { useState,useRef } from 'react'
import Header from './components/Header'
import Editor from './components/Editor'
import List from './components/List'

const mockData =[
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
]

function App() {
  const [todos, setTodos] = useState([mockData]);
  const idRef = useRef(3)

  const onCreate = (content) => {
    const newTodo = {
      id : idRef.current++,
      isDone: false,
      content: content,
      date: new Date().getTime()
    }

    setTodos([newTodo, ...todos])
  }

  const onUpdate = (targetId)=>{
    setTodos(
      todos.map((todo)=>
        todo.id === targetId
          ? {...todo, isDone: !todo.isDone}
          : todo
      )
    )
  }

  return <div className='App'>
    <Header />
    <Editor onCreate={onCreate} />
    <List todos={todos} onUpdate={onUpdate} />
  </div>
}

export default App
```

```jsx
import "./List.css"
import TodoItem from "./TodoItem"
import { useState } from "react"

const List = ({todos, onUpdate}) =>{
    const [search, setSearch] = useState("")

    const onChangeSearch = (e) => {
        setSearch(e.target.value);
    }

    const getFilteredData = () => {
        if (search === ""){
            return todos;
        }
        return todos.filter((todo) =>
            todo.content.toLowerCase().includes(search.toLowerCase())
        )
    }

    const filteredTodos = getFilteredData();

    return(
        <div className="List">
        <h4>Todo List 🌱</h4>
        <input 
            value={search}
            onChange={onChangeSearch}
            placeholder="검색어를 입력하세요" 
        />
        <div className="todos_wrapper">
            {filteredTodos.map((todo)=>{
                return <TodoItem key={todo.id} {...todo} onUpdate={onUpdate} />;
            })}
        </div>
    </div>
    )
}

export default List
```

```jsx
import './TodoItem.css'

const TodoItem = ({id, isDone, content, date, onUpdate}) => {

    const onChangeCheckbox = () => {
        onUpdate(id);
    }
    return <div className="TodoItem">
        <input 
            onChange={onChangeCheckbox}
            readOnly
            checked={isDone} 
            type="checkbox"
        />
        <div className="content">{content}</div>
        <div className="date">
            {new Date(date).toLocaleDateString()}
        </div>
        <button>삭제</button>
    </div>
}

export default TodoItem
```

8.7) Delete- 투두 삭제하기

```jsx
import './App.css'
import { useState,useRef } from 'react'
import Header from './components/Header'
import Editor from './components/Editor'
import List from './components/List'

const mockData =[
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
]

function App() {
  const [todos, setTodos] = useState([mockData]);
  const idRef = useRef(3)

  const onCreate = (content) => {
    const newTodo = {
      id : idRef.current++,
      isDone: false,
      content: content,
      date: new Date().getTime()
    }

    setTodos([newTodo, ...todos])
  }

  const onUpdate = (targetId)=>{
    setTodos(
      todos.map((todo)=>
        todo.id === targetId
          ? {...todo, isDone: !todo.isDone}
          : todo
      )
    )
  }
  
  const onDelete = (targetId)=>{
    setTodos(todos.filter((todo)=>todo.id !== targetId))
  }

  return <div className='App'>
    <Header />
    <Editor onCreate={onCreate} />
    <List 
      todos={todos} 
      onUpdate={onUpdate} 
      onDelete = {onDelete}
    />
  </div>
}

export default App
```

```jsx
import "./List.css"
import TodoItem from "./TodoItem"
import { useState } from "react"

const List = ({todos, onUpdate, onDelete}) =>{
    const [search, setSearch] = useState("")

    const onChangeSearch = (e) => {
        setSearch(e.target.value);
    }

    const getFilteredData = () => {
        if (search === ""){
            return todos;
        }
        return todos.filter((todo) =>
            todo.content.toLowerCase().includes(search.toLowerCase())
        )
    }

    const filteredTodos = getFilteredData();

    return(
        <div className="List">
        <h4>Todo List 🌱</h4>
        <input 
            value={search}
            onChange={onChangeSearch}
            placeholder="검색어를 입력하세요" 
        />
        <div className="todos_wrapper">
            {filteredTodos.map((todo)=>{
                return (
                    <TodoItem 
                    key={todo.id} 
                    {...todo} 
                    onUpdate={onUpdate} 
                    onDelete={onDelete}
                    />
                )
            })}
        </div>
    </div>
    )
}

export default List
```

```jsx
import './TodoItem.css'

const TodoItem = ({id, isDone, content, date, onUpdate, onDelete}) => {

    const onChangeCheckbox = () => {
        onUpdate(id);
    }

    const onClickDeleteButton = () => {
        onDelete(id)
    }
    return <div className="TodoItem">
        <input 
            onChange={onChangeCheckbox}
            readOnly
            checked={isDone} 
            type="checkbox"
        />
        <div className="content">{content}</div>
        <div className="date">
            {new Date(date).toLocaleDateString()}
        </div>
        <button onClick={onClickDeleteButton}>삭제</button>
    </div>
}

export default TodoItem
```

# 섹션 9. useReducer

9.1) useReducer를 소개합니다

useReducer 

- 컴포넌트 내부에 새로운 State를 생성하는 React Hook
- 모든 useState는 useReducer로 대체 가능
- 상태 관리 코드를 컴포넌트 외부로 분리할 수 있음

```jsx
import './App.css'
import { useState,useRef } from 'react'
import Header from './components/Header'
import Editor from './components/Editor'
import List from './components/List'
import Exam from './components/Exam'

const mockData =[
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
]

function App() {
  const [todos, setTodos] = useState([mockData]);
  const idRef = useRef(3)

  const onCreate = (content) => {
    const newTodo = {
      id : idRef.current++,
      isDone: false,
      content: content,
      date: new Date().getTime(),
    }

    setTodos([newTodo, ...todos])
  }

  const onUpdate = (targetId)=>{
    setTodos(
      todos.map((todo)=>
        todo.id === targetId
          ? {...todo, isDone: !todo.isDone}
          : todo
      )
    )
  }
  
  const onDelete = (targetId)=>{
    setTodos(todos.filter((todo)=>todo.id !== targetId))
  }

  return <div className='App'>
    <Exam />
    {/* <Header />
    <Editor onCreate={onCreate} />
    <List 
      todos={todos} 
      onUpdate={onUpdate} 
      onDelete = {onDelete}
    /> */}
  </div>
}

export default App
```

```jsx
import { act, useReducer } from "react"

//reducer : 변환기
// -> 상태를 실제로 변화시키는 변환기 역할
function reducer(state, action) {
    switch(action.type){
        case 'INCREASE': return state+action.data;
        case 'DECREASE': return state - action.data;
        default: return state;
    }
}

const Exam = () => {
    //dispatch : 발송하다, 급송하다
    // -> 상태 변화가 있어야 한다는 사실을 알리는, 발송하는 함수
    const [state, dispatch] = useReducer(reducer, 0);

    const onClickplus = () => {
        //인수: 상태가 어떻게 변화되길 원하는지
        // -> 액션 객체
        dispatch({
            type: "INCREASE",
            data: 1,
        })
    }

    const onClickMinus = () => {
        dispatch({
            type: "DECREASE",
            data: 1,
        })
    }

    return <div>
        <h1>{state}</h1>
        <button onClick={onClickplus}>+</button>
        <button onClick={onClickMinus}>-</button>
    </div>
}

export default Exam
```

9.2) 투두리스트 업그레이드

```jsx
import './App.css'
import { useState,useRef,useReducer, act } from 'react'
import Header from './components/Header'
import Editor from './components/Editor'
import List from './components/List'

const mockData =[
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
]

function reducer(state, action){
  switch(action.type){
    case "CREATE":
      return [action.data, ...state];
    case "UPDATE":
      return state.map((item) => 
        item.id === action.targetId
          ? {...item, isDone : !item.isDone }
          : item
      )
    case 'DELETE':
      return state.filter((item)=>item.id !== action.targetId);
    default:
      return state;
  } 
}

function App() {
  const [todos, dispatch] = useReducer(reducer, mockData)
  const idRef = useRef(3)

  const onCreate = (content) => {
    dispatch({
      type: "CREATE",
      data: {
        id: idRef.current++,
        isDone: false,
        content: content,
        date: new Date().getTime(),
      }
    })
  }

  const onUpdate = (targetId)=>{
    dispatch({
      type: "UPDATE",
      targetId : targetId,
    })
  }
  
  const onDelete = (targetId)=>{
    dispatch({
      type:"DELETE",
      targetId: targetId,
    })
  }

  return <div className='App'>
    <Header />
    <Editor onCreate={onCreate} />
    <List 
      todos={todos} 
      onUpdate={onUpdate} 
      onDelete = {onDelete}
    />
  </div>
}

export default App
```

# 섹션 12. 프로젝트3. 감정 일기장

12.1) 프로젝트 소개 및 준비

12.2) 페이지 라우팅 1. 소개

페이지 라우팅 = 경로에 따라 알맞은 페이지를 렌더링 하는 과정 ex) /new → new 페이지 렌더링

페이지 라우팅의 원리

- Mulit Page Application (MPA) = 애초에 서버가 여러 개의 페이지를 가지고 있음

but, MPA는 페이지 이동이 쾌적하지 못함, 서버의 부하가 심해짐

- 서버 사이드 렌더링

React의 SPA(Single Page Application)

- 페이지 이동이 매끄럽고 효율적임
- 다수의 사용자가 접속해도 크게 상관 없음

React App 사용: 모든 페이지, 컴포넌트가 들어가 있음

12.3) 페이지 라우팅 2. 라우팅 설정하기

React Router = 대다수의 리액트 앱이 사용하고 있는 대표격 라이브러리

```jsx
import './App.css'
import { Routes, Route } from 'react-router-dom'
import Home from './pages/Home'
import Diary from './pages/Diary'
import New from './pages/New'
import Notfound from './pages/Notfound'

//1. "/" :  모든 일기를 조회하는 Home 페이지
//2. "/new": 새로운 일기를 작성하는 New 페이지
//3. "/diary" : 일기를 상세히 조회하는 Diary 페이지
function App() {
  return <Routes>
    <Route path='/' element={<Home />} />
    <Route path='/new' element={<New />} />
    <Route path='/diary' element={<Diary />} />
    <Route path='*' element={<Notfound />} />
  </Routes>
}

export default App
```

```jsx
const Home = () => {
    return <div>Home</div>;
}

export default Home;
```

```jsx
const Diary = () => {
    return <div>Diary</div>;
}

export default Diary;
```

```jsx
const New = () => {
    return <div>New</div>;
}

export default New;
```

```jsx
const Notfound = () => {
    return <div>잘못된 페이지입니다.</div>
}

export default Notfound
```

```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './index.css'
import { BrowserRouter } from 'react-router-dom'

ReactDOM.createRoot(document.getElementById('root')).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
)
```

12.4) 페이지 라우팅 3. 페이지 이동

```jsx
import './App.css'
import { Routes, Route, Link, useNavigate } from 'react-router-dom'
import Home from './pages/Home'
import Diary from './pages/Diary'
import New from './pages/New'
import Notfound from './pages/Notfound'

//1. "/" :  모든 일기를 조회하는 Home 페이지
//2. "/new": 새로운 일기를 작성하는 New 페이지
//3. "/diary" : 일기를 상세히 조회하는 Diary 페이지
function App() {
  const nav = useNavigate();

  const onClickBUtton = () => {
    nav("/new");
  }

  return (
    <>
      <div>
        <Link to={"/"}>Home</Link>
        <Link to={"/new"}>New</Link>
        <Link to={"/diary"}>Diary</Link>
      </div>
      <button onClick={onClickBUtton}>
        New 페이지로 이동
      </button>
      <Routes>
      <Route path='/' element={<Home />} />
      <Route path='/new' element={<New />} />
      <Route path='/diary' element={<Diary />} />
      <Route path='*' element={<Notfound />} />
    </Routes>
    </>
  )
}

export default App
```

12.5) 페이지 라우팅 4. 동적 경로

동적 경로(Dynamic Segments) = 동적인 데이터를 포함하고 있는 경로

URL Parameter(/ 뒤에 아이템의 id를 명시) = 아이템의 id 등의 변경되지 않는 값을 주소로 명시하기 위해 사용됨

Query String(? 뒤에 변수명과 값 명시) = 검색어 등의 자주 변경되는 값을 주소로 명시하기 위해 사용

```jsx
import './App.css'
import { Routes, Route, Link, useNavigate } from 'react-router-dom'
import Home from './pages/Home'
import Diary from './pages/Diary'
import New from './pages/New'
import Notfound from './pages/Notfound'

//1. "/" :  모든 일기를 조회하는 Home 페이지
//2. "/new": 새로운 일기를 작성하는 New 페이지
//3. "/diary" : 일기를 상세히 조회하는 Diary 페이지
function App() {
  const nav = useNavigate();

  const onClickBUtton = () => {
    nav("/new");
  }

  return (
    <>
      <div>
        <Link to={"/"}>Home</Link>
        <Link to={"/new"}>New</Link>
        <Link to={"/diary"}>Diary</Link>
      </div>
      <button onClick={onClickBUtton}>
        New 페이지로 이동
      </button>
      <Routes>
      <Route path='/' element={<Home />} />
      <Route path='/new' element={<New />} />
      <Route path='/diary:id' element={<Diary />} />
      <Route path='*' element={<Notfound />} />
    </Routes>
    </>
  )
}

export default App
```

```jsx
import { useParams } from "react-router-dom";

const Diary = () => {
    const params = useParams();
    console.log(params);

    return <div>{params.id}번 일기입니다.</div>;
}

export default Diary;
```

```jsx
import { useSearchParams } from "react-router-dom";

const Home = () => {
    const [params, setParams] = useSearchParams();
    console.log(params.get("value"))
    
    return <div>Home</div>;
}

export default Home;
```

# 섹션 10. 최적화

10.1) 최적화란

최적화(Optimization) = 웹 서비스의 성능을 개선하는 모든 행위를 일컫음, 아주 단순한 것부터 아주 어려운 방법까지 매우 다양함

일반적인 웹 서비스 최적화 방법

- 서버의 응답속도 개선
- 이미지, 폰트, 코드 파일 등의 정적 파일 로딩 개선
- 불필요한 네트워크 요청 줄임

React App 내부의 최적화 방법

- 컴포넌트 내부의 불필요한 연산 방지
- 컴포넌트 내부의 불필요한 함수 재생성 방지
- 컴포넌트의 불필요한 리렌더링 방지

10.2) useMemo와 연산 최적화

useMemo = “메모이제이션” 기법을 기반으로 불필요한 연산을 최적화 하는 리액트 훅

메모이제이션(Memoization): 기억해두기, 메모해두기 라는 뜻

```jsx
import "./List.css"
import TodoItem from "./TodoItem"
import { useState, useMemo } from "react"

const List = ({todos, onUpdate, onDelete}) =>{
    const [search, setSearch] = useState("")

    const onChangeSearch = (e) => {
        setSearch(e.target.value);
    }

    const getFilteredData = () => {
        if (search === ""){
            return todos;
        }
        return todos.filter((todo) =>
            todo.content.toLowerCase().includes(search.toLowerCase())
        )
    }

    const filteredTodos = getFilteredData();

    const {totalCount, doneCount, notDoneCount} = useMemo( ()=>{
        console.log("getAnalyzedData 호출!");
        const totalCount = todos.length;
        const doneCount = todos.filter(
            (todo) => todo.isDone
        ).length;
        const notDoneCount = totalCount - doneCount;

        return {
            totalCount,
            doneCount,
            notDoneCount
        }
    }, [todos])
    //의존성배열 : deps

    return(
        <div className="List">
            <h4>Todo List 🌱</h4>
        <div>
            <div>total: {totalCount}</div>
            <div>done: {doneCount}</div>
            <div>notDone: {notDoneCount}</div>
        </div>
            <input 
                value={search}
                onChange={onChangeSearch}
                placeholder="검색어를 입력하세요" 
            />
            <div className="todos_wrapper">
                {filteredTodos.map((todo)=>{
                    return (
                        <TodoItem 
                        key={todo.id} 
                        {...todo} 
                        onUpdate={onUpdate} 
                        onDelete={onDelete}
                        />
                    )
                })}
            </div>
    </div>
    )
}

export default List
```

10.3) React.memo와 컴포넌트 렌더링 최적화

Reacto.memo = 컴포넌트를 인수로 받아, 최적화된 컴포넌트로 만들어 반환

```jsx
const MemoizedComponent = memo(Componet)
```

```jsx
import './TodoItem.css'
import { memo } from 'react';

const TodoItem = ({id, isDone, content, date, onUpdate, onDelete}) => {

    const onChangeCheckbox = () => {
        onUpdate(id);
    }

    const onClickDeleteButton = () => {
        onDelete(id)
    }
    return <div className="TodoItem">
        <input 
            onChange={onChangeCheckbox}
            readOnly
            checked={isDone} 
            type="checkbox"
        />
        <div className="content">{content}</div>
        <div className="date">
            {new Date(date).toLocaleDateString()}
        </div>
        <button onClick={onClickDeleteButton}>삭제</button>
    </div>
}

//고차 컴포넌트 (HOC)
export default memo(TodoItem, (prevProps, nextProps) => {
    //반환값에 따라, Props가 바뀌었는지 안바뀌었는지 판단
    // T -> Props 바뀌지 않음 -> 리렌더링 X
    // F -> Props 바뀜 -> 리렌더링 O

    if (prevProps.id !== nextProps.id) return false;
    if (prevProps.isDone !== nextProps.isDone) return false;
    if (prevProps.content !== nextProps.content) return false;
    if (prevProps.date !== nextProps.date) return false;

    return true;
})
```

```jsx
import "./Header.css"
import { memo } from "react"

const Header = () =>{
    return <div className="Header">
        <h3>오늘은 📆</h3>
        <h1>{new Date().toDateString()}</h1>
    </div>
}

export default memo(Header)
```

10.4) useCallback과 함수 재생성 방지

```jsx
import './TodoItem.css'
import { memo } from 'react';

const TodoItem = ({id, isDone, content, date, onUpdate, onDelete}) => {

    const onChangeCheckbox = () => {
        onUpdate(id);
    }

    const onClickDeleteButton = () => {
        onDelete(id)
    }
    return <div className="TodoItem">
        <input 
            onChange={onChangeCheckbox}
            readOnly
            checked={isDone} 
            type="checkbox"
        />
        <div className="content">{content}</div>
        <div className="date">
            {new Date(date).toLocaleDateString()}
        </div>
        <button onClick={onClickDeleteButton}>삭제</button>
    </div>
}

// //고차 컴포넌트 (HOC)
// export default memo(TodoItem, (prevProps, nextProps) => {
//     //반환값에 따라, Props가 바뀌었는지 안바뀌었는지 판단
//     // T -> Props 바뀌지 않음 -> 리렌더링 X
//     // F -> Props 바뀜 -> 리렌더링 O

//     if (prevProps.id !== nextProps.id) return false;
//     if (prevProps.isDone !== nextProps.isDone) return false;
//     if (prevProps.content !== nextProps.content) return false;
//     if (prevProps.date !== nextProps.date) return false;

//     return true;
// })

export default memo(TodoItem)
```

```jsx
import './App.css'
import { useState,useRef,useReducer, useCallback } from 'react'
import Header from './components/Header'
import Editor from './components/Editor'
import List from './components/List'

const mockData =[
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
]

function reducer(state, action){
  switch(action.type){
    case "CREATE":
      return [action.data, ...state];
    case "UPDATE":
      return state.map((item) => 
        item.id === action.targetId
          ? {...item, isDone : !item.isDone }
          : item
      )
    case 'DELETE':
      return state.filter((item)=>item.id !== action.targetId);
    default:
      return state;
  } 
}

function App() {
  const [todos, dispatch] = useReducer(reducer, mockData)
  const idRef = useRef(3)

  const onCreate = useCallback((content) => {
    dispatch({
      type: "CREATE",
      data: {
        id: idRef.current++,
        isDone: false,
        content: content,
        date: new Date().getTime(),
      }
    })
  }, [])

  const onUpdate = useCallback((targetId)=>{
    dispatch({
      type: "UPDATE",
      targetId : targetId,
    })
  }, [])

  const onDelete = useCallback((targetId)=>{
    dispatch({
      type:"DELETE",
      targetId: targetId,
    })
  }, [])

  return <div className='App'>
    <Header />
    <Editor onCreate={onCreate} />
    <List 
      todos={todos} 
      onUpdate={onUpdate} 
      onDelete = {onDelete}
    />
  </div>
}

export default App
```

# 섹션 11. Context

11.1) Context란

React Context = 컴포넌트간의 데이터를 전달하는 또 다른 방법, 기존의 Props가 가지고 있던 단점을 해결할 수 있음

Props의 단점: Props Drilling

- Props는 부모→자식 으로만 데이터를 전달할 수 있었음

context = 데이터 보관소 (객체)

11.2) Context 사용하기

```jsx
import './App.css'
import { useState,useRef,useReducer, useCallback,createContext } from 'react'
import Header from './components/Header'
import Editor from './components/Editor'
import List from './components/List'

const mockData =[
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
]

function reducer(state, action){
  switch(action.type){
    case "CREATE":
      return [action.data, ...state];
    case "UPDATE":
      return state.map((item) => 
        item.id === action.targetId
          ? {...item, isDone : !item.isDone }
          : item
      )
    case 'DELETE':
      return state.filter((item)=>item.id !== action.targetId);
    default:
      return state;
  } 
}

export const TodoContext = createContext();

function App() {
  const [todos, dispatch] = useReducer(reducer, mockData)
  const idRef = useRef(3)

  const onCreate = useCallback((content) => {
    dispatch({
      type: "CREATE",
      data: {
        id: idRef.current++,
        isDone: false,
        content: content,
        date: new Date().getTime(),
      }
    })
  }, [])

  const onUpdate = useCallback((targetId)=>{
    dispatch({
      type: "UPDATE",
      targetId : targetId,
    })
  }, [])

  const onDelete = useCallback((targetId)=>{
    dispatch({
      type:"DELETE",
      targetId: targetId,
    })
  }, [])

  return <div className='App'>
    <Header />
    <TodoContext.Provider value={{
      todos, onCreate, onUpdate, onDelete,
    }}>
      <Editor />
      <List />
    </TodoContext.Provider>
  </div>
}

export default App
```

```jsx
import "./Editor.css"
import { useState,useRef,useContext } from "react"
import { TodoContext } from "../App"

const Editor = () => {
    const { onCreate } = useContext(TodoContext)
    const [content, setContent] = useState("");
    const contentRef = useRef();

    const onChangeContent = (e) => {
        setContent(e.target.value);
    }

    const onKeydown = (e) => {
        if(e.keyCode === 13){
            onsubmit();
        }
    }

    const onsubmit = () => {
        if (content === "") {
            contentRef.current.focus();
            return;
        }
        onCreate(content)
        setContent("")
    }

    return <div className="Editor">
        <input 
            ref={contentRef}
            value={content}
            onKeyDown={onkeydown}
            onChange={onChangeContent}
            placeholder="새로운 Todo..." 
        />
        <button onClick={onsubmit}>추가</button>
    </div>
}

export default Editor
```

```jsx
import "./List.css"
import TodoItem from "./TodoItem"
import { useState, useMemo, useContext } from "react"
import { TodoContext } from "../App"

const List = () =>{
    const {todos} = useContext(TodoContext)
    const [search, setSearch] = useState("")

    const onChangeSearch = (e) => {
        setSearch(e.target.value);
    }

    const getFilteredData = () => {
        if (search === ""){
            return todos;
        }
        return todos.filter((todo) =>
            todo.content.toLowerCase().includes(search.toLowerCase())
        )
    }

    const filteredTodos = getFilteredData();

    const {totalCount, doneCount, notDoneCount} = useMemo( ()=>{
        console.log("getAnalyzedData 호출!");
        const totalCount = todos.length;
        const doneCount = todos.filter(
            (todo) => todo.isDone
        ).length;
        const notDoneCount = totalCount - doneCount;

        return {
            totalCount,
            doneCount,
            notDoneCount
        }
    }, [todos])
    //의존성배열 : deps

    return(
        <div className="List">
            <h4>Todo List 🌱</h4>
        <div>
            <div>total: {totalCount}</div>
            <div>done: {doneCount}</div>
            <div>notDone: {notDoneCount}</div>
        </div>
            <input 
                value={search}
                onChange={onChangeSearch}
                placeholder="검색어를 입력하세요" 
            />
            <div className="todos_wrapper">
                {filteredTodos.map((todo)=>{
                    return (
                        <TodoItem 
                        key={todo.id} 
                        {...todo} 
                        />
                    )
                })}
            </div>
    </div>
    )
}

export default List
```

```jsx
import './TodoItem.css'
import { memo,useContext } from 'react';
import { TodoContext } from '../App';

const TodoItem = ({id, isDone, content, date}) => {
    const {onUpdate, onDelete} = useContext(TodoContext)

    const onChangeCheckbox = () => {
        onUpdate(id);
    }

    const onClickDeleteButton = () => {
        onDelete(id)
    }
    return <div className="TodoItem">
        <input 
            onChange={onChangeCheckbox}
            readOnly
            checked={isDone} 
            type="checkbox"
        />
        <div className="content">{content}</div>
        <div className="date">
            {new Date(date).toLocaleDateString()}
        </div>
        <button onClick={onClickDeleteButton}>삭제</button>
    </div>
}

// //고차 컴포넌트 (HOC)
// export default memo(TodoItem, (prevProps, nextProps) => {
//     //반환값에 따라, Props가 바뀌었는지 안바뀌었는지 판단
//     // T -> Props 바뀌지 않음 -> 리렌더링 X
//     // F -> Props 바뀜 -> 리렌더링 O

//     if (prevProps.id !== nextProps.id) return false;
//     if (prevProps.isDone !== nextProps.isDone) return false;
//     if (prevProps.content !== nextProps.content) return false;
//     if (prevProps.date !== nextProps.date) return false;

//     return true;
// })

export default memo(TodoItem)
```

11.3) Context 분리하기

Todocontext 

1. TodoStateContext(변경될 수 있는 값)
2. TodoDispatchContext(변경되지 않는 값)

```jsx
import './App.css'
import { useState,useRef,useReducer, useCallback,createContext,useMemo } from 'react'
import Header from './components/Header'
import Editor from './components/Editor'
import List from './components/List'

const mockData =[
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
]

function reducer(state, action){
  switch(action.type){
    case "CREATE":
      return [action.data, ...state];
    case "UPDATE":
      return state.map((item) => 
        item.id === action.targetId
          ? {...item, isDone : !item.isDone }
          : item
      )
    case 'DELETE':
      return state.filter((item)=>item.id !== action.targetId);
    default:
      return state;
  } 
}

export const TodoStateContext = createContext()
export const TodoDispatchContext = createContext()

function App() {
  const [todos, dispatch] = useReducer(reducer, mockData)
  const idRef = useRef(3)

  const onCreate = useCallback((content) => {
    dispatch({
      type: "CREATE",
      data: {
        id: idRef.current++,
        isDone: false,
        content: content,
        date: new Date().getTime(),
      }
    })
  }, [])

  const onUpdate = useCallback((targetId)=>{
    dispatch({
      type: "UPDATE",
      targetId : targetId,
    })
  }, [])

  const onDelete = useCallback((targetId)=>{
    dispatch({
      type:"DELETE",
      targetId: targetId,
    })
  }, [])

  const memoizedDispatch = useMemo(()=>{
    return { onCreate, onUpdate, onDelete }
  }, [])

  return <div className='App'>
    <Header />
    <TodoStateContext.Provider value={todos}>
      <TodoDispatchContext.Provider value={memoizedDispatch}>
        <Editor />
        <List />
      </TodoDispatchContext.Provider>
    </TodoStateContext.Provider>
  </div>
}

export default App
```

```jsx
import "./Editor.css"
import { useState,useRef,useContext } from "react"
import { TodoDispatchContext } from "../App"

const Editor = () => {
    const { onCreate } = useContext(TodoDispatchContext)
    const [content, setContent] = useState("");
    const contentRef = useRef();

    const onChangeContent = (e) => {
        setContent(e.target.value);
    }

    const onKeydown = (e) => {
        if(e.keyCode === 13){
            onsubmit();
        }
    }

    const onsubmit = () => {
        if (content === "") {
            contentRef.current.focus();
            return;
        }
        onCreate(content)
        setContent("")
    }

    return <div className="Editor">
        <input 
            ref={contentRef}
            value={content}
            onKeyDown={onkeydown}
            onChange={onChangeContent}
            placeholder="새로운 Todo..." 
        />
        <button onClick={onsubmit}>추가</button>
    </div>
}

export default Editor
```

```jsx
import "./List.css"
import TodoItem from "./TodoItem"
import { useState, useMemo, useContext } from "react"
import { TodoStateContext } from "../App"

const List = () =>{
    const todos = useContext(TodoStateContext)
    const [search, setSearch] = useState("")

    const onChangeSearch = (e) => {
        setSearch(e.target.value);
    }

    const getFilteredData = () => {
        if (search === ""){
            return todos;
        }
        return todos.filter((todo) =>
            todo.content.toLowerCase().includes(search.toLowerCase())
        )
    }

    const filteredTodos = getFilteredData();

    const {totalCount, doneCount, notDoneCount} = useMemo( ()=>{
        console.log("getAnalyzedData 호출!");
        const totalCount = todos.length;
        const doneCount = todos.filter(
            (todo) => todo.isDone
        ).length;
        const notDoneCount = totalCount - doneCount;

        return {
            totalCount,
            doneCount,
            notDoneCount
        }
    }, [todos])
    //의존성배열 : deps

    return(
        <div className="List">
            <h4>Todo List 🌱</h4>
        <div>
            <div>total: {totalCount}</div>
            <div>done: {doneCount}</div>
            <div>notDone: {notDoneCount}</div>
        </div>
            <input 
                value={search}
                onChange={onChangeSearch}
                placeholder="검색어를 입력하세요" 
            />
            <div className="todos_wrapper">
                {filteredTodos.map((todo)=>{
                    return (
                        <TodoItem 
                        key={todo.id} 
                        {...todo} 
                        />
                    )
                })}
            </div>
    </div>
    )
}

export default List
```

```jsx
import './TodoItem.css'
import { memo,useContext } from 'react';
import { TodoDispatchContext } from '../App';

const TodoItem = ({id, isDone, content, date}) => {
    const {onUpdate, onDelete} = useContext(TodoDispatchContext)

    const onChangeCheckbox = () => {
        onUpdate(id);
    }

    const onClickDeleteButton = () => {
        onDelete(id)
    }
    return <div className="TodoItem">
        <input 
            onChange={onChangeCheckbox}
            readOnly
            checked={isDone} 
            type="checkbox"
        />
        <div className="content">{content}</div>
        <div className="date">
            {new Date(date).toLocaleDateString()}
        </div>
        <button onClick={onClickDeleteButton}>삭제</button>
    </div>
}

// //고차 컴포넌트 (HOC)
// export default memo(TodoItem, (prevProps, nextProps) => {
//     //반환값에 따라, Props가 바뀌었는지 안바뀌었는지 판단
//     // T -> Props 바뀌지 않음 -> 리렌더링 X
//     // F -> Props 바뀜 -> 리렌더링 O

//     if (prevProps.id !== nextProps.id) return false;
//     if (prevProps.isDone !== nextProps.isDone) return false;
//     if (prevProps.content !== nextProps.content) return false;
//     if (prevProps.date !== nextProps.date) return false;

//     return true;
// })

export default memo(TodoItem)
```