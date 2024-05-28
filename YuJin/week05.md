# 3주차

**강의**
[인프런] - 한입 크기로 잘라머는 리액트(React.js) : 기초부터 실전까지
(https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8)

### 범위

섹션 12

- [x] 12.  프로젝트3. 감정 일기장 5강

---

</br>

### 학습 내용

# Ch.12 프로젝트3. 감정 일기장

### 페이지 라우팅(Page Routing)

페이지 라우팅

: 경로에 따라 알맞은 페이지를 렌더링 하는 과정

ex) /new → new 페이지 렌더링

**Multi Page Applicaiton (MPA)**

: 서버가 여러개 페이지를 가지고 있음(리엑트는 이 방식을 따르지 않음)

- 단점
    - 페이지 이동이 쾌적하지 못함
    - 다수의 사용자 접속시 서버의 부하가 심해짐

![Untitled](Ch%2012%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B33%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%8C%E1%85%A5%E1%86%BC%20%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%80%E1%85%B5%E1%84%8C%E1%85%A1%E1%86%BC%2073557e06bc8d42b4a2352518ef940d97/Untitled.png)

**React는 SPA 방식을 사용!**

**Single Page Application (SPA)**

- 페이지 이동이 매끄럽고 효율적임
- 다수의 사용자가 접속해도 크게 상관 없음

```jsx
import { useState } from 'react'
import './App.css'
import { Route, Routes, Link, useNavigate } from 'react-router-dom'
import Home from './pages/Home'
import Diary from './pages/Diary'
import New from './pages/New'
import NotFound from './pages/NotFound'

// 1. "/" : 모든 일기를 조회하는 Home 페이지
// 2. "/new" : 새로운 일기를 작성하는 New 페이지
// 3. "/diary" : 일기를 상세히 조회하는 Diary 페이지 

function App() {

  const nav = useNavigate();

  return (
    <Routes>
      <Route path='/' element={<Home/>}/>
      <Route path='/new' element={<New/>}/>
      <Route path='/diary/:id' element={<Diary/>}/>
      <Route path='*' element={<NotFound/>}/> 
    </Routes>
  )
  // path의 *은 switch문의 default와 같은 역할 지정한 path가 아니면 * 페이지를 보여줌
  // 내부 링크는 새로고침이 되지 않는 Link 사용하는 게 좋음
  // 조건에 따라 이동할 경우에는 useNavigate 사용
}

export default App
```

### 동적 경로

동적 경로

: 동적인 데이터를 포함하고 있는 경로 

![Untitled](Ch%2012%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B33%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%8C%E1%85%A5%E1%86%BC%20%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%80%E1%85%B5%E1%84%8C%E1%85%A1%E1%86%BC%2073557e06bc8d42b4a2352518ef940d97/Untitled%201.png)

**URL Parameter 사용 예시**

```jsx
//App.jsx의 <Routes> 태그 안에 루트 설정시 param 지정
<Route path='/diary/:id' element={<Diary/>}/>
```

```jsx
import { useParams } from "react-router-dom";

//useParams 사용해서 parameter 받아오기

const Diary = () => {

    const params = useParams();
    
    return <div>Diary</div>
}

export default Diary;
```

**Query String 사용 예시**

```jsx
import { useSearchParams } from "react-router-dom";

const Home = () => {
    const [params, setparams] = useSearchParams();
    //params로 현재 parameter의 값을 가져오고
    // setParams로 parameter의 값을 변경할 수 있음 
    
    return <div>Home</div>
}

export default Home;
```

### 폰트, 이미지, 레이아웃 설정하기

**public 폴더가 아닌 asset 폴더에 이미지를 넣고 Import해서 사용 하는 이유**

```jsx
    // assect 폴더에 넣어서 import 하고 사용
    <img src={emotion1}/>
```

차이는 vite의 이미지 최적화 기능이다! 

이미지 주소가 데이터 URI로 되어 있고, 한 번 불러오면 다시는 불러 오지 않는다(최적화)

```jsx
 // public 폴더에 넣어서 src로 가져와서 사용
    <img src={'./emtion1.png'}/>
```

새로 고침 할 때마다 매번 불러온다

