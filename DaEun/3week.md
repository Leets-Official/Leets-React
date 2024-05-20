# 3주차 스터디

# 08. 투두리스트 프로젝트

## UI 구현하기

**Header 컴퍼넌트 구현**

- App.css

```css
.App {
    display: flex; /*자식 요소를 유연하게 (한줄로)*/
    flex-direction: column; /*열로 배치*/
    gap: 10px; /*간격*/
}
```

![Untitled](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled.png)

```css
width: 500px; /*요소를 화면 가운데에 배치*/
margin: 0 auto;
```

- Header.jsx

```jsx
import "./Header.css";

const Header = ()=>{
    return <div className="Header"> {/*Header의 css를 만들기 위해 이름 붙임*/}
        <h3>오늘은 👻</h3>
        <h1>{new Date().toDateString()}</h1> {/*현재 날짜*/}
    </div>;
};

export default Header;
```

→ components 폴더 안에 Header.css 파일 추가

- Header.css

```css
.Header >h1 {
    color: rgb(37, 147, 255); /*날짜를 하늘색으로*/
}
```

![Untitled](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%201.png)

**Editor 컴퍼넌트 구현**

- Editor.jsx

```jsx
import "./Editor.css"

const Editor = ()=>{
    return (
    <div className="Editor">
        <input placeholder="새로운 Todo..."/>
        <button>추가</button>
    </div>
    );
};

export default Editor;
```

![Untitled](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%202.png)

→ components 폴더 안에 Editor.css 파일 추가

- Editor.css

```css
.Editor {
    display: flex;
    gap: 10px; /*인풋과 버튼 사이의 간격*/
}

.Editor input { 
    flex: 1; /*인풋 박스 최대한 길게*/
    padding: 15px;
    border: 1px solid rgb(220, 220, 220); /*테두리*/
    border-radius: 5px; /*모서리를 5만큼 둥글게*/
}

.Editor button { /*버튼 꾸미기*/
    cursor: pointer; /*버튼에 마우스 올리면 커서가 손가락 모양*/
    width: 80px;
    border: none;
    background-color: rgb(37, 147, 255);
    color: white;
    border-radius: 5px;
}
```

![Untitled](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%203.png)

**List 컴퍼넌트 구현**

- List.jsx

```jsx
import "./List.css";

const List = ()=>{
    return (
        <div className="List">
            <h4>Todo List 🦕</h4>
            <input placeholder="검색어를 입력하세요" />
        </div>
    );
};

export default List;
```

![Untitled](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%204.png)

- List.css

```css
.List > input {
    width: 100%;
    border: none;
    border-bottom: 1px solid rgb(220, 220, 220);
    padding: 15px 0px;
}

.List > input:focus { /*검색창을 클릭했을 때*/
    outline: none;
    border-bottom: 1px solid rgb(37, 147, 255);
}
```

![Untitled](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%205.png)

→  components 폴더 안에 TodoItem.jsx 파일 추가

- TodoItem.jsx

```jsx
const TodoItem = () => {
    return (
        <div>
            TodoItem
        </div>
    );
};

export default TodoItem;
```

→ 그리고 List.jsx에 불러오기

```jsx
import "./List.css";
import TodoItem from "./TodoItem";

const List = ()=>{
    return (
        <div className="List">
            <h4>Todo List 🦕</h4>
            <input placeholder="검색어를 입력하세요" />
            <div>
                <TodoItem />
                <TodoItem />
                <TodoItem />
            </div>
        </div>
    );
};

export default List;
```

![Untitled](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%206.png)

**TodoItem 컴퍼넌트 구현**

- TodoItem.jsx

```jsx
import "./TodoItem.css";

const TodoItem = () => {
    return (
        <div className="TodoItem">
            <input type="checkbox" />
            <div className="content">Todo...</div>
            <div className="date">Date</div>
            <button>삭제</button>
        </div>
    );
};

export default TodoItem;
```

![Untitled](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%207.png)

→  components 폴더 안에 TodoItem.css 파일 추가

- TodoItem.css

