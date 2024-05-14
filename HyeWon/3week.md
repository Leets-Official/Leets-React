# 3주차

**강의**
[인프런] - 한입 크기로 잘라머는 리액트(React.js) : 기초부터 실전까지
(https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8)

### 범위

섹션 8 ~ 섹션 12.5

- [] 8. 프로젝트2. 투두리스트
- [] 9. useReducer
- [] 10. 최적화
- [] 11. Context
- [] 12. 프로젝트3. 감정 일기장 5강

---

</br>

### 학습 내용

# ch08. 프로젝트2 : 투두리스트

- 각각의 섹션 만들 떄:

## 2. UI 구현하기

![Untitled](ch08%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B32%20%E1%84%90%E1%85%AE%E1%84%83%E1%85%AE%E1%84%85%E1%85%B5%E1%84%89%E1%85%B3%E1%84%90%E1%85%B3%20144689c094f1440ab9628ba2994012e6/Untitled.png)

1. 앞에서처럼 필요 없는 코드들, 파일들 없애기
2. src 아래 components 폴더 만들고 header.jsx, edit.jsx, … 파일 만들기
3. 각 파일에 기본적인 코드 작성

   ```jsx
   // e.g., Header.jsx

   const Header = () => {
     return <div>Header</div>;
   };

   export default Header;
   ```

   ```jsx
   import './App.css' -> 이 다음엔 App.css로 이동
   import Header from "./components/Header";
   import Editor from "./components/Editor";
   import List from "./components/List";

   function App() {

     return (
       <div className="App">
       <Header/>  // -> 랜더링되게 함!
       <Editor/>
       <List/>
       </div>
     )
   }

   export default App
   ```

   ```css
   .App {
     // 한가운데 오도록!
     width: 500px;
     margin: 0 auto;

     // flex(유동적) 사용
     display: flex;
     flex-direction: column; // 세로줄로 나열되도록
     gap: 10px; // 각 글자간 간격 (gap은 flex일때만 사용가능)
   }
   ```

4. Header 요소 완성 시키기

   - tip : window + . = 이모지 입력 가능함

   ```jsx
   // Header.jsx

   import "./Header.css";

   const Header = () => {
     return (
       <div className="Header">
         <h3>오늘은 📆</h3>
         <h1>{new Date().toDateString()}</h1>
       </div>
     );
   };

   export default Header;
   ```

   ```css
   // Header.css

   .Header > h1 {
     color: rgb(37, 147, 255);
   }
   ```

   ![Untitled](ch08%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B32%20%E1%84%90%E1%85%AE%E1%84%83%E1%85%AE%E1%84%85%E1%85%B5%E1%84%89%E1%85%B3%E1%84%90%E1%85%B3%20144689c094f1440ab9628ba2994012e6/Untitled%201.png)

5. Edit 요소 완성시키기

   ```jsx
   //Editor.jsx

   import "./Editor.css";

   const Editor = () => {
     return (
       <div className="Editor">
         <input placeholder="새로운 Todo..." />
         <button>추가</button>
       </div>
     );
   };

   export default Editor;
   ```

   ```css
   //Editor.css

   .Editor {
     display: flex;
     gap: 10px;
   }

   .Editor input {
     flex: 1; // 벗어나지 않는 범위에서 최대로 입력칸이 늘어나게 됨
     padding: 15px; // 내부 영역
     border: 1px solid rgb(220, 220, 220); // 테두리
     border-radius: 5px; // 모서리 얼마나 둥글게 할지
   }

   .Editor button {
     cursor: pointer; // 마우스 갖다대면 마우스 모양으로 바뀌도록
     width: 80px;
     border: none;
     background-color: rgb(37, 147, 255); // 색은 제목 색과 같도록
     color: white;
     border-radius: 5px;
   }
   ```

   ![Untitled](ch08%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B32%20%E1%84%90%E1%85%AE%E1%84%83%E1%85%AE%E1%84%85%E1%85%B5%E1%84%89%E1%85%B3%E1%84%90%E1%85%B3%20144689c094f1440ab9628ba2994012e6/Untitled%202.png)

6. List 요소 완성시키기

   ```jsx
   // List.jsx

   import "./List.css";
   import TodoItem from "./TodoItem"; // 왜 계속 오류라는 거임?

   const List = () => {
     return (
       <div className="List">
         <h4>Todo List 🌱</h4>
         <input placeholder="검색어를 입력하세요" />
         <div className="todos_wrapper">
           <TodoItem />
           <TodoItem />
           <TodoItem />
         </div>
       </div>
     );
   };

   export default List;
   ```

   ```css
   // List.css

   .List {
     display: flex; //가로로 나
     flex-direction: column; // 세로로 만들기
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
   //TodoItem.jsx

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

   ```css
   //TodoItem.css

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

   ![Untitled](ch08%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B32%20%E1%84%90%E1%85%AE%E1%84%83%E1%85%AE%E1%84%85%E1%85%B5%E1%84%89%E1%85%B3%E1%84%90%E1%85%B3%20144689c094f1440ab9628ba2994012e6/Untitled%203.png)

## 3. Todo-List 기능 구현하기

- App component 안에 todos라는 새로운 state 만들고,
  이제부터 이 state의 모든 아이템들을 보관하기로 함