**but,, 이미지가 많이 필요한 경우는 public 폴더에 저장하는 게 좋을 수 있다(메모리 부하 이슈)**

**따로 파일을 만들어 더 깔끔하게 사용하기**

src안에 util 폴더를 만들어 get-emotion-images.js 파일을 작성하여 이미지 로드를 따로 관리한다. 

```jsx
import emotion1 from './../assets/emotion1.png';
import emotion2 from './../assets/emotion2.png';
import emotion3 from './../assets/emotion3.png';
import emotion4 from './../assets/emotion4.png';
import emotion5 from './../assets/emotion5.png';

export function getEmotionImage(emotionId){
    switch(emotionId){
        case 1: return emotion1;
        case 2: return emotion2;
        case 3: return emotion3;
        case 4: return emotion4;
        case 5: return emotion5;
        default : return null;
    }
}

```

```jsx
      <div>
      <img src={getEmotionImage(1)}/>
      </div>
```

### 공통 컴포넌트 구현하기

<aside>
💡 **화면에 공통으로 쓰일 Header와 Button 컴포넌트 구현하기**

</aside>

- Header

```jsx
import './Header.css'

const Header = ({title, leftChild, rightChild})=>{
    return (
        <hedaer className="Header">
            <div className='header_left'>{leftChild}</div>
            <div className='header_center'>{title}</div>
            <div className='header_right'>{rightChild}</div>
        </hedaer>
    );
    // Header의 왼쪽, 가운데, 오른쪽 나누기
};

export default Header;
```

```css
.Header{
    display: flex;
    align-items: center;
    padding: 20px 0px;
    border-bottom: 1px solid rgb(226,226,226);
}

.Header > div{
    display: flex;

}

.Header .header_center{
    width: 50%;
    font-size: 25px;
    justify-content: center;
}

.Header .header_left{
    width: 25%;
    justify-content: flex-start;
}

.Header .header_right{
    width: 25%;
    justify-content: flex-end;
}
```

- Button

```jsx
import "./Button.css"

const Button = ({text,type,onClick})=>{
    return(
        <button onClick={onClick} 
        className={`Button Button_${type}`}>{text}</button>
    )
    // 버튼 타입별로 다른 스타일 적용 되도록 ClassName 설정 
};

export default Button;
```

```css
.Button{
    background-color: rgb(236,236,236);
    cursor: pointer;
    border:none;
    border-radius: 5px;
    padding: 10px 20px;
    font-size: 18px;
    white-space: nowrap;
}

.Button_POSITIVE{
    background-color: rgb(100,201,100);
    color: white;
}

.Button_NEGATIVE{
    background-color: rgb(253,86,95);
    color:white
}
```

### 일기 관리 기능 구현하기

<aside>
💡 **일기 생성, 수정, 삭제 기능 만들기**

</aside>

```jsx
function reducer(state, action){
  switch(action.type){
    case 'CREATE':
      return [action.data, ...state];
    case 'UPDATE':
      return state.map((item)=>
        String(item.id) === String(action.data.id)? 
      action.data:item);
    case 'DELETE':
      return state.filter((item)=>String(item.id)!==String(action.id));
    default:
      return state;
  }
}

const DiaryStateContext = createContext();
const DiaryDispatchContext = createContext();

function App() {
  const [data, dispatch]  = useReducer(reducer, mockData);
  const IdRef = useRef(3);

  //새로운 일기 추가
  const onCreate =(createDate, emotionId, content) =>{
    dispatch(
      {
        type: "CREATE",
        data: {
          id: IdRef.current++,
          createDate,
          emotionId,
          content,
        }
      }
    )

  }
  // 기존 일기 수정
  const onUpdate = (id, createDate, emotionId, content) =>{
    dispatch({
      type:"UPDATE",
      data:{
        id,
        createDate,
        emotionId,
        content,
      }
    })
  }

  // 기존 일기 삭제
  const onDelete = (id)=>{
    dispatch({
      type:"DELETE",
      id
    })
  }

```

**useReducer로 data를 관리하고, context에 저장해서 사용**

### Home 페이지 구현

<aside>
💡 **Home의 Header, ,DiaryList 구현하기**

</aside>