```css
.TodoItem {
    display: flex;
    align-items: center;
    gap: 20px;
    padding-bottom: 20px;
    border-bottom: 1px solid rgb(240, 240, 240);
}

.TodoItem input {
    width: 20px;
}

.TodoItem .content {
    flex:  1;
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

![Untitled](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%208.png)

- List.jsx (TodoItem의 클래스 네임 설정)

```
            <div className="todos_wapper">
                <TodoItem />
                <TodoItem />
                <TodoItem />
            </div>
```

- List.css

```css
.List {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.List .todos_wapper {
    display: flex;
    flex-direction: column;
    gap: 20px;
}
```

![사이사이 간격 늘어남](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%209.png)

사이사이 간격 늘어남

## 기능 구현 준비하기

- 투두 아이템들의 데이터를 스테이트로 만들어서 보관해야 함 → 추가/삭제 등 변형되었을 때 바로바로 화면에 보여주기 때문
- 스테이트는 모든 컴포넌트의 조상인 APP 컴포넌트에 배치

![Untitled](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%2010.png)

```jsx
import { useState } from "react";
const [todos, setTodos] = useState([]); //이것들 추가
```

- 임시 데이터를 객체로 추가 (App() 외부에 추가해도 됨)

```jsx
const mockData = [ //몫 데이터
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
```

```jsx
const [todos, setTodos] = useState([mockData]); //App()내부에 있는 useState의 값을 mockData로 초기화
```

⇒ 개발자 창 → Components → App → State에서 저장된 것을 확인할 수 있음

![Untitled](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%2011.png)

## 기능 구현 - 새로운 투두 추가하기

**값 추가**

- App.jsx

```jsx
import './App.css'
import { useState } from "react";
import Header from './components/Header';
import Editor from './components/Editor';
import List from './components/List';

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
  const [todos, setTodos] = useState([mockData]);

  const onCreate = (content) => {
    const newTodo = {
      id : 0,
      isDone: false,
      content: content,
      date : new Date().getTime(),
    }

    setTodos([newTodo, ...todos]); /*무조건 이렇게 배열에 추가해야함*/
  };

  return (
    <div className="App">
      <Header />
      <Editor onCreate={onCreate} />
      <List />
    </div>
  );
}

export default App

```

- Editor.jsx

```jsx
import "./Editor.css"
import { useState } from "react";

const Editor = ({onCreate})=>{
    const [content, setContent] = useState("");

    const onChangeContent = (e) => {
        setContent(e.target.value);
    };

    const onsubmit = () => {
        onCreate(content);
    }

    return (
    <div className="Editor">
        <input value={content}
        onChange={onChangeContent}placeholder="새로운 Todo..."/>
        <button onClick={onsubmit}>추가</button>
    </div>
    );
};

export default Editor;
```

![123 추가했더니 배열 첫 번째에 들어간 것을 확인할 수 있음 ](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%2012.png)

123 추가했더니 배열 첫 번째에 들어간 것을 확인할 수 있음 

→ 문제: 추가하면 Id가 모두 0으로 나옴

**아이디를 기록하는 것을 따로 만들기**

- App.jsx

```jsx
import './App.css'
import { useState, useRef } from "react"; //추가
import Header from './components/Header';
import Editor from './components/Editor';
import List from './components/List';

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
  const [todos, setTodos] = useState([mockData]);
  const idRef = useRef(3) //추가

  const onCreate = (content) => {
    const newTodo = {
      id : idRef.current++, //추가
      isDone: false,
      content: content,
      date : new Date().getTime(),
    }

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

export default App

```

![아이템별로 고유 아이디 생성](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%2013.png)

아이템별로 고유 아이디 생성

**빈 입력 추가 방지하기**

- Editor.jsx

```jsx
import "./Editor.css"
import { useState, useRef } from "react"; //추가

const Editor = ({onCreate})=>{
    const [content, setContent] = useState("");
    const contentRef = useRef(); //추가

    const onChangeContent = (e) => {
        setContent(e.target.value);
    };

    const onsubmit = () => {
        if (content === "" ) { //추가
            contentRef.current.focus(); 
            return;
        }
        onCreate(content);
    };

    return (
    <div className="Editor">
        <input 
        ref={contentRef} //추가
        value={content}
        onChange={onChangeContent}placeholder="새로운 Todo..."/>
        <button onClick={onsubmit}>추가</button>
    </div>
    );
};

export default Editor;
```

**추가하면 인풋창에 있는 텍스트 비우기**

- Editor.jsx

```jsx
import "./Editor.css"
import { useState, useRef } from "react"; 

const Editor = ({onCreate})=>{
    const [content, setContent] = useState("");
    const contentRef = useRef(); 

    const onChangeContent = (e) => {
        setContent(e.target.value);
    };

    const onsubmit = () => {
        if (content === "" ) { 
            contentRef.current.focus(); 
            return;
        }
        onCreate(content);
        setContent(""); //추가
    };

    return (
    <div className="Editor">
        <input 
        ref={contentRef} 
        value={content}
        onChange={onChangeContent}placeholder="새로운 Todo..."/>
        <button onClick={onsubmit}>추가</button>
    </div>
    );
};

export default Editor;
```

**추가 버튼 안 누르고 엔터만 눌러도 추가되도록 하기**

- Editor.jsx

```jsx
import "./Editor.css"
import { useState, useRef } from "react"; 

const Editor = ({onCreate})=>{
    const [content, setContent] = useState("");
    const contentRef = useRef(); 

    const onChangeContent = (e) => {
        setContent(e.target.value);
    };

    const onKeydown = (e) => { //추가
        if (e.keyCode === 13) {
            onsubmit();
        }
    };

    const onsubmit = () => {
        if (content === "" ) { 
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
        onKeyDown={onKeydown} //추가
        onChange={onChangeContent}placeholder="새로운 Todo..."/>
        <button onClick={onsubmit}>추가</button>
    </div>
    );
};

export default Editor;
```

## 기능 구현 - 투두리스트 렌더링하기

- List.jsx

```jsx
import "./List.css";
import TodoItem from "./TodoItem";

const List = ({ todos }) => {
    return (
        <div className="List">
            <h4>Todo List 🦕</h4>
            <input placeholder="검색어를 입력하세요" />
            <div className="todos_wrapper">
                {todos.map((todo)=>{
                    return <TodoItem {...todo} />;
                })}
            </div>
        </div>
    );
};

export default List;
```

- TodoItem.jsx

```jsx
import "./TodoItem.css";

const TodoItem = ({id, isDone, content, date}) => {
    return (
        <div className="TodoItem">
            <input checked={isDone} type="checkbox" />
            <div className="content">{content}</div>
            <div className="date">{new Date(date).toLocaleDateString()}</div>
            <button>삭제</button>
        </div>
    );
};

export default TodoItem;
```

- List.jsx (검색어 필터링 기능)

```jsx
import "./List.css";
import TodoItem from "./TodoItem";
import { useState } from "react";

const List = ({ todos }) => {
    const [search, setSearch]=useState("");

    const onChangeSearch = (e) => {
        setSearch(e.target.value);
    };

    const getFilteredData = () => {
        if(search ===""){
            return todos;
        }
        return todos.filter((todo)=>
            todo.content.toLowerCase().includes(search.toLowerCase())
        );
    };

    const filteredTodos = getFilteredData();

    return (
        <div className="List">
            <h4>Todo List 🦕</h4>
            <input 
            value={search}
            onChange={onChangeSearch}
            placeholder="검색어를 입력하세요" />
            <div className="todos_wrapper">
                {filteredTodos.map((todo)=>{
                    return <TodoItem key={todo.id} {...todo} />;
                })}
            </div>
        </div>
    );
};

export default List;
```

## 기능 구현 - 투두 수정하기

- App.jsx

```jsx
import './App.css'
import { useState, useRef } from "react"; 
import Header from './components/Header';
import Editor from './components/Editor';
import List from './components/List';

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
  const [todos, setTodos] = useState([mockData]);
  const idRef = useRef(3) 

  const onCreate = (content) => {
    const newTodo = {
      id : idRef.current++, 
      isDone: false,
      content: content,
      date : new Date().getTime(),
    }

    setTodos([newTodo, ...todos]); 
  };

  const onUpdate = (targetId)=>{
    //todos State의 값들 중에
    //targetId와 일치하는 id를 갖는 투두 아이템의 isDone변경

    //인수: todos 배열에서 targetId와 일치하는 id를 갖는 요소의 데이터만 딱 바꾼 새로운 배열
    setTodos(
      todos.map((todo)=>
        todo.id === targetId
          ? { ...todo, isDone: !todo.isDone }
          : todo
      )
    );
  };

  return (
    <div className="App">
      <Header />
      <Editor onCreate={onCreate} />
      <List todos={todos} onUpdate={onUpdate} /> 
    </div>
  );
}

export default App

```

- List.jsx

```jsx
import "./List.css";
import TodoItem from "./TodoItem";
import { useState } from "react";

const List = ({ todos, onUpdate }) => {
    const [search, setSearch]=useState("");

    const onChangeSearch = (e) => {
        setSearch(e.target.value);
    };

    const getFilteredData = () => {
        if(search ===""){
            return todos;
        }
        return todos.filter((todo)=>
            todo.content.toLowerCase().includes(search.toLowerCase())
        );
    };

    const filteredTodos = getFilteredData();

    return (
        <div className="List">
            <h4>Todo List 🦕</h4>
            <input 
            value={search}
            onChange={onChangeSearch}
            placeholder="검색어를 입력하세요" />
            <div className="todos_wrapper">
                {filteredTodos.map((todo)=>{
                    return <TodoItem key={todo.id} {...todo} onUpdate={onUpdate} />;
                })}
            </div>
        </div>
    );
};

export default List;
```

- TodoItem.jsx

```jsx
import "./TodoItem.css";

const TodoItem = ({id, isDone, content, date, onUpdate }) => {

    const onChangeCheckbox = () => {
        onUpdate(id);
    };

    return (
        <div className="TodoItem">
            <input 
            onChange={onChangeCheckbox}
            readOnly
            checked={isDone} 
            type="checkbox" 
            />
            <div className="content">{content}</div>
            <div className="date">{new Date(date).toLocaleDateString()}</div>
            <button>삭제</button>
        </div>
    );
};

export default TodoItem;
```

## 기능 구현 - 투두 삭제하기

- App.jsx

```jsx
import './App.css'
import { useState, useRef } from "react";
import Header from './components/Header';
import Editor from './components/Editor';
import List from './components/List';

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
  const [todos, setTodos] = useState([mockData]);
  const idRef = useRef(3) 

  const onCreate = (content) => {
    const newTodo = {
      id : idRef.current++, 
      isDone: false,
      content: content,
      date : new Date().getTime(),
    }

    setTodos([newTodo, ...todos]); 
  };

  const onUpdate = (targetId)=>{

    setTodos(
      todos.map((todo)=>
        todo.id === targetId
          ? { ...todo, isDone: !todo.isDone }
          : todo
      )
    );
  };

  const onDelete = (targetId) => {
    //인수: todos 배열에서 targetId와 잃치하는 id를 갖는 요소만 삭제한 새로운 배열
    setTodos(todos.filter((todo)=>todo.id !== targetId));
  };

  return (
    <div className="App">
      <Header />
      <Editor onCreate={onCreate} />
      <List 
        todos={todos} 
        onUpdate={onUpdate} 
        onDelete={onDelete} /*추가*/
      /> 
    </div>
  );
}

export default App

```

- List.jsx

```jsx
import "./List.css";
import TodoItem from "./TodoItem";
import { useState } from "react";

const List = ({ todos, onUpdate, onDelete }) => { //추가
    const [search, setSearch]=useState("");

    const onChangeSearch = (e) => {
        setSearch(e.target.value);
    };

    const getFilteredData = () => {
        if(search ===""){
            return todos;
        }
        return todos.filter((todo)=>
            todo.content.toLowerCase().includes(search.toLowerCase())
        );
    };

    const filteredTodos = getFilteredData();

    return (
        <div className="List">
            <h4>Todo List 🦕</h4>
            <input 
            value={search}
            onChange={onChangeSearch}
            placeholder="검색어를 입력하세요" />
            <div className="todos_wrapper">
                {filteredTodos.map((todo)=>{
                    return (
                    <TodoItem 
                        key={todo.id} {...todo} 
                        onUpdate={onUpdate} 
                        onDelete={onDelete} //추가
                    />
                );
                })}
            </div>
        </div>
    );
};

export default List;
```

- TodoItem.css

```jsx
import "./TodoItem.css";

const TodoItem = ({
    id, 
    isDone, 
    content, 
    date, 
    onUpdate, 
    onDelete, //추가
}) => {

    const onChangeCheckbox = () => {
        onUpdate(id);
    };

    const onClickDeleteButton = ()=>{ //추가
        onDelete(id)
    }

    return (
        <div className="TodoItem">
            <input 
            onChange={onChangeCheckbox}
            readOnly
            checked={isDone} 
            type="checkbox" 
            />
            <div className="content">{content}</div>
            <div className="date">{new Date(date).toLocaleDateString()}</div>
            <button onClick={onClickDeleteButton}>삭제</button>  //추가
        </div>
    );
};

export default TodoItem;
```

![Untitled](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%2014.png)

![Untitled](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%2015.png)

완성!

# 09. 투두리스트 정리하기

### **useReducer**

컴포넌트 내부에 새로운 State를 생성하는 React Hook

모든 useState는 useReducer로 대체 가능

차이점: 상태 관리 코드를 컴포넌트 외부로 분리할 수 있음

상태를 관리하는 코드들은 길어질수록 App 외부에서 관리하는 것이 좋음

→ components폴더 안에 Exam.jsx 만들어서 알아볼 것임

 

- Exam.jsx

```jsx
import { useReducer } from "react";

// reducer : 변환기
// -> 상태를 실제로 변화시키는 변환기 역할
function reducer(state, action){
    console.log(state, action);
    if(action.type ==='INCREASE'){
        return state + action.data
    }
}

const Exam = ()=> {

    // daspatch: 발송하다, 급송하다
    // -> 상태 변화가 있어야 한다는 사실을 알리는, 발송하는 함수
    const [state, dispatch] = useReducer(reducer, 0);

    const onClickPlus = ()=>{
        // 인수 : 상태가 어떻게 변화되길 원하는 지
        // -> 액션 객체
        dispatch({
            type : "INCREASE",
            data: 1,
        });
    };

    return (
        <div>
         <h1>{state}</h1>
         <button onClick={onClickPlus}>+</button>
         </div>
    ); 
};

export default Exam;
```

![+버튼을 누르면 숫자 증가](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%2016.png)

+버튼을 누르면 숫자 증가

- Exam.jsx (if보다 switch로 하는게 더 일반적)

```jsx
import { useReducer } from "react";

// reducer : 변환기
// -> 상태를 실제로 변화시키는 변환기 역할
function reducer(state, action){
    console.log(state, action);
    if(action.type ==='INCREASE'){
        return state + action.data
    } else if (action.type === "DECREASE") {
        return state - action.data;
    }
}

const Exam = ()=> {

    // daspatch: 발송하다, 급송하다
    // -> 상태 변화가 있어야 한다는 사실을 알리는, 발송하는 함수
    const [state, dispatch] = useReducer(reducer, 0);

    const onClickPlus = ()=>{
        // 인수 : 상태가 어떻게 변화되길 원하는 지
        // -> 액션 객체
        dispatch({
            type : "INCREASE",
            data: 1,
        });
    };
    
    const onClickMinus = () => {
        dispatch({
            type : "DECREASE",
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

![Untitled](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%2017.png)

## 투두 리스트 업그레이드

- useReducer 이용해서 App.jsx 정리

```jsx
import './App.css'
import { useState, useRef, useReducer } from "react"; //추가
import Header from './components/Header';
import Editor from './components/Editor';
import List from './components/List';

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

function reducer(state, action){ //추가
  switch (action.type){
    case "CREATE":
      return [action.data, ...state];
    case "UPDATE":
      return state.map((item)=>
        item.id === action.targetId 
      ? {...item, isDone: !item.isDone}
      : item
    );
    case 'DELETE':
      return state.filter(
        (item)=>item.id !== action.targetId
    );
    default:
      return state;
  }
}

function App() {
  const [todos, dispatch] = useReducer(reducer, mockData); //추가
  const idRef = useRef(3) 

  const onCreate = (content) => { //변형
    dispatch({
      type :"CREATE",
      data : {
        id : idRef.current ++,
        isDone: false,
        content: content,
        date : new Date().getTime()
      },
    });
  };

  const onUpdate = (targetId)=>{ //변형
    dispatch({
      type: "UPDATE",
      targetId : targetId
    })
  };

  const onDelete = (targetId) => { //변형
    dispatch({
      type: "DELETE",
      targetId: targetId,
    });
  };

  return (
    <div className="App">

      <Header />
      <Editor onCreate={onCreate} />
      <List 
        todos={todos} 
        onUpdate={onUpdate} 
        onDelete={onDelete} 
      />
    </div>
  );
}

export default App

```

# 10. 최적화

**최적화**

웹 서비스의 성능을 개선하는 모든 행위를 일컫음

아주 단순한 것부터 아주 어려운 방법까지 매우 다양함

**리액트 최적화 방법**

컴포넌트 내부의 불필요한 연산 방지

컴포넌트 내부의 불필요한 함수 재생성 방지

컴포넌트의 불필요한 리렌더링 방지

useMemo

Memoization 기법을 기반으로 불필요한 연산을 최적화 하는 리액트 훅

- List.jsx

```jsx
import "./List.css";
import TodoItem from "./TodoItem";
import { useState } from "react";

const List = ({ todos, onUpdate, onDelete }) => { 
    const [search, setSearch]=useState("");

    const onChangeSearch = (e) => {
        setSearch(e.target.value);
    };

    const getFilteredData = () => {
        if(search ===""){
            return todos;
        }
        return todos.filter((todo)=>
            todo.content.toLowerCase().includes(search.toLowerCase())
        );
    };

    const filteredTodos = getFilteredData();

    const getAnalyzedData =()=>{ //추가
        const totalCount = todos.length;
        const doneCount = todos.filter(
            (todo)=>todo.isDone
        ).length;
        const notDoneCount = totalCount - doneCount;

        return {
            totalCount,
            doneCount,
            notDoneCount,
        }
    };

    const {totalCount, doneCount, notDoneCount} = getAnalyzedData()

    return (
        <div className="List">
            <h4>Todo List 🦕</h4>
            <div> {/*추가*/}
                <div>total: {totalCount}</div>
                <div>done: {doneCount}</div>
                <div>notDone: {notDoneCount}</div>
            </div>
            <input 
            value={search}
            onChange={onChangeSearch}
            placeholder="검색어를 입력하세요" />
            <div className="todos_wrapper">
                {filteredTodos.map((todo)=>{
                    return (
                    <TodoItem 
                        key={todo.id} {...todo} 
                        onUpdate={onUpdate} 
                        onDelete={onDelete} 
                    />
                );
                })}
            </div>
        </div>
    );
};

export default List;
```

![Untitled](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%2018.png)

문제: 연산이 너무 오래 걸림 → useMemo 사용

- List.jsx

```jsx
import "./List.css";
import TodoItem from "./TodoItem";
import { useState, useMemo } from "react"; //useMemo 추가

const List = ({ todos, onUpdate, onDelete }) => { 
    const [search, setSearch]=useState("");

    const onChangeSearch = (e) => {
        setSearch(e.target.value);
    };

    const getFilteredData = () => {
        if(search ===""){
            return todos;
        }
        return todos.filter((todo)=>
            todo.content.toLowerCase().includes(search.toLowerCase())
        );
    };

const filteredTodos = getFilteredData(); //추가

//추가
const {totalCount, doneCount, notDoneCount} = 
    useMemo(()=>{
        const totalCount = todos.length;
        const doneCount = todos.filter(
            (todo)=>todo.isDone
        ).length;
        const notDoneCount = totalCount - doneCount;

        return {
            totalCount,
            doneCount,
            notDoneCount,
        };
    }, [todos]);

    //const {totalCount, doneCount, notDoneCount} = getAnalyzedData()

    return (
        <div className="List">
            <h4>Todo List 🦕</h4>
            <div> 
                <div>total: {totalCount}</div>
                <div>done: {doneCount}</div>
                <div>notDone: {notDoneCount}</div>
            </div>
            <input 
            value={search}
            onChange={onChangeSearch}
            placeholder="검색어를 입력하세요" />
            <div className="todos_wrapper">
                {filteredTodos.map((todo)=>{
                    return (
                    <TodoItem 
                        key={todo.id} {...todo} 
                        onUpdate={onUpdate} 
                        onDelete={onDelete} 
                    />
                );
                })}
            </div>
        </div>
    );
};

export default List;
```

![Untitled](3%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A5%E1%84%83%E1%85%B5%20e77e7a398df049ed8438bc9e2fdcc4be/Untitled%2019.png)