```jsx
// App.jsx

import "./App.css";
import { useState } from "react";
import Header from "./components/Header";
import Editor from "./components/Editor";
import List from "./components/List";

const mockData = [
  // = 임시데이터
  {
    id: 0,
    isDone: false,
    content: "React 공부하기",
    date: new Date().getTime(),
  },
  {
    id: 1,
    isDone: false,
    content: "과제하기",
    date: new Date().getTime(),
  },
  {
    id: 2,
    isDone: false,
    content: "영어 공부하기",
    date: new Date().getTime(),
  },
];

function App() {
  const [todos, setTodos] = useState(mockData); //처음: 여러개 넣을까니까 빈 배열
  return (
    <div className="App">
      <Header />
      <Editor />
      <List />
    </div>
  );
}

export default App;
```

## 4. TodoList - Create(투두 추가하기)

- editor component에 새로운 todo를 입력하고 추가 버튼 누르면
  코드상의 todos state값을 변경해줘야 함(setTodos)
  → setTodos를 직접 호출해 값을 바꿔줘야겠군!

+state의 값은 상태변화함수를 통해서만 수정 가능!

```jsx
//App.jsx

import "./App.css";
import { useState, useRef } from "react";
import Header from "./components/Header";
import Editor from "./components/Editor";
import List from "./components/List";

const mockData = [
  // = 임시데이터
  {
    id: 0,
    isDone: false,
    content: "React 공부하기",
    date: new Date().getTime(),
  },
  {
    id: 1,
    isDone: false,
    content: "과제하기",
    date: new Date().getTime(),
  },
  {
    id: 2,
    isDone: false,
    content: "영어 공부하기",
    date: new Date().getTime(),
  },
];

function App() {
  const [todos, setTodos] = useState(mockData);
  const idRef = useRef(3); // 앞에 있는 2랑 안 겹치려고 3 함

  const onCreate = (content) => {
    //onCreate함수를 통해 props로 Editor 컴포넌트에 전달
    const newTodo = {
      // , 새로운 todo 추가되게 함
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

- 추가적인 완성도를 위한 작업들

```jsx
// Editor.jsx

import "./Editor.css";
import { useState, useRef } from "react";

const Editor = ({ onCreate }) => {
  const [content, setContent] = useState("");
  const contentRef = useRef();

  const onChangeContent = (e) => {
    setContent(e.target.value);
  };

  const onKeydown = (e) => {
    // 엔터 눌렀을 때도 잘 실행되도록 함
    if (e.KeyCode === 13) {
      onSubmit();
    }
  };

  const onSubmit = () => {
    if (content === "") {
      contentRef.current.focus(); // 빈칸 비어있을 때 추가 누르면 빈칸 강조됨
      return;
    }
    onCreate(content);
    setContent(""); // 값 입력 후, 다시 입력하기 쉽게 칸이 초기화됨(비게)
  };

  return (
    <div className="Editor">
      <input
        ref={contentRef}
        value={content}
        onKeyDown={onKeydown}
        onChange={onChangeContent}
        placeholder="새로운 Todo..."
      />
      <button onClick={onSubmit}>추가</button>
    </div>
  );
};

export default Editor;
```

## 5. TodoList - Read (투두리스트 렌더링)

- 리스트 형태로 렌더링 하기
  → app component의 todos component에 저장된 데이터를 List component에서
  map 메서드를 통해 List 형태로 렌더링하기
  ![Untitled](ch08%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B32%20%E1%84%90%E1%85%AE%E1%84%83%E1%85%AE%E1%84%85%E1%85%B5%E1%84%89%E1%85%B3%E1%84%90%E1%85%B3%20144689c094f1440ab9628ba2994012e6/Untitled%204.png)
- search를 했을 때, 관련 키워드와 연관된 목록이 뜨도록 설정
  ![Untitled](ch08%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B32%20%E1%84%90%E1%85%AE%E1%84%83%E1%85%AE%E1%84%85%E1%85%B5%E1%84%89%E1%85%B3%E1%84%90%E1%85%B3%20144689c094f1440ab9628ba2994012e6/Untitled%205.png)

```jsx
// List.jsx

import "./List.css";
import TodoItem from "./TodoItem";
import { useState } from "react";

const List = ({ todos }) => {
  const [search, setSearch] = useState("");

  const onChangeSearch = (e) => {
    setSearch(e.target.value);
  };

  const getFilteredData = () => {
    if (search === "") {
      return todos;
    }
    // search 시, 콜백함수를 통해 todo 중 참이 되는 함수를 반환(?)
    // content에는 "React 공부하기" 등이 포함되어있음
    // includes는 특정 요소 들어있으면 참, 아니면 거짓
    // toLowerCase()는 대소문자 신경 X
    return todos.filter((todo) =>
      todo.content.toLowerCase().includes(search.toLowerCase())
    );
  };

  const filteredTodos = getFilteredData();

  return (
    <div className="List">
      <h4>Todo List 🌱</h4>
      <input
        value={search}
        onChange={onChangeSearch}
        placeholder="검색어를 입력하세요"
      />
      <div className="todos_wrapper">
        {filteredTodos.map((todo) => {
          // 리스트로 렌더링하기
          return <TodoItem key={todo.id} {...todo} />;
        })}
      </div>
    </div>
  );
};

export default List;
```

## 6. TodoList - Update (투두 수정하기)

체크박스 클릭하면 하나의 아이템을 수정하는 기능 만들기

![Untitled](ch08%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B32%20%E1%84%90%E1%85%AE%E1%84%83%E1%85%AE%E1%84%85%E1%85%B5%E1%84%89%E1%85%B3%E1%84%90%E1%85%B3%20144689c094f1440ab9628ba2994012e6/Untitled%206.png)

```jsx
//App.jsx