**Header**

```jsx
import './Header.css'

const Header = ({title, leftChild, rightChild})=>{
    return (
        <header className="Header">
            <div className='header_left'>{leftChild}</div>
            <div className='header_center'>{title}</div>
            <div className='header_right'>{rightChild}</div>
        </header>
    );
};

export default Header;
```

**DiaryList**

<aside>
💡 **DiaryList에서 menu와 list로 나누어 구현하기
list에 들어갈 diary는 DiaryItem으로 따로 구현**

</aside>

**날짜 최신순 오래된순 솔팅 기능 구현**

**DiaryList.jsx**

```jsx
import "./DiaryList.css";
import Button from "./Button";
import DiaryItem from "./DiaryItem";
import { useNavigate } from "react-router-dom";
import { useState } from "react";

const DiaryList = ({ data }) => {
  const nav = useNavigate();
  // 최신순으로 기본값 설정
  const [sortType, setSortType] = useState("latest");

  const onChangeSortType = (e) => {
    setSortType(e.target.value);
  };

  const getSortedData = () => {
    // 원본 배열은 두고 새로운 배열 수정
    return data.toSorted((a, b) => {
      if (sortType === "oldest") {
        return Number(a.createdDate) - Number(b.createdDate);
      } else {
        return Number(b.createdDate) - Number(a.createdDate);
      }
    });
  };

  const sortedData = getSortedData();

  return (
    <div className="DiaryList">
      <div className="menu_bar">
        <select value={sortType} onChange={onChangeSortType}>
          <option value={"latest"}>최신순</option>
          <option value={"oldest"}>오래된 순</option>
        </select>
        <Button
          onClick={() => nav("/new")}
          text={"새 일기 쓰기"}
          type={"POSITIVE"}
        />
      </div>
      <div className="list_wrapper">
        {sortedData.map((item) => (
          <DiaryItem key={item.id} {...item} />
        ))}
      </div>
    </div>
  );
};

export default DiaryList;
```

**DiaryItem.jsx**

```jsx
import "./DiaryItem.css"
import { useNavigate } from "react-router-dom";
import {getEmotionImage} from "../util/get-emtion-image"
import Button from "./Button";

const DiaryItem = ({ id, emotionId, createdDate, content }) => {
    const nav = useNavigate();
  
    const goDiaryPage = () => {
      nav(`/diary/${id}`);
    };
  
    const goEditPage = () => {
      nav(`/edit/${id}`);
    };
  
    return (
      <div className="DiaryItem">
        <div
          onClick={goDiaryPage}
          className={`img_section img_section_${emotionId}`}
        >
          <img src={getEmotionImage(emotionId)} />
        </div>
        <div onClick={goDiaryPage} className="info_section">
          <div className="created_date">
            {new Date(createdDate).toLocaleDateString()}
          </div>
          <div className="content">{content}</div>
        </div>
        <div className="button_section">
          <Button onClick={goEditPage} text={"수정하기"} />
        </div>
      </div>
    );
  };
  
  export default DiaryItem;
```

**해당 월의 일기만 보이도록 필터링**

**Home.jsx**

```jsx
const getMonthlyData = (pivotDate, data) => {
    const beginTime = new Date(
      //해달월의 1일의 0시 0분 0초
      pivotDate.getFullYear(),
      pivotDate.getMonth(),
      1,
      0,
      0,
      0
    ).getTime();
  
    const endTime = new Date(
      pivotDate.getFullYear(),
      pivotDate.getMonth() + 1,
      // 이전 달의 마지막날 23시 59분 59초
      0,
      23,
      59,
      59
    ).getTime();
  
    return data.filter(
      (item) =>
        beginTime <= item.createdDate && item.createdDate <= endTime
    );
  };

const Home = () => {
    const data = useContext(DiaryStateContext);
    const [pivotDate, setPivotDate] = useState(new Date());

    //이번달 일기만 보이도록 필터링
    const monthlyData = getMonthlyData(pivotDate,data);

    const onIncreaseMonth =()=>{
        //기존 pivotDate와 연도는 동일하지만 한달후
        setPivotDate(new Date(pivotDate.getFullYear(),pivotDate.getMonth()+1));

    };
    const onDecreaseMonth=()=>{
        //기존 pivotDate와 연도는 동일하지만 한달전
        setPivotDate(new Date(pivotDate.getFullYear(),pivotDate.getMonth()-1));

    
    }
    
    return (
        <div>
            <Header title={`${pivotDate.getFullYear()}년 ${pivotDate.getMonth()+1}월`}
            leftChild={<Button onClick={onDecreaseMonth} text="<"/>}
            rightChild={<Button onClick={onIncreaseMonth} text=">"/>}/>
            <DiaryList data={monthlyData}/>
        </div>
    )
}

export default Home;
```

### New 페이지 구현

<aside>
💡 **Header, Editor, EmotionItem 컴포넌트로 구현**

</aside>

**Header**

**New.jsx**

```jsx
      <Header
        title={"새 일기 쓰기"}
        leftChild={
          <Button onClick={() => nav(-1)} text={"< 뒤로 가기"} />
        }
      />
```

**Editor**

**New.jsx**

```jsx
  const onSubmit = (input) => {
    onCreate(
      input.createdDate.getTime(),
      input.emotionId,
      input.content
    );
    //제출시 홈으로 이동, 뒤로가기 방지
    nav("/", { replace: true });
  };
  
  // return 안에
  <Editor onSubmit={onSubmit} />
```

 **Editor.jsx**

```jsx
import "./Editor.css";
import EmotionItem from "./EmotionItem";
import Button from "./Button";
import { useState,useEffect } from "react";
import { useNavigate } from "react-router-dom";
import { emotionList } from "../util/constants";
import { getStringedDate } from "../util/get-stringed-date";
  
  const Editor = ({ initData, onSubmit }) => {
    const [input, setInput] = useState({
      createdDate: new Date(),
      emotionId: 3,
      content: "",
    });
    const nav = useNavigate();
  
    const onChangeInput = (e) => {
      let name = e.target.name;
      let value = e.target.value;
  
      if (name === "createdDate") {
        value = new Date(value);
      }
  
      setInput({
        ...input,
        [name]: value,
      });
    };

    useEffect(() => {
        if (initData) {
          setInput({
            ...initData,
            createdDate: new Date(Number(initData.createdDate)),
          });
        }
      }, [initData]);
  
    const onSubmitButtonClick = () => {
      onSubmit(input);
    };
  
    return (
      <div className="Editor">
        <section className="date_section">
          <h4>오늘의 날짜</h4>
          <input
            name="createdDate"
            onChange={onChangeInput}
            value={getStringedDate(input.createdDate)}
            type="date"
          />
        </section>
        <section className="emotion_section">
          <h4>오늘의 감정</h4>
          <div className="emotion_list_wrapper">
            {emotionList.map((item) => (
              <EmotionItem
                onClick={() =>
                  onChangeInput({
                    target: {
                      name: "emotionId",
                      value: item.emotionId,
                    },
                  })
                }
                key={item.emotionId}
                {...item}
                isSelected={item.emotionId === input.emotionId}
              />
            ))}
          </div>
        </section>
        <section className="content_section">
          <h4>오늘의 일기</h4>
          <textarea
            name="content"
            onChange={onChangeInput}
            placeholder="오늘은 어땠나요?"
          />
        </section>
        <section className="button_section">
          <Button onClick={() => nav(-1)} text={"취소하기"} />
          <Button
            onClick={onSubmitButtonClick}
            text={"작성완료"}
            type={"POSITIVE"}
          />
        </section>
      </div>
    );
  };
  
  export default Editor;
```

**EmotionItem**

**EmotionItem.jsx**

```jsx
import "./EmotionItem.css";
import { getEmotionImage } from "../util/get-emtion-image";
const EmotionItem = ({ emotionId, emotionName, isSelected, onClick }) => {
  return (
    <div
    onClick={onClick}
    className={`EmotionItem ${
        isSelected ? `EmotionItem_on_${emotionId}` : ""
      }`}
    >
      <img className="emotion_img" src={getEmotionImage(emotionId)} />
      <div className="emotion_name">{emotionName}</div>
    </div>
  );
};

export default EmotionItem;
```

### Edit 페이지 구현