import "./App.css";
import { useState, useRef } from "react";
import Header from "./components/Header";
import Editor from "./components/Editor";
import List from "./components/List";

const mockData = [
  // = 임시데이터
  {
    id: 0,
    isDone: false,
    content: "React 공부하기",
    date: new Date().getTime(),
  },
  {
    id: 1,
    isDone: false,
    content: "과제하기",
    date: new Date().getTime(),
  },
  {
    id: 2,
    isDone: false,
    content: "영어 공부하기",
    date: new Date().getTime(),
  },
];

function App() {
  const [todos, setTodos] = useState(mockData);
  const idRef = useRef(3); // 앞에 있는 2랑 안 겹치려고 3 함

  const onCreate = (content) => {
    const newTodo = {
      id: idRef.current++,
      isDone: false,
      content: content,
      date: new Date().getTime(),
    };

    setTodos([newTodo, ...todos]);
  };

  const onUpdate = (targetId) => {
    // todos State의 값들 중에
    // targetID와 일치하는 id를 갖는 투두 아이템의 isDone 변경

    // 인수: todos 배열에서 targetId와 일치하는 id를 갖는 요소의 데이터만 딱 바꾼 새로운 배열
    setTodos(
      todos.map((todo) =>
        todo.id === targetId ? { ...todo, isDone: !todo.isDone } : todo
      )
    );
    // = 위의 코드랑 같은 의미
    // if(todo.id === targetId){
    //   return {
    //   ...todo,
    //   isDone: !todo.isDone
    //   }
    // }
    // return todo
  };

  return (
    <div className="App">
      <Header />
      <Editor onCreate={onCreate} />
      <List todos={todos} onUpdate={onUpdate} />
    </div>
  );
}

export default App;
```

```jsx
// List.jsx (App의 자식)

import "./List.css";
import TodoItem from "./TodoItem";
import { useState } from "react";

const List = ({ todos, onUpdate }) => {
  const [search, setSearch] = useState("");

  const onChangeSearch = (e) => {
    setSearch(e.target.value);
  };

  const getFilteredData = () => {
    if (search === "") {
      return todos;
    }
    return todos.filter((todo) =>
      todo.content.toLowerCase().includes(search.toLowerCase())
    );
  };

  const filteredTodos = getFilteredData();

  return (
    <div className="List">
      <h4>Todo List 🌱</h4>
      <input
        value={search}
        onChange={onChangeSearch} //
        placeholder="검색어를 입력하세요"
      />
      <div className="todos_wrapper">
        {filteredTodos.map((todo) => {
          // 리스트로 렌더링하기
          return <TodoItem key={todo.id} {...todo} onUpdate={onUpdate} />;
        })}
      </div>
    </div>
  );
};

export default List;
```

```jsx
//todoItem.jsx (List.jsx의 자식)

import "./TodoItem.css";