<aside>
💡 **Header, Editor, EmotionItem 컴포넌트로 구현**

</aside>

**Header**

**Edit.jsx**

```jsx
 <Header
          title={"일기 수정하기"}
          leftChild={
            <Button onClick={() => nav(-1)} text={"< 뒤로 가기"} />
          }
          rightChild={
            <Button
              onClick={onClickDelete}
              text={"삭제하기"}
              type={"NEGATIVE"}
            />
          }
```

**Editor**

**Edit.jsx**

```jsx
    const params = useParams();
    const nav = useNavigate();
    const { onDelete, onUpdate } = useContext(DiaryDispatchContext);
    const curDiaryItem = useDiary(params.id);
    usePageTitle('일기 수정하기')
  
    const onClickDelete = () => {
      if (
        //팝업창 띄우기
        window.confirm("일기를 정말 삭제할까요? 다시 복구되지 않아요!")
      ) {
        // 일기 삭제 로직
        onDelete(params.id);
        nav("/", { replace: true });
      }
    };
  
    const onSubmit = (input) => {
      if (window.confirm("일기를 정말 수정할까요?")) {
        onUpdate(
          params.id,
          input.createdDate.getTime(),
          input.emotionId,
          input.content
        );
        nav("/", { replace: true });
      }
    };
    
    //return 안에
      <Editor initData={curDiaryItem} onSubmit={onSubmit} />
```

**EmotionItem**

**EmotionItem.jsx**

```jsx
import "./EmotionItem.css";
import { getEmotionImage } from "../util/get-emtion-image";
const EmotionItem = ({ emotionId, emotionName, isSelected, onClick }) => {
  return (
    <div
    onClick={onClick}
    className={`EmotionItem ${
        isSelected ? `EmotionItem_on_${emotionId}` : ""
      }`}
    >
      <img className="emotion_img" src={getEmotionImage(emotionId)} />
      <div className="emotion_name">{emotionName}</div>
    </div>
  );
};

export default EmotionItem;
```

### Diary 페이지 구현

<aside>
💡 **Header, Viewer 컴포넌트로 구현**

</aside>

**Header**

```jsx
      <Header
        title={`${title} 기록`}
        leftChild={
          <Button onClick={() => nav(-1)} text={"< 뒤로 가기"} />
        }
        rightChild={
          <Button
            onClick={() => nav(`/edit/${params.id}`)}
            text={"수정하기"}
          />
        }
      />
```

**Viewer**

**Viewer.jsx**

```jsx
import "./Viewer.css";
import { getEmotionImage } from "../util/get-emtion-image";
import { emotionList } from "../util/constants";

const Viewer = ({ emotionId, content }) => {
  const emotionItem = emotionList.find(
    (item) => String(item.emotionId) === String(emotionId)
  );

  return (
    <div className="Viewer">
      <section className="img_section">
        <h4>오늘의 감정</h4>
        <div
          className={`emotion_img_wrapper emotion_img_wrapper_${emotionId}`}
        >
          <img src={getEmotionImage(emotionId)} />
          <div>{emotionItem.emotionName}</div>
        </div>
      </section>
      <section className="content_section">
        <h4>오늘의 일기</h4>
        <div className="content_wrapper">
          <p>{content}</p>
        </div>
      </section>
    </div>
  );
};

export default Viewer;
```

**Diary.jsx**

```jsx
  const params = useParams();
  const nav = useNavigate();
  usePageTitle(`${params.id}번 일기`);

  const curDiaryItem = useDiary(params.id);

  if (!curDiaryItem) {
    return <div>데이터 로딩중...!</div>;
  }

  const { createdDate, emotionId, content } = curDiaryItem;
  const title = getStringedDate(new Date(createdDate));
  
  //return 내부
   <Viewer emotionId={emotionId} content={content} />

```

# 배포

### 웹 스토리지(Web Storage)

우리가 추가한 일기 데이터는 React Storage에 저장돼서 새로고침 시 초기화

→ 외부 데이터 베이스에 저장해서 데이터 유지

![Untitled](%E1%84%87%E1%85%A2%E1%84%91%E1%85%A9%20455ef6fa2df94e2993fcc32f4326a596/Untitled.png)