const TodoItem = ({ id, isDone, content, date, onUpdate }) => {
  const onChangeCheckbox = () => {
    onUpdate(id);
  };
  return (
    <div className="TodoItem">
      <input
        onChange={onChangeCheckbox} // onClick이 아니라 onChange 이벤트 핸들러 사용이유:
        readOnly // 이 요소가 버튼이 아니라 input 요소여서
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

## 7. TodoList - Delete (투두 삭제하기)

- 삭제 버튼 누르면 리스트가 삭제되도록 → 마찬가지로 todos state값을 수정해야 함
  → 1. 삭제 버튼은 List 섹션을 고쳐야 하므로 App→List→TodoItem 고쳐야겠다 판단
  → 2. App에서 이에 관한 const 만들고, return안에 콜백함수로..
  → 3. List에서 const List에서 인수로 받기, return으로 받음
  → 4. todoItem에서 const TodoItem에서 인수로 받기, onClickDeleteButton 함수 만들기
  return으로 받

```jsx
// App.jsx

import "./App.css";
import { useState, useRef } from "react";
import Header from "./components/Header";
import Editor from "./components/Editor";
import List from "./components/List";

const mockData = [
  // = 임시데이터
  {
    id: 0,
    isDone: false,
    content: "React 공부하기",
    date: new Date().getTime(),
  },
  {
    id: 1,
    isDone: false,
    content: "과제하기",
    date: new Date().getTime(),
  },
  {
    id: 2,
    isDone: false,
    content: "영어 공부하기",
    date: new Date().getTime(),
  },
];

function App() {
  const [todos, setTodos] = useState(mockData);
  const idRef = useRef(3); // 앞에 있는 2랑 안 겹치려고 3 함

  const onCreate = (content) => {
    const newTodo = {
      id: idRef.current++,
      isDone: false,
      content: content,
      date: new Date().getTime(),
    };

    setTodos([newTodo, ...todos]);
  };

  const onUpdate = (targetId) => {
    // todos State의 값들 중에
    // targetID와 일치하는 id를 갖는 투두 아이템의 isDone 변경

    // 인수: todos 배열에서 targetId와 일치하는 id를 갖는 요소의 데이터만 딱 바꾼 새로운 배열
    setTodos(
      todos.map((todo) =>
        todo.id === targetId ? { ...todo, isDone: !todo.isDone } : todo
      )
    );
  };

  const onDelete = (targetId) => {
    // 인수: todos 배열에서 targetId와 일치하는 id를 찾는 요소만 삭제한 새로운 배열
    // 기존 배열에서 조건을 만족하는 배열만 제외하고 필터링
    setTodos(todos.filter((todo) => todo.id !== targetId));
  };

  return (
    <div className="App">
      <Header />
      <Editor onCreate={onCreate} />
      <List todos={todos} onUpdate={onUpdate} onDelete={onDelete} /> //
    </div>
  );
}

export default App;
```

```jsx
// List.jsx

import "./List.css";
import TodoItem from "./TodoItem";
import { useState } from "react";

const List = ({ todos, onUpdate, onDelete }) => {
  const [search, setSearch] = useState("");

  const onChangeSearch = (e) => {
    setSearch(e.target.value);
  };

  const getFilteredData = () => {
    if (search === "") {
      return todos;
    }
    return todos.filter((todo) =>
      todo.content.toLowerCase().includes(search.toLowerCase())
    );
  };

  const filteredTodos = getFilteredData();

  return (
    <div className="List">
      <h4>Todo List 🌱</h4>
      <input
        value={search}
        onChange={onChangeSearch}
        placeholder="검색어를 입력하세요"
      />
      <div className="todos_wrapper">
        {filteredTodos.map((todo) => {
          // 리스트로 렌더링하기
          return (
            <TodoItem
              key={todo.id}
              {...todo}
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

```jsx
// TodoItem.jsx

import "./TodoItem.css";

const TodoItem = ({ id, isDone, content, date, onUpdate, onDelete }) => {
  const onChangeCheckbox = () => {
    onUpdate(id);
  };

  const onClickDeleteButton = () => {
    onDelete(id);
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
      <button onClick={onClickDeleteButton}>삭제</button>
    </div>
  );
};

export default TodoItem;
```

# ch09. useReducer

## 1. useReducer

= 컴포넌트 내부에 새로운 State를 생성하는 React Hook

모든 useState는 useReducer로 대체 가능!

→ useState와의 차이점 : useReducer는 상태 관리 코드를 컴포넌트 외부로 분리 가

![Untitled](ch09%20useReducer%20cd6f840ab8ed44a492cdb116b692fe60/Untitled.png)

![Untitled](ch09%20useReducer%20cd6f840ab8ed44a492cdb116b692fe60/Untitled%201.png)

→ UserReducer쓰는 이유 :

state가 복잡해지거나 다양한 상태 변화를 제공하게 되면 컴포넌트 안에 더 긴 코드 작성하게 됨(+App 컴포넌트의 주된 목적은 UI를 렌더링하는 것!)

```jsx
// Exam.jsx

import { useReducer } from "react";

// reducer : 변환기
// -> 상태를 실제로 변화시키는 변환기 역할
function reducer(state, action) {
  console.log(state, action);
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
  // 따라서 useReducer가 상태변화를 실제로 처리할 함수 호출, 두 번째 인수는 초기값

  const onClickPlus = () => {
    // 인수: 상태가 어떻게 변화되길 원하는지
    // -> 액션 객체 (type, data)
    dispatch({
      type: "INCREASE",
      data: 1, // 1만큼
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

![Untitled](ch09%20useReducer%20cd6f840ab8ed44a492cdb116b692fe60/Untitled%202.png)

## 2. TodoList 앱 업그레이드 (useReducer)

삭제 버튼 눌렀을 때 삭제되는 기능 (Reducer로)

→ 가독성이 좋음.

→ dispatch 함수를 통해 바로바로 볼 수 있음

```jsx
// App.jsx

import "./App.css";
import { useState, useRef, useReducer } from "react";
import Header from "./components/Header";
import Editor from "./components/Editor";
import List from "./components/List";

const mockData = [
  // = 임시데이터
  {
    id: 0,
    isDone: false,
    content: "React 공부하기",
    date: new Date().getTime(),
  },
  {
    id: 1,
    isDone: false,
    content: "과제하기",
    date: new Date().getTime(),
  },
  {
    id: 2,
    isDone: false,
    content: "영어 공부하기",
    date: new Date().getTime(),
  },
];

function reducer(state, action) {
  switch (action.type) {
    case "CREATE":
      return [action.data, ...state];
    case "UPDATE":
      return state.map((item) =>
        item.id === action.target.Id ? { ...item, isDone: !item.isDone } : item
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
      targetId: targetId, // 어떤 요소 수정할지만 전달
    });
  };

  const onDelete = (targetId) => {
    dispatch({
      type: "DELETE",
      targetId: targetId,
    });
  };

  return (
    <div className="App">
      <Header />
      <Editor onCreate={onCreate} />
      <List todos={todos} onUpdate={onUpdate} onDelete={onDelete} />
    </div>
  );
}

export default App;
```

# ch10. (여기서부터 작동 안 됨)

## 1. 최적화

= 웹 서비스의 성능을 개선하는 모든 행위

- 일반적인 웹 서비스 최적화 방법
- React App 내부의 최적화 방법

## 2. useMemo - 불필요한 연산 방지

useMemo = 메모리제이션(기억) 기법을 기반으로 불필요한 연산을 최적화하는 리액트

→ 반복적으로 수행되는 동일한 연산을 할 때,

최초로 한 번 계산했을 때의 결과값을 메모리 어딘가에 보관해둔다.

이후에 또 동일한 연산을 수행해야 할 때 거기서 가져다 쓴다.

+다시는 생성 못하도록 감싸 줌

```jsx
// List.jsx (근데 왜 페이지가 계속 오류가 뜨는지 모르겠다..)-여기서부터

const filteredTodos = getFilteredData();

    const {totalCount, doneCount, notDoneCount} =
     useMemo(()=>{
        console.log("getAnalyzeData 호출!");
        const totalCount = todos.length;
        const doneCount = todos.filter(
            (todo)=> todo.isDone
        ).length;
        const notDoneCount = totalCount-doneCount;

        return {
            totalCount,
            donecount,
            notDoneCount,
        }
    }, [todos]);
    // 의존성 배열 : deps

    // const {totalCount, doneCount, notDoneCount} =  getAnalyizedDate(); //구조분해할당

    return (
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
         {filteredTodos.map((todo)=>{ // 리스트로 렌더링하기
          return (
          <TodoItem
            key={todo.id}
            {...todo}
            onUpdate={onUpdate}
            onDelete={onDelete}
          />
        );
    })}
        </div>
    </div>
    )
};

```

## 3. React.memo - 불필요한 리렌더링 방지하기

React.memo = 컴포넌트를 인수로 받아 최적화된 컴포넌트로 만들어 반환

![Untitled](<ch10%20(%E1%84%8B%E1%85%A7%E1%84%80%E1%85%B5%E1%84%89%E1%85%A5%E1%84%87%E1%85%AE%E1%84%90%E1%85%A5%20%E1%84%8C%E1%85%A1%E1%86%A8%E1%84%83%E1%85%A9%E1%86%BC%20%E1%84%8B%E1%85%A1%E1%86%AB%20%E1%84%83%E1%85%AC%E1%86%B7)%201306a6f3e2104f83955312f4ba1d7b1d/Untitled.png>)

![Untitled](<ch10%20(%E1%84%8B%E1%85%A7%E1%84%80%E1%85%B5%E1%84%89%E1%85%A5%E1%84%87%E1%85%AE%E1%84%90%E1%85%A5%20%E1%84%8C%E1%85%A1%E1%86%A8%E1%84%83%E1%85%A9%E1%86%BC%20%E1%84%8B%E1%85%A1%E1%86%AB%20%E1%84%83%E1%85%AC%E1%86%B7)%201306a6f3e2104f83955312f4ba1d7b1d/Untitled%201.png>)

```jsx
// TodoItem.jsx

// 고차 컴포넌트 (HOC)
export default memo(TodoItem, (prevProps, nextProps) => {
  // 반환값에 따라, Props가 바뀌었는지 안 바뀌었는지 판단
  // T->Props 바뀌지 X - > 리렌더링 X
  // F - > Props 바뀜 -> 리렌더링 O

  if (prevProps.id !== nextProps.is) return false;
  if (prevProps.isDone !== nextProps.isDone) return false;
  if (prevProps.content !== nextProps.content) return false;
  if (prevProps.date !== nextProps.date) return false;

  return true;
});
```

```jsx
// Header.jsx

import "./Header.css";
import { memo } from "react";

const Header = () => {
  return (
    <div className="Header">
      <h3>오늘은 📆</h3>
      <h1>{new Date().toDateString()}</h1>
    </div>
  );
};

// const memoizedHeader = memo(Header) // 최적화하고 싶은 컴포넌트 인수로 넣기
// 자신이 받은 props가 바뀌지 않으면 다시는 리렌더링 발생 X

export default memo(Header);
```

```jsx
// App.jsx

import "./App.css";
import { useState, useRef, useReducer } from "react";
import Header from "./components/Header";
import Editor from "./components/Editor";
import List from "./components/List";

const mockData = [
  // = 임시데이터
  {
    id: 0,
    isDone: false,
    content: "React 공부하기",
    date: new Date().getTime(),
  },
  {
    id: 1,
    isDone: false,
    content: "과제하기",
    date: new Date().getTime(),
  },
  {
    id: 2,
    isDone: false,
    content: "영어 공부하기",
    date: new Date().getTime(),
  },
];

function reducer(state, action) {
  switch (action.type) {
    case "CREATE":
      return [action.data, ...state];
    case "UPDATE":
      return state.map((item) =>
        item.id === action.target.Id ? { ...item, isDone: !item.isDone } : item
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
      targetId: targetId, // 어떤 요소 수정할지만 전달
    });
  };

  const onDelete = (targetId) => {
    dispatch({
      type: "DELETE",
      targetId: targetId,
    });
  };

  return (
    <div className="App">
      <Header />
      <Editor onCreate={onCreate} />
      <List todos={todos} onUpdate={onUpdate} onDelete={onDelete} />
    </div>
  );
}

export default App;
```

## 4. UseCallback - 불필요한 함수 재생성 방지하기

useCallBack(()=>{},[]) // 첫번째 인수 = 불필요하게 재생성하고 싶지 않은 인수

- 리액트 최적화 적절 시기 : 하나의 프로젝트 거의 완성한 시기

→ 따라서, 순서는 1. 기능 구현 2. 최적화(마지막에 하는 게 좋음)

- 최적화 대상 : 최적화가 꼭 필요할 것 같은 연산, 함수, 컴포넌트에 사용해야

```jsx
// App.jsx

const onCreate = useCallBack((content) => {
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

const onUpdate = useCallBack(() => {
  (targetId) => {
    dispatch({
      type: "UPDATE",
      targetId: targetId, // 어떤 요소 수정할지만 전달
    });
  };
}, []);

// 마운트될 때만 딱 한 번 생성! 아무리 리렌더링 많이 발생해도 다시는 생성 X게 최적화!
const onDelete = useCallBack((targetId) => {
  dispatch({
    type: "DELETE",
    targetId: targetId,
  });
}, []); // 두 번째 인수를 빈 배열로 해서 한 번 하고, 다시는 생성하지 않게!
```

```jsx
// TodoItem.jsx
//고차 컴포넌트 지우고 밑의 내용만 수정
// 고차 컴포넌트 대신 위의 App.jsx에서도 최적화 가능!

export default memo(TodoItem);
```

# ch11. Context

## 1. Context

- React context = 컴포넌트간의 데이터를 전달하는 또 다른 방법

                                 기존의 Props가 가지고 있던 단점 해결 가능

- Props의 단점 : Props Drilling
  Props는 부모→자식으로만 데이터를 전달할 수 있었음
  ![Untitled](ch11%20Context%20462819bc36e742bc8246395f4ea04ddf/Untitled.png)
  → 중간 다리를 거쳐 이중으로 가야 했음 ( not good..)
- React Context(위 문제의 솔루션)
  context = 데이터 보관소 (객체)
  context에 데이터 보관해놨다가 필요한 애들에게 데이터 공급 가능
  ![Untitled](ch11%20Context%20462819bc36e742bc8246395f4ea04ddf/Untitled%201.png)

## 2. Context 사용하기

![Untitled](ch11%20Context%20462819bc36e742bc8246395f4ea04ddf/Untitled%202.png)

+여기서 생긴 문제 3에서 다룰 것. (3이 최종)

## 3. Context 분리하기

P) 원래는 memo method를 써서 자신이 받는 Props가 바뀌지 않으면

아예 리렌더링 안 되도록 해서 최적화를 하려고 했었는데

근데, 지금은 왜 리렌더링이 되는거지?

→ 새로운 todo를 추가하거나 기존 todo를 수정, 삭제하는 경우,

App 컴포넌트의 todos state가 변경되어서

App 컴포넌트가 리렌더링 될텐데

Provider 컴포넌트에게 value Props로 전달하는 객체 자체가

다시 생성되기 때문이다.

![Untitled](ch11%20Context%20462819bc36e742bc8246395f4ea04ddf/Untitled%203.png)

따라서, TodoItem 컴포넌트에서 useContext를 호출해서

TodoContext로부터 불러온 이 객체 자체가 생성되는 거기 때문에

결국 TodoItem 컴포넌트도 리렌더링 발생하는 것임.

![Untitled](ch11%20Context%20462819bc36e742bc8246395f4ea04ddf/Untitled%204.png)

S) TodoContext를 두 개로 분리해서 해결 가능

![Untitled](ch11%20Context%20462819bc36e742bc8246395f4ea04ddf/Untitled%205.png)

![Untitled](ch11%20Context%20462819bc36e742bc8246395f4ea04ddf/Untitled%206.png)

```jsx
// App.jsx

import './App.css'
import {useState, useRef, useReducer, useCallBack, createContext, useMemo} from "react";
import Header from "./components/Header";
import Editor from "./components/Editor";
import List from "./components/List";

const mockData=[ // = 임시데이터
    {
      id: 0,
      isDone: false,
      content: "React 공부하기",
      date: new Date().getTime(),
    },
    {
      id: 1,
      isDone: false,
      content: "과제하기",
      date: new Date().getTime(),
    },
    {
      id: 2,
      isDone: false,
      content: "영어 공부하기",
      date: new Date().getTime(),
    },
  ];

  function reducer(state, action){
    switch(action.type){
      case "CREATE":
        return [action.data, ...state]
      case "UPDATE":
        return state.map((item)=>
          item.id === action.target.Id
           ? {...item, isDone: !item.isDone}
           : item
        )
      case "DELETE":
        return state.filter(
          (item)=>item.id !== action.targetId)
      default:
        return state;
  }
}

export const TodoStateContext = createContext();
export const TodoDispatchContext = createContext();

function App() {
  const [todos, dispatch] = useReducer(reducer, mockData);
  const idRef = useRef(3);

  const onCreate = useCallBack((content)=>{
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

  const onUpdate = useCallBack(()=>{
    (targetId)=>{
      dispatch({
        type: "UPDATE",
        targetId: targetId, // 어떤 요소 수정할지만 전달
      })
    }
  },[])

  // 마운트될 때만 딱 한 번 생성! 아무리 리렌더링 많이 발생해도 다시는 생성 X게 최적화!
  const onDelete = useCallBack((targetId)=>{
    dispatch({
      type: "DELETE",
      targetId: targetId,
    })
  }, []) // 두 번째 인수를 빈 배열로 해서 한 번 하고, 다시는 생성하지 않게!

  const memoizedDispatch = useMemo(()=>{
    return {onCreate, onUpdate, onDelete};
  }, []);

  return (
    <div className="App">
    <Header />
      <TodoStateContext.Provider value={todos}>
        <TodoDispatchContext.Provider
          value={{memoizedDispatch}}
        >
          <Editor />
          <List />
        </TodoDispatchContext.Provider>
      </TodoStateContext.Provider>
    </div>
  )
}

export default App;

// Head.jsx

import "./Header.css";
import {memo} from "react";

const Header = ()=>{
    return (
    <div className="Header">
        <h3>오늘은 📆</h3>
        <h1>{new Date().toDateString()}</h1>
    </div>
    )
};

// const memoizedHeader = memo(Header) // 최적화하고 싶은 컴포넌트 인수로 넣기
// 자신이 받은 props가 바뀌지 않으면 다시는 리렌더링 발생 X

export default memo(Header);
```

```jsx
//Editor.jsx

import { useState, useRef, useContext } from "react";
import "./Editor.css";
import { TodoDispatchContext } from "../App";

const Editor = () => {
  const { onCreate } = useContext(TodoDispatchContext);
  const [content, setContent] = useState("");
  const contentRef = useRef();

  const onChangeContent = (e) => {
    setContent(e.target.value);
  };

  const onKeydown = (e) => {
    // 엔터 눌렀을 때도 잘 실행되도록 함
    if (e.KeyCode === 13) {
      onSubmit();
    }
  };

  const onSubmit = () => {
    if (content === "") {
      contentRef.current.focus(); // 빈칸 비어있을 때 추가 누르면 빈칸 강조됨
      return;
    }
    onCreate(content);
    setContent(""); // 값 입력 후, 다시 입력하기 쉽게 칸이 초기화됨(비게)
  };

  return (
    <div className="Editor">
      <input
        ref={contentRef}
        value={content}
        onKeyDown={onKeydown}
        onChange={onChangeContent}
        placeholder="새로운 Todo..."
      />
      <button onClick={onSubmit}>추가</button>
    </div>
  );
};

export default Editor;
```

```jsx
// List.jsx

import "./List.css";
import TodoItem from "./TodoItem";
import { useState, useMemo, useContext } from "react";
import { TodoStateContext } from "../App";

const List = () => {
  const todos = useContext(TodoStateContext); //App.jsx에서 todos라는 state를 value로 그대로 전달해서 todos는 더이상 객체가 X

  const [search, setSearch] = useState("");

  const onChangeSearch = (e) => {
    setSearch(e.target.value);
  };

  const getFilteredData = () => {
    if (search === "") {
      return todos;
    }
    return todos.filter((todo) =>
      todo.content.toLowerCase().includes(search.toLowerCase())
    );
  };

  const filteredTodos = getFilteredData();

  const { totalCount, doneCount, notDoneCount } = useMemo(() => {
    console.log("getAnalyzeData 호출!");
    const totalCount = todos.length;
    const doneCount = todos.filter((todo) => todo.isDone).length;
    const notDoneCount = totalCount - doneCount;

    return {
      totalCount,
      doneCount,
      notDoneCount,
    };
  }, [todos]);
  // 의존성 배열 : deps

  // const {totalCount, doneCount, notDoneCount} =  getAnalyizedDate(); //구조분해할당

  return (
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
        {filteredTodos.map((todo) => {
          // 리스트로 렌더링하기
          return <TodoItem key={todo.id} {...todo} />;
        })}
      </div>
    </div>
  );
};

export default List;
```

```jsx
//TodoItem.jsx

import "./TodoItem.css";
import { memo, useContext } from "react";
import { TodoDispatchContext } from "../App";

const TodoItem = ({ id, isDone, content, date }) => {
  const { onUpdate, onDelete } = useContext(TodoDispatchContext);

  const onChangeCheckbox = () => {
    onUpdate(id);
  };

  const onClickDeleteButton = () => {
    onDelete(id);
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
      <button onClick={onClickDeleteButton}>삭제</button>
    </div>
  );
};

// // 고차 컴포넌트 (HOC)
// export default memo(TodoItem, (prevProps, nextProps)=>{
//     // 반환값에 따라, Props가 바뀌었는지 안 바뀌었는지 판단
//     // T->Props 바뀌지 X - > 리렌더링 X
//     // F - > Props 바뀜 -> 리렌더링 O

//     if (prevProps.id !== nextProps.is) return false;
//     if (prevProps.isDone !== nextProps.isDone) return false;
//     if (prevProps.content !== nextProps.content) return false;
//     if (prevProps.date !== nextProps.date) return false;

//     return true;
// });

export default memo(TodoItem);
```

# ch12. 프로젝트3 : 감정 일기장

## 1. 감정 일기장 소개

**감정 일기장**

= 일기 작성 서비스

= 감정까지 함께 기록 할 수 있음

- 새로운 일기를 작성하는 페이지
  - /new 라는 경로를 가짐
  - 여러 페이지로 이루어짐
  ![Untitled](ch12%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B33%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%8C%E1%85%A5%E1%86%BC%20%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%80%E1%85%B5%E1%84%8C%E1%85%A1%E1%86%BC%205d8774f911d34398a894ae81ca331f4c/Untitled.png)

**[ 이 강의에서 배울 수 있는 것들]**

- 외부 폰트 사용법
- 이미지 사용법 (+최적화)
- 다양한 페이지 제공하는 법
- 공통 컴포넌트(자주 쓰이는 것들)로 UI 요소 모듈화
- 복잡한 데이터 다루는 방법
- 리액트 앱 실제로 배포하는 법

## 2. 페이지 라우팅

= 경로에 따라 알맞은 페이지를 렌더링 하는 과정

ex) /new → new 페이지 렌더링

![Untitled](ch12%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B33%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%8C%E1%85%A5%E1%86%BC%20%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%80%E1%85%B5%E1%84%8C%E1%85%A1%E1%86%BC%205d8774f911d34398a894ae81ca331f4c/Untitled%201.png)

- Multi Page Application (MPA)
  = 애초에 서버가 여러 개의 페이지를 가지고 있음
  많은 서비스가 사용하는 전통적인 방식 (직관적이어서)
  → **but, React.js는 이 방식 X (빠르고 쾌적한 이동 제공X)**
  - 단점 : 페이지 이동 비효율적, 다수의 사용자 접속시, 서버 부하 심해짐
- 서버 사이드 렌더링 = 이미 완성되어있는 페이지 응답하는 방식

→ 대다수의 서버가 MPA 방식으로 다수의 웹페이지 보유하고 있는데 브라우저가 요청하면

서버 사이드 렌더링 방식으로 이미 만들어진 페이지를 응답한다.

![Untitled](ch12%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B33%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%8C%E1%85%A5%E1%86%BC%20%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%80%E1%85%B5%E1%84%8C%E1%85%A1%E1%86%BC%205d8774f911d34398a894ae81ca331f4c/Untitled%202.png)

그렇다면 React.js는?

**SPA(Single Page Application)** 사용함!

- 클라이언트 사이드 렌더링 (↔ 서버 사이드 렌더링)
  = 브라우저에서 직접 JS 실행해서 화면에 렌더링하도록 하는 것

![Untitled](ch12%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B33%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%8C%E1%85%A5%E1%86%BC%20%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%80%E1%85%B5%E1%84%8C%E1%85%A1%E1%86%BC%205d8774f911d34398a894ae81ca331f4c/Untitled%203.png)

![Untitled](ch12%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B33%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%8C%E1%85%A5%E1%86%BC%20%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%80%E1%85%B5%E1%84%8C%E1%85%A1%E1%86%BC%205d8774f911d34398a894ae81ca331f4c/Untitled%204.png)

## 3. 페이지 라우팅 - 라우팅 설정하기

- React Router = npmjs.com에 등록되어있는 라이브러리
                       대다수의 리액트 앱이 사용하고 있는 대표적 라이브러리

+리액트에선 모든 게 컴포넌트로 나눠지기 때문에 페이지도 나눠짐

- 주의 사항
  - 라우츠 컴포넌트 안에는 라우트만 들어갈 수 있다
  - 라우츠 컴포넌트 바깥에 있는 요소들은 페이지 라우팅과는 상관없이
    모든 페이지에 동일하게 렌더링

```jsx
// App.jsx

import "./App.css";
import { Routes, Route } from "react-router-dom";
import Home from "./pages/Home";
import Diary from "./pages/Diary";
import New from "./pages/New";
import Notfound from "./pages/Notfound";

// 1. "/" : 모든 일기를 조회하는 Home 페이지
// 2. "/new" : 새로운 일기를 작성하는 New 페이지
// 3. "/diary" : 일기를 상세히 조회하는 Diary 페이지
function App() {
  return (
    <>
      <div>Hello</div>
      <Routes>
        <Route path="/" element={<Home />} /> // "/" 경로로 이동했을 때
        element값이 렌더링되도록 하기
        <Route path="/new" element={<New />} />
        <Route path="/diary" element={<Diary />} />
        <Route path="*" element={<Notfound />} />
      </Routes>
    </>
  );
}

export default App;
```

```jsx
// main.jsx

import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";
import "./index.css";
import { BrowserRouter } from "react-router-dom";

//<BrowserRouter>는 browser의 현재 주소를 저장하고, 감지하는 역
// <BrowserRouter로 App 컴포넌트 감싸야 함!
ReactDOM.createRoot(document.getElementById("root")).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```

```jsx
// Home.jsx

const Home = () => {
  return <div>Home</div>;
};

export default Home;
```

```jsx
// Notfound.jsx

const Notfound = () => {
  return <div>잘못된 페이지입니다.</div>;
};

export default Notfound;
```

## 4. 페이지 라우팅 - 페이지 이동

```jsx
// App.jsx

import "./App.css";
import { Routes, Route, Link, useNavigate } from "react-router-dom";
import Home from "./pages/Home";
import Diary from "./pages/Diary";
import New from "./pages/New";
import Notfound from "./pages/Notfound";

// 1. "/" : 모든 일기를 조회하는 Home 페이지
// 2. "/new" : 새로운 일기를 작성하는 New 페이지
// 3. "/diary" : 일기를 상세히 조회하는 Diary 페이지
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
      <button>New 페이지로 이동</button>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/new" element={<New />} />
        <Route path="/diary" element={<Diary />} />
        <Route path="*" element={<Notfound />} />
      </Routes>
    </>
  );
}

export default App;
```

## 5. 페이지 라우팅 - 동적 경로

- 동적 경로 = 동적인 데이터 포함하고 있는 경로
  - URL Parameter = /뒤에 아이템의 id 명시
  - Query String = ? 뒤에 변수명과 값

```jsx
// App.jsx

import "./App.css";
import { Routes, Route, Link, useNavigate } from "react-router-dom";
import Home from "./pages/Home";
import Diary from "./pages/Diary";
import New from "./pages/New";
import Notfound from "./pages/Notfound";

// 1. "/" : 모든 일기를 조회하는 Home 페이지
// 2. "/new" : 새로운 일기를 작성하는 New 페이지
// 3. "/diary" : 일기를 상세히 조회하는 Diary 페이지
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
      <button>New 페이지로 이동</button>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/new" element={<New />} />
        <Route path="/diary" element={<Diary />} />
        <Route path="*" element={<Notfound />} />
      </Routes>
    </>
  );
}

export default App;
```

```jsx
// Diary.jsx

import { useSearchParams } from "react-router-dom";

const Diary = () => {
  const [params, setParams] = useSearchParmas();
  console.log(params.get("value"));

  return <div>Diary</div>;
};

export default Diary;
```

-

</br>

### 질문

페이지 ch10부터 페이지에 아무것도 출력이 안 되었다..
이유가 뭔지 계속 찾아봐야할 것 같다..