![Untitled](%E1%84%87%E1%85%A2%E1%84%91%E1%85%A9%20455ef6fa2df94e2993fcc32f4326a596/Untitled%201.png)

local storage 사용

![Untitled](%E1%84%87%E1%85%A2%E1%84%91%E1%85%A9%20455ef6fa2df94e2993fcc32f4326a596/Untitled%202.png)

> 값 저장

```jsx

  localStorage.setItem("test","hello");
  //원시형태로만 전달 가능, JSON.stringfy사용해서 문자열로 변경
  localStorage.setItem("person",JSON.stringify({name:"이유진"}));
```

> 값 꺼내와서 사용 

```jsx
  console.log(localStorage.getItem("test"));
  //JSON.parse 사용해서 객체 형태로 바꿔줌
  console.log(JSON.parse(localStorage.getItem("person")));
```

> 데이터 삭제

```jsx

 localStorage.removeItem("test");
```

## 배포 준비하기

![Untitled](%E1%84%87%E1%85%A2%E1%84%91%E1%85%A9%20455ef6fa2df94e2993fcc32f4326a596/Untitled%203.png)

### 페이지 타이틀 설정

**index.html 에서 title 변경**

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>감정 일기장</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>

```

**다른 페이지 타이틀도 변경**

```jsx
import { useEffect } from "react";

const usePageTitle = (title) =>{
    useEffect(()=>{
        const $title = document.getElementsByTagName("title")[0];
        $title.innerText = title;
    },[title]);
}

export default usePageTitle;
```

### Favicon 설정

**index.html 에서 icon 링크 변경**

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>감정 일기장</title>
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

### 오픈 그래프 태그 설정

**index.html 에서 meta 태그 설정**

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/favicon.ico" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1.0"
    />
    <title>감정 일기장</title>
    <meta property="og:title" content="감정 일기장" />
    <meta
      property="og:description"
      content="나만의 작은 감정 일기장"
    />
    <meta property="og:image" content="/thumbnail.png" />
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.jsx"></script>
  </body>
</html>
```

### 프로젝트 빌드(build)

![Untitled](%E1%84%87%E1%85%A2%E1%84%91%E1%85%A9%20455ef6fa2df94e2993fcc32f4326a596/Untitled%204.png)

### 배포

**다른 PC에 리액트 돌리기**

![Untitled](%E1%84%87%E1%85%A2%E1%84%91%E1%85%A9%20455ef6fa2df94e2993fcc32f4326a596/Untitled%205.png)

→ 비용, 방화벽 및 보안설정, 포트 포워딩, 무정전 전원 공급 등 신경 쓸 게 많음

**클라우드 서비스**

![Untitled](%E1%84%87%E1%85%A2%E1%84%91%E1%85%A9%20455ef6fa2df94e2993fcc32f4326a596/Untitled%206.png)

→ 편리함

![Untitled](%E1%84%87%E1%85%A2%E1%84%91%E1%85%A9%20455ef6fa2df94e2993fcc32f4326a596/Untitled%207.png)

1. vercel 회원가입
2. vercel login
    
    에러 등장..
    
    ![Untitled](%E1%84%87%E1%85%A2%E1%84%91%E1%85%A9%20455ef6fa2df94e2993fcc32f4326a596/Untitled%208.png)
    
    → 터미널에 `npm install -g vercel`  입력
    
    보안 이슈
    
    ![Untitled](%E1%84%87%E1%85%A2%E1%84%91%E1%85%A9%20455ef6fa2df94e2993fcc32f4326a596/Untitled%209.png)
    
    → 관리자 권한으로 실행한 power shall에 `Set-ExecutionPolicy RemoteSigned` 입력
    
3. vercel login
4. vercel 입력 후 이후 상황에 맞게 선택
    
    ![Untitled](%E1%84%87%E1%85%A2%E1%84%91%E1%85%A9%20455ef6fa2df94e2993fcc32f4326a596/Untitled%2010.png)
    
5. 배포 완료 
[https://emotion-diary-tvahafyni-leeyujins-projects.vercel.app](https://emotion-diary-tvahafyni-leeyujins-projects.vercel.app/)
