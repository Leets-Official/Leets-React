# 섹션 12. 프로젝트3. 감정 일기장

12.6) 폰트, 이미지, 레이아웃 설정하기

```jsx
import './App.css'
import { Routes, Route, Link, useNavigate } from 'react-router-dom'
import Home from './pages/Home'
import Diary from './pages/Diary'
import New from './pages/New'
import Notfound from './pages/Notfound'

import { getEmotionImage } from './Util/get-emtion-img'

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
      <img src={getEmotionImage(1)} />
      <img src={getEmotionImage(2)} />
      <img src={getEmotionImage(3)} />
      <img src={getEmotionImage(4)} />
      <img src={getEmotionImage(5)} />
    </div>
    
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
@font-face {
  font-family: "NanumPenScript";
  src: url("/public/NanumPenScript-Regular.ttf");
}

html, body {
  margin: 0px;
  width: 100%;
  background-color: rgb(246, 246, 246);
}

#root {
  background-color: white;
  max-width: 600px;
  width: 100%;
  margin: 0 auto;
  min-height: 100vh;
  height: 100%;
  box-shadow: rgba(100, 100, 100, 0.2) 0px 0px 29px 0px;
}
body * {
  font-family: "NanumPenScript"
}
```

```jsx
import emotion1 from './../assets/emotion1.png'
import emotion2 from './../assets/emotion2.png'
import emotion3 from './../assets/emotion3.png'
import emotion4 from './../assets/emotion4.png'
import emotion5 from './../assets/emotion5.png'

export function getEmotionImage (emotionId) {
    switch (emotionId) {
        case 1:
            return emotion1;
        case 2:
            return emotion2;
        case 3:
            return emotion3;
        case 4:
            return emotion4;
        case 5:
            return emotion5;
        default:
            return null;
    }
}
```

12.7) 공통 컴포넌트 구현하기

공통 컴포넌트를 먼저 구현하는 이유: 프로젝트 개발 순서는 사람마다 다름

```jsx
import './App.css'
import { Routes, Route, Link, useNavigate } from 'react-router-dom'
import Home from './pages/Home'
import Diary from './pages/Diary'
import New from './pages/New'
import Notfound from './pages/Notfound'
import Button from './components/Button'
import Header from './components/Header'

import { getEmotionImage } from './Util/get-emtion-img'

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
    <Header title={"Header"}
      leftChild={<Button text={"Left"}/>}
      rightChild={<Button text={"Right"}/>}
    />

    <Button
      text={"123"}
      type={"DEFAULT"}
      onClick={()=>{
        console.log("123번 버튼 클릭!")
      }}
      />
      <Button
      text={"123"}
      type={"POSITIVE"}
      onClick={()=>{
        console.log("123번 버튼 클릭!")
      }}
      />
      <Button
      text={"123"}
      type={"NEGATIVE"}
      onClick={()=>{
        console.log("123번 버튼 클릭!")
      }}
      />
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
import './Header.css'

const Header = ({title, leftChild, rightChild}) => {
    return (
    <header className="Header">
        <div className='header_left'>{leftChild}</div>
        <div className='header_center'>{title}</div>
        <div className='header_right'>{rightChild}</div>
    </header>
    )
}

export default Header;
```

```jsx
.Header {
    display: flex;
    align-items: center;

    padding: 20px 0px;
    border-bottom: 1px solid rgb(226,226,226);
}

.Header > div {
    display: flex;
}

.Header .header_center {
    width: 50%;
    font-size: 25px;
    justify-content: center;
}

.Header .header_left {
    width: 25%;
    justify-content: flex-start;
}

.Header .header_right {
    width: 25%;
    justify-content: flex-end;
}
```

```jsx
.Button{
    background-color: rgb(236,236,236);
    cursor: pointer;
    border: none;
    border-radius: 5px;
    padding: 10px 20px;
    font-size: 18px;
    white-space: nowrap;
}

.Button_POSITIVE {
    background-color: rgb(100, 201, 100);
    color: white;
}

.Button_NEGATIVE {
    background-color: rgb(253, 86, 95);
    color: white;
}
```

```jsx
import './Button.css'

const Button = ({ text, type,onClick }) => {
    return (
    <button 
        onClick={onClick} 
        className={`Button Button_${type}`}
    >
        {text}
    </button>
    )
}

export default Button
```

12.8) 일기 관리 기능 구현하기 1

감정 일기장 프로젝트 = “일기”라는 형태의 데이터를 관리하는 프로그램

home: 일기 리스트 렌더링

diary: 일기 상세 조회

new: 새로운 일기 작성

edit: 기존 일기 수정

```jsx
import './App.css'
import { useReducer } from 'react'
import { Routes, Route } from 'react-router-dom'
import Home from './pages/Home'
import Diary from './pages/Diary'
import New from './pages/New'
import Edit from './pages/Edit'
import Notfound from './pages/Notfound'

const mockData = [
  {
    id:1,
    createdData: new Date().getTime(),
    emotionId : 1,
    content: "1번 일기 내용",
  },
  {
    id:2,
    createdData: new Date().getTime(),
    emotionId : 2,
    content: "2번 일기 내용",
  },
]

function reducer(state, action){
  return state;
}

function App() {
  const [data, dispatch] = useReducer(reducer, mockData)
  return (
    <>
      <Routes>
        <Route path='/' element={<Home />} />
        <Route path='/new' element={<New />} />
        <Route path='/diary:id' element={<Diary />} />
        <Route path='/edit/:id' element={<Edit />} />
        <Route path='*' element={<Notfound />} />
    </Routes>
    </>
  )
}

export default App
```

```jsx
import { useParams } from "react-router-dom"

const Edit= ()=>{
    const params = useParams()
    return <div>{params.id}번 일기 수정페이지입니다</div>
}

export default Edit
```

12.9) 일기 관리 기능 구현하기 2

```jsx
import './App.css'
import { useReducer, useRef, createContext } from 'react'
import { Routes, Route } from 'react-router-dom'
import Home from './pages/Home'
import Diary from './pages/Diary'
import New from './pages/New'
import Edit from './pages/Edit'
import Notfound from './pages/Notfound'

const mockData = [
  {
    id:1,
    createdDate: new Date().getTime(),
    emotionId : 1,
    content: "1번 일기 내용",
  },
  {
    id:2,
    createdDate: new Date().getTime(),
    emotionId : 2,
    content: "2번 일기 내용",
  },
]

function reducer(state, action){
  switch(action.type){
    case 'CREATE':
      return [action.data, ...state];
    case 'UPDATE':
      return state.map((item)=>
        String(item.id) === String(action.data.id) 
          ? action.data 
          : item
      )
    case 'DELETE':
      return state.filter(
        (item)=> String(item.id) !== String(action.id)
    )
    default:
      return state;
  }
}

const DiaryStateContext = createContext()
const DiaryDispatchContext = createContext()

function App() {
  const [data, dispatch] = useReducer(reducer, mockData)
  const idRef = useRef(3)

  //새로운 일기 추가
  const onCreate = (createdDate, emotionId, content) => {
    dispatch({
      type:"CREATE",
      data: {
        id: idRef.current++,
        createdDate,
        emotionId,
        content,
      },
    })
  }
  //기존 일기 수정
  const onUpdate = (id, createdDate, emotionId, content) => {
    dispatch({
      type:"UPDATE",
      data : {
        id, createdDate, emotionId, content
      }
    })
  }

  //기존 일기 삭제
  const onDelete = (id) => {
    dispatch({
      type:"DELETE",
      id,
    })
  }

  return (
    <>
    <button onClick={() => {
      onCreate(new Date().getTime(), 1, "Hello")
    }}
    >
      일기 추가 테스트
    </button>

    <button onClick={()=>{
      onUpdate(1, new Date().getTime(), 3, "수정된 일기입니다")
    }}
    >
      일기 수정 테스트
    </button>

    <button onClick={() => {
      onDelete(1)
    }}>
      일기 삭제 테스트
    </button>

    <DiaryStateContext.Provider value={data}>
      <DiaryDispatchContext.Provider
        value={{
          onCreate,
          onUpdate,
          onDelete,
        }}
      >
        <Routes>
          <Route path='/' element={<Home />} />
          <Route path='/new' element={<New />} />
          <Route path='/diary:id' element={<Diary />} />
          <Route path='/edit/:id' element={<Edit />} />
          <Route path='*' element={<Notfound />} />
        </Routes>
      </DiaryDispatchContext.Provider>
    </DiaryStateContext.Provider>
    </>
  )
}

export default App
```

12.10) Home 페이지 구현하기 1. UI

Home 컴포넌트 - Header, DiaryList, DiaryItem 컴포넌트

```jsx
import Header from "../components/Header";
import Button from "../components/Button"
import DiaryList from "../components/DiaryList"

const Home = () => {    
    return <div>
        <Header title={"2024년 2월"}
            leftChild={<Button text={"<"}/>}
            rightChild={<Button text={">"} />}
        />
        <DiaryList />
    </div>;
}

export default Home;
```

```jsx
import './DiaryList.css'
import Button from "./Button"
import DiaryItem from './DiaryItem'

const DiaryList = () => {
    return (
    <div className="DiaryList">
        <div className="menu_bar">
            <select>
                <option value={"latest"}>최신순</option>
                <option value={"oldest"}>오래된 순</option>
            </select>
            <Button text={"새 일기 쓰기"} type={"POSITIVE"} />
        </div>
        <div className="list_wrapper">
            <DiaryItem />
        </div>
    </div>
    )
}

export default DiaryList
```

```jsx
import { getEmotionImage } from '../Util/get-emtion-img'
import Button from './Button'
import './DiaryItem.css'

const DiaryItem = () => {
    const emotionId = 1;

    return (
    <div className="DiaryItem">
        <div className={`img_section img_section_${emotionId}`}>
            <img src={getEmotionImage(1)} />
        </div>
        <div className="info_section">
            <div className='created_date'>
                {new Date().toLocaleDateString()}
            </div>
            <div className='content'>
                일기 컨텐츠
            </div>
        </div>
        <div className="button_section">
            <Button text={"수정하기"} />
        </div>
    </div>
    )
}

export default DiaryItem
```

```jsx
.DiaryItem {
    display: flex;
    gap: 15px;
    justify-content: space-between;

    padding: 15px 0px;
    border-bottom: 1px solid rgb(236,236,236);
}

.DiaryItem .img_section {
    min-width: 120px;
    height: 80px;

    display: flex;
    justify-content: center;
    cursor: pointer;

    border-radius: 5px;
}

.DiaryItem .img_section > img {
    width: 50%;
}

.DiaryItem .img_section_1 {
    background-color: rgb(100, 201, 100);
}

.DiaryItem .img_section_2 {
    background-color: rgb(157, 215, 114);
}

.DiaryItem .img_section_3 {
    background-color: rgb(253,206,23);
}

.DiaryItem .img_section_4 {
    background-color: rgb(253, 132, 70);
}
.DiaryItem .img_section_5 {
    background-color: rgb(253, 86, 95);
}

.DiaryItem .info_section {
    flex: 1;
    cursor: pointer;
}

.DiaryItem .info_section .created_date {
    font-weight: bold;
    font-size: 25px;
}

.DiaryItem .info_section .content {
    font-size: 18px;
}

.DiaryItem .button_section {
    min-width: 70px;
}
```

12.11) Home 페이지 구현하기 2. 기능

```jsx
import './DiaryList.css'
import Button from "./Button"
import DiaryItem from './DiaryItem'
import { useNavigate } from 'react-router-dom'
import { useState } from 'react'

const DiaryList = ({data}) => {
    const nav = useNavigate()
    const [sortType, setSortType ] = useState("latest")

    const onChangeSortType = (e) =>{
        setSortType(e.target.value)
    }

    const getSortedDate = () => {
        return data.toSorted((a,b)=>{
            if(sortType === 'oldest'){
                return Number(a.createdDate) - Number(b.createdDate)
            }else{
                return Number(b.createdDate) - Number(a.createdDate)
            }
        })
    }

    const sortedData = getSortedDate()

    return (
    <div className="DiaryList">
        <div className="menu_bar">
            <select onChange={onChangeSortType}>
                <option value={"latest"}>최신순</option>
                <option value={"oldest"}>오래된 순</option>
            </select>
            <Button 
                onClick={() => nav('/new')}
                text={"새 일기 쓰기"} 
                type={"POSITIVE"} 
            />
        </div>
        <div className="list_wrapper">
            {sortedData.map((item)=>(
                <DiaryItem key={item.id} {...item}/>
            ))}
        </div>
    </div>
    )
}

export default DiaryList
```

```jsx
import { useState,useContext } from 'react'
import { DiaryStateContext } from '../App';

import Header from "../components/Header";
import Button from "../components/Button"
import DiaryList from "../components/DiaryList"

const getMonthlyData =( pivotDate, data ) => {
    const beginTime = new Date(
        pivotDate.getFullYear(), 
        pivotDate.getMonth(),
        1,
        0,
        0,
        0
    ).getTime()

    const endTime = new Date(
        pivotDate.getFullYear(),
        pivotDate.getMonth() +1,
        0,
        23,
        59,
        59
    ).getTime()

    return data.filter(
        (item) => 
            beginTime <= item.createdDate && item.createdDate <= endTime
    )
}

const Home = () => {
    const data = useContext(DiaryStateContext)
    const [pivotDate, setPivotDate] = useState(new Date())

    const monthlyData = getMonthlyData(pivotDate, data)

    const onIncreaseMonth = () => {
        setPivotDate(
            new Date(pivotDate.getFullYear(), pivotDate.getMonth()+1)
        )
    }

    const onDecreaseMonth = () => {
        setPivotDate(
            new Date(pivotDate.getFullYear(), pivotDate.getMonth()-1)
        )
    }

    return (
        <div>
            <Header 
                title={`${pivotDate.getFullYear()}년 ${pivotDate.getMonth()+1}월`}
                leftChild={<Button onClick={onDecreaseMonth} text={"<"}/>}
                rightChild={<Button onClick={onIncreaseMonth} text={">"} />}
            />
            <DiaryList data = {monthlyData} />
        </div>
    )
}

export default Home;
```

```jsx
import { getEmotionImage } from '../Util/get-emtion-img'
import Button from './Button'
import './DiaryItem.css'
import { useNavigate } from 'react-router-dom'

const DiaryItem = ({id, emotionId, createdDate, content}) => {
    const nav = useNavigate()

    return (
    <div className="DiaryItem">
        <div
            onClick={()=>nav(`/diary/${id}`)} 
            className={`img_section img_section_${emotionId}`}>
            <img src={getEmotionImage(emotionId)} />
        </div>
        <div 
            onClick={()=>nav(`/diary/${id}`)} 
            className="info_section">
            <div className='created_date'>
                {new Date(createdDate).toLocaleDateString()}
            </div>
            <div className='content'>
                {content}
            </div>
        </div>
        <div className="button_section">
            <Button 
                onClick={()=>nav(`/edit/${id}`)}
                text={"수정하기"} 
            />
        </div>
    </div>
    )
}

export default DiaryItem
```

```jsx
import './App.css'
import { useReducer, useRef, createContext } from 'react'
import { Routes, Route } from 'react-router-dom'
import Home from './pages/Home'
import Diary from './pages/Diary'
import New from './pages/New'
import Edit from './pages/Edit'
import Notfound from './pages/Notfound'

const mockData = [
  {
    id:1,
    createdDate: new Date("2024-05-19").getTime(),
    emotionId : 1,
    content: "1번 일기 내용",
  },
  {
    id:2,
    createdDate: new Date("2024-05-18").getTime(),
    emotionId : 2,
    content: "2번 일기 내용",
  },
  {
    id:3,
    createdDate: new Date("2024-04-25").getTime(),
    emotionId : 3,
    content: "3번 일기 내용",
  },
]

function reducer(state, action){
  switch(action.type){
    case 'CREATE':
      return [action.data, ...state];
    case 'UPDATE':
      return state.map((item)=>
        String(item.id) === String(action.data.id) 
          ? action.data 
          : item
      )
    case 'DELETE':
      return state.filter(
        (item)=> String(item.id) !== String(action.id)
    )
    default:
      return state;
  }
}

export const DiaryStateContext = createContext()
export const DiaryDispatchContext = createContext()

function App() {
  const [data, dispatch] = useReducer(reducer, mockData)
  const idRef = useRef(3)

  //새로운 일기 추가
  const onCreate = (createdDate, emotionId, content) => {
    dispatch({
      type:"CREATE",
      data: {
        id: idRef.current++,
        createdDate,
        emotionId,
        content,
      },
    })
  }
  //기존 일기 수정
  const onUpdate = (id, createdDate, emotionId, content) => {
    dispatch({
      type:"UPDATE",
      data : {
        id, createdDate, emotionId, content
      }
    })
  }

  //기존 일기 삭제
  const onDelete = (id) => {
    dispatch({
      type:"DELETE",
      id,
    })
  }

  return (
    <>
      <DiaryStateContext.Provider value={data}>
        <DiaryDispatchContext.Provider
          value={{
            onCreate,
            onUpdate,
            onDelete,
          }}
        >
          <Routes>
            <Route path='/' element={<Home />} />
            <Route path='/new' element={<New />} />
            <Route path='/diary:id' element={<Diary />} />
            <Route path='/edit/:id' element={<Edit />} />
            <Route path='*' element={<Notfound />} />
          </Routes>
        </DiaryDispatchContext.Provider>
      </DiaryStateContext.Provider>
    </>
  )
}

export default App
```

12.13) New 페이지 구현하기 1. UI

```jsx
import './Editor.css'
import EmotionItem from './EmotionItem'
import Button from './Button'

const emotionList = [
    {
        emotionId:1,
        emotionName:"완전 좋음"
    },
    {
        emotionId:2,
        emotionName:"좋음"
    },
    {
        emotionId:3,
        emotionName:"그럭저럭"
    },
    {
        emotionId:4,
        emotionName:"나쁨"
    },
    {
        emotionId:5,
        emotionName:"끔찍함"
    },
]

const Editor = () => {
    const emotionId = 1;

    return (
    <div className='Editor'>
        <section className='date_section'>
            <h4>오늘의 날짜</h4>
            <input type ="date" />
        </section>
        <section className='emotion_section'>
            <h4>오늘의 감정</h4>
            <div className='emotion_list_wrapper'>
                {emotionList.map((item)=> (
                    <EmotionItem 
                        key = {item.emotionId} 
                        {...item} 
                        isSelected={item.emotionId === emotionId}
                    />
                ))}
            </div>
        </section>
        <section className='content_section'>
            <h4>오늘의 일기</h4>
            <textarea placeholder='오늘은 어땠나요?'/>
        </section>
        <section className='button_section'>
            <Button text={"취소하기"} />
            <Button text={"작성완료"}/>
        </section>
    </div>
    )
}

export default Editor
```

```jsx
.Editor > section {
    margin-bottom: 40px;
}

.Editor > section >h4 {
    font-size: 22px;
    font-weight: bold;
}

.Editor > section >input,textarea {
    background-color: rgb(236,236,236);
    border: none;
    border-radius: 5px;
    font-size: 20px;
    padding: 10px 20px;
}

.Editor > section > textarea {
    padding: 20px;
    width: 100%;
    min-height: 200px;
    resize: vertical;
    box-sizing: border-box;
}

.Editor .emotion_section .emotion_list_wrapper {
    display: flex;
    justify-content: space-around;
    gap: 2%;
}

.Editor .button_section {
    display: flex;
    justify-content: space-between;
}
```

```jsx
import "./EmotionItem.css"
import {getEmotionImage} from '../Util/get-emtion-img'

const EmotionItem = ({emotionId, emotionName, isSelected}) => {
    return(
    <div className={`EmotionItem ${
        isSelected ? `EmotionItem_on_${emotionId}`: ""
        }`}
    >
        <img className='emtion_img' src={getEmotionImage(emotionId)} />
        <div className='emotion_name'>
            {emotionName}
        </div>
    </div>
    )
}

export default EmotionItem
```

```jsx
.EmotionItem {
    background-color: rgb(236,236,236);
    padding: 20px;
    border-radius: 5px;
    cursor: pointer;
    text-align: center;
}

.EmotionItem .emotion_img {
    width: 50%;
    margin-bottom: 10px;
}

.EmotionItem_on_1{
    color: white;
    background-color: rgb(100, 201, 100);
}

.EmotionItem_on_2{
    color: white;
    background-color: rgb(157, 215, 114);
}

.EmotionItem_on_3{
    color: white;
    background-color: rgb(253,206,23);
}

.EmotionItem_on_4{
    color: white;
    background-color: rgb(253, 132, 70);
}

.EmotionItem_on_5{
    color: white;
    background-color: rgb(253, 86, 95);
}
```

12.14) New 페이지 구현하기 2. 기능

```jsx
import Header from "../components/Header"
import Button from "../components/Button"
import Editor from "../components/Editor"
import { useNavigate } from "react-router-dom"
import { useContext } from "react"
import { DiaryDispatchContext } from "../App"

const New = () => {
    const {onCreate} = useContext(DiaryDispatchContext)
    const nav = useNavigate()

    const onSubmit = (input) => {
        onCreate(
            input.createdDate.getTime(), 
            input.emotionId, 
            input.content
        )
        nav('/', {replace:true})
    }
    return(
        <div>
            <Header 
                title={"새 일기 쓰기"}
                leftChild={<Button 
                    onClick={()=>nav(-1)}
                    text={"< 뒤로 가기 "} 
                    />}
            />
            <Editor onSubmit={onSubmit}/>
        </div>
    )
}

export default New;
```

```jsx
import './Editor.css'
import EmotionItem from './EmotionItem'
import Button from './Button'
import { useState } from 'react'
import { useNavigate } from 'react-router-dom'

const emotionList = [
    {
        emotionId:1,
        emotionName:"완전 좋음"
    },
    {
        emotionId:2,
        emotionName:"좋음"
    },
    {
        emotionId:3,
        emotionName:"그럭저럭"
    },
    {
        emotionId:4,
        emotionName:"나쁨"
    },
    {
        emotionId:5,
        emotionName:"끔찍함"
    },
]

const getStringedDate = (targetDate) => {
    let year = targetDate.getFullYear()
    let month = targetDate.getMonth() +1
    let date = targetDate.getDate()

    if(month < 10){
        month = `0${month}`
    }
    if(date < 10){
        date = `0${date}`
    }

    return `${year}-${month}-${date}`
}

const Editor = ({onSubmit}) => {
    const [input, setInput] = useState({
        createdDate : new Date(),
        emotionId : 3,
        content:"",
    })
    const nav = useNavigate()

    const onChangeInput = (e) => {
        let name = e.target.name;
        let value = e.target.value;

        if(name === 'createdDate'){
            value = new Date(value)
        }

        setInput({
            ...input,
            [name] : value,

        })
    }

    const onClickSubmitButton = () => {
        onSubmit(input)
    }

    return (
    <div className='Editor'>
        <section className='date_section'>
            <h4>오늘의 날짜</h4>
            <input 
                name="createdDate"
                onChange={onChangeInput}
                value={getStringedDate(input.createdDate)} 
                type ="date" 
            />
        </section>
        <section className='emotion_section'>
            <h4>오늘의 감정</h4>
            <div className='emotion_list_wrapper'>
                {emotionList.map((item)=> (
                    <EmotionItem 
                    onClick={()=>onChangeInput({
                        target: {
                            name :"emotionId",
                            value : item.emotionId,
                        }
                    })}
                        key = {item.emotionId} 
                        {...item} 
                        isSelected={item.emotionId === input.emotionId}
                    />
                ))}
            </div>
        </section>
        <section className='content_section'>
            <h4>오늘의 일기</h4>
            <textarea 
            name = "content"
            value={input.content}
            onChange={onChangeInput}
            placeholder='오늘은 어땠나요?'/>
        </section>
        <section className='button_section'>
            <Button onClick={()=>nav(-1)} text={"취소하기"} />
            <Button 
                onClick={onClickSubmitButton}
                text={"작성완료"} 
                type={"POSITIVE"} />
        </section>
    </div>
    )
}

export default Editor
```

```jsx
import "./EmotionItem.css"
import {getEmotionImage} from '../Util/get-emtion-img'

const EmotionItem = ({
    emotionId, 
    emotionName, 
    isSelected, 
    onClick,
}) => {
    return(
    <div 
        onClick={onClick}
        className={`EmotionItem ${
        isSelected ? `EmotionItem_on_${emotionId}`: ""
        }`}
    >
        <img className='emtion_img' src={getEmotionImage(emotionId)} />
        <div className='emotion_name'>
            {emotionName}
        </div>
    </div>
    )
}

export default EmotionItem
```

12.15) Edit 페이지 구현하기

```jsx
import { useParams,useNavigate } from "react-router-dom"
import Header from "../components/Header"
import Button from "../components/Button"
import Editor from "../components/Editor"
import { useContext,useEffect,useState } from "react"
import { DiaryDispatchContext,DiaryStateContext } from "../App"

const Edit= ()=>{
    const params = useParams()
    const nav = useNavigate()
    const {onDelete, onUpdate} = useContext(DiaryDispatchContext)
    const data = useContext(DiaryStateContext)
    const [curDiaryItem, setCurDiaryItem] = useState()

    useEffect(()=>{
        const currentDiaryItem = data.find(
            (item)=>String(item.id) === String(params.id)
        )
    
        if(!currentDiaryItem){
            window.alert("존재하지 않는 일기입니다.")
            nav('/', {replace: true})
        }

        setCurDiaryItem(currentDiaryItem)
    },[params.id, data])

    const onClickDelete = () => {
        if(
            window.confirm("일기를 정말 삭제할까요? 다시 복구되지 않아요!")
        ) {
            onDelete(params.id)
            nav('/',{replace: true})
        }
    }

    const onSubmit = (input) => {
        if(
            window.confirm("일기를 정말 수정할까요?")
        ){
            onUpdate(
                params.id, 
                input.createdDate.getTime(), 
                input.emotionId, 
                input.content
            )
            nav('/',{replace: true})
        }
    }

    return <div>
        <Header 
            title = {"일기 수정하기"} 
            leftChild={
                <Button onClick={()=>nav(-1)} text = {"< 뒤로 가기"}/>
            } 
            rightChild={
                <Button 
                    onClick={onClickDelete} 
                    text = {"삭제하기"} 
                    type = {"NEGATIVE"}
                />
            }
        />
        <Editor initData={curDiaryItem} onSubmit={onSubmit} />
    </div>
}

export default Edit
```

```jsx
import './Editor.css'
import EmotionItem from './EmotionItem'
import Button from './Button'
import { useState,useEffect } from 'react'
import { useNavigate } from 'react-router-dom'

const emotionList = [
    {
        emotionId:1,
        emotionName:"완전 좋음"
    },
    {
        emotionId:2,
        emotionName:"좋음"
    },
    {
        emotionId:3,
        emotionName:"그럭저럭"
    },
    {
        emotionId:4,
        emotionName:"나쁨"
    },
    {
        emotionId:5,
        emotionName:"끔찍함"
    },
]

const getStringedDate = (targetDate) => {
    let year = targetDate.getFullYear()
    let month = targetDate.getMonth() +1
    let date = targetDate.getDate()

    if(month < 10){
        month = `0${month}`
    }
    if(date < 10){
        date = `0${date}`
    }

    return `${year}-${month}-${date}`
}

const Editor = ({initData, onSubmit}) => {
    const [input, setInput] = useState({
        createdDate : new Date(),
        emotionId : 3,
        content:"",
    })
    const nav = useNavigate()

    useEffect(()=>{
        if(initData){
            setInput({
                ...initData,
                createdDate : new Date(Number(initData.createdDate)),
            })
        }
    }, [initData])

    const onChangeInput = (e) => {
        let name = e.target.name;
        let value = e.target.value;

        if(name === 'createdDate'){
            value = new Date(value)
        }

        setInput({
            ...input,
            [name] : value,

        })
    }

    const onClickSubmitButton = () => {
        onSubmit(input)
    }

    return (
    <div className='Editor'>
        <section className='date_section'>
            <h4>오늘의 날짜</h4>
            <input 
                name="createdDate"
                onChange={onChangeInput}
                value={getStringedDate(input.createdDate)} 
                type ="date" 
            />
        </section>
        <section className='emotion_section'>
            <h4>오늘의 감정</h4>
            <div className='emotion_list_wrapper'>
                {emotionList.map((item)=> (
                    <EmotionItem 
                    onClick={()=>onChangeInput({
                        target: {
                            name :"emotionId",
                            value : item.emotionId,
                        }
                    })}
                        key = {item.emotionId} 
                        {...item} 
                        isSelected={item.emotionId === input.emotionId}
                    />
                ))}
            </div>
        </section>
        <section className='content_section'>
            <h4>오늘의 일기</h4>
            <textarea 
            name = "content"
            value={input.content}
            onChange={onChangeInput}
            placeholder='오늘은 어땠나요?'/>
        </section>
        <section className='button_section'>
            <Button onClick={()=>nav(-1)} text={"취소하기"} />
            <Button 
                onClick={onClickSubmitButton}
                text={"작성완료"} 
                type={"POSITIVE"} />
        </section>
    </div>
    )
}

export default Editor
```

12.16) Diary 페이지 구현하기

```jsx
import { useParams,useNavigate } from "react-router-dom";
import Header from "../components/Header"
import Button from "../components/Button"
import Viewer from "../components/Viewer";
import useDiary from "../hooks/useDiary";
import { getStringedDate } from "../Util/get-stringed-date";

const Diary = () => {
    const params = useParams();
    const nav = useNavigate()

    const curDiaryItem = useDiary(params.id)

    if (!curDiaryItem) {
        return <div>데이터 로딩중...!</div>
    }

    const { createdDate, emotionId, content} = curDiaryItem
    const title = getStringedDate(new Date(createdDate))

    return <div>
        <Header 
            title={`${title} 기록`} 
            leftChild={
                <Button onClick={()=>nav(-1)} text = {"< 뒤로 가기"} />
            }
            rightChild={
                <Button 
                    onClick={() => nav(`/edit/${params.id}`)} 
                    text = {"수정하기"} 
                />
            }
        />
        <Viewer emotionId={emotionId} content={content} />
    </div>;
}

export default Diary;
```

```jsx
export const getStringedDate = (targetDate) => {
    let year = targetDate.getFullYear()
    let month = targetDate.getMonth() +1
    let date = targetDate.getDate()

    if(month < 10){
        month = `0${month}`
    }
    if(date < 10){
        date = `0${date}`
    }

    return `${year}-${month}-${date}`
}
```

```jsx
import { useParams,useNavigate } from "react-router-dom"
import Header from "../components/Header"
import Button from "../components/Button"
import Editor from "../components/Editor"
import { useContext,useEffect,useState } from "react"
import { DiaryDispatchContext,DiaryStateContext } from "../App"
import useDiary from "../hooks/useDiary"

const Edit= ()=>{
    const params = useParams()
    const nav = useNavigate()
    const {onDelete, onUpdate} = useContext(DiaryDispatchContext)
    const curDiaryItem= useDiary(params.id)

    const onClickDelete = () => {
        if(
            window.confirm("일기를 정말 삭제할까요? 다시 복구되지 않아요!")
        ) {
            onDelete(params.id)
            nav('/',{replace: true})
        }
    }

    const onSubmit = (input) => {
        if(
            window.confirm("일기를 정말 수정할까요?")
        ){
            onUpdate(
                params.id, 
                input.createdDate.getTime(), 
                input.emotionId, 
                input.content
            )
            nav('/',{replace: true})
        }
    }

    return <div>
        <Header 
            title = {"일기 수정하기"} 
            leftChild={
                <Button onClick={()=>nav(-1)} text = {"< 뒤로 가기"}/>
            } 
            rightChild={
                <Button 
                    onClick={onClickDelete} 
                    text = {"삭제하기"} 
                    type = {"NEGATIVE"}
                />
            }
        />
        <Editor initData={curDiaryItem} onSubmit={onSubmit} />
    </div>
}

export default Edit
```

```jsx
import { useContext, useState,useEffect } from "react"
import { DiaryStateContext } from "../App"
import { useNavigate } from "react-router-dom"

const useDiary = (id) =>{
    const data = useContext(DiaryStateContext)
    const [curDiaryItem, setCurDiaryItem] = useState()
    const nav = useNavigate()

    useEffect(()=>{
        const currentDiaryItem = data.find(
            (item)=>String(item.id) === String(id)
        )
    
        if(!currentDiaryItem){
            window.alert("존재하지 않는 일기입니다.")
            nav('/', {replace: true})
        }

        setCurDiaryItem(currentDiaryItem)
    },[id, data])

    return curDiaryItem
}

export default useDiary
```

```jsx
import "./Viewer.css"
import { getEmotionImage} from "../Util/get-emtion-img"
import { emotionList } from "../Util/constants";

const Viewer = ( emotionId, content) => {

    const emotionItem = emotionList.find(
        (item) => String(item.emotionId) === String(emotionId)
    )

    return (
        <div className="Viewer">
            <section className="img_section">
                <h4>오늘의 감정</h4>
                <div className= {`emotion_img_wrapper emotion_img_wrapper_${emotionId}`}>
                    <img src = {getEmotionImage(emotionId)} />
                    <div>
                        {emotionItem.emotionName}
                    </div>
                </div>
            </section>
            <section className="content_section">
                <h4>오늘의 일기</h4>
                <div className="content_wrapper">
                    <p>{content}</p>
                </div>
            </section>
        </div>
    )
}

export default Viewer
```

```jsx
import './Editor.css'
import EmotionItem from './EmotionItem'
import Button from './Button'
import { useState,useEffect } from 'react'
import { useNavigate } from 'react-router-dom'
import { emotionList } from '../Util/constants'
import { getStringedDate } from '../Util/get-stringed-date'

const Editor = ({initData, onSubmit}) => {
    const [input, setInput] = useState({
        createdDate : new Date(),
        emotionId : 3,
        content:"",
    })
    const nav = useNavigate()

    useEffect(()=>{
        if(initData){
            setInput({
                ...initData,
                createdDate : new Date(Number(initData.createdDate)),
            })
        }
    }, [initData])

    const onChangeInput = (e) => {
        let name = e.target.name;
        let value = e.target.value;

        if(name === 'createdDate'){
            value = new Date(value)
        }

        setInput({
            ...input,
            [name] : value,

        })
    }

    const onClickSubmitButton = () => {
        onSubmit(input)
    }

    return (
    <div className='Editor'>
        <section className='date_section'>
            <h4>오늘의 날짜</h4>
            <input 
                name="createdDate"
                onChange={onChangeInput}
                value={getStringedDate(input.createdDate)} 
                type ="date" 
            />
        </section>
        <section className='emotion_section'>
            <h4>오늘의 감정</h4>
            <div className='emotion_list_wrapper'>
                {emotionList.map((item)=> (
                    <EmotionItem 
                    onClick={()=>onChangeInput({
                        target: {
                            name :"emotionId",
                            value : item.emotionId,
                        }
                    })}
                        key = {item.emotionId} 
                        {...item} 
                        isSelected={item.emotionId === input.emotionId}
                    />
                ))}
            </div>
        </section>
        <section className='content_section'>
            <h4>오늘의 일기</h4>
            <textarea 
            name = "content"
            value={input.content}
            onChange={onChangeInput}
            placeholder='오늘은 어땠나요?'/>
        </section>
        <section className='button_section'>
            <Button onClick={()=>nav(-1)} text={"취소하기"} />
            <Button 
                onClick={onClickSubmitButton}
                text={"작성완료"} 
                type={"POSITIVE"} />
        </section>
    </div>
    )
}

export default Editor
```

```jsx
export const emotionList = [
    {
        emotionId:1,
        emotionName:"완전 좋음"
    },
    {
        emotionId:2,
        emotionName:"좋음"
    },
    {
        emotionId:3,
        emotionName:"그럭저럭"
    },
    {
        emotionId:4,
        emotionName:"나쁨"
    },
    {
        emotionId:5,
        emotionName:"끔찍함"
    },
]
```

```jsx
.Viewer > section {
    width: 100%;
    margin-bottom: 100px;

    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
}

.Viewer >section >h4{
    font-size: 22px;
    font-weight: bold;
}

.Viewer .emtion_img_wrapper {
    width: 250px;
    height: 250px;
    border-radius: 5px;

    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;

    color: white;
    font-size: 25px;
}

.Viewer .emtion_img_wrapper_1{
    background-color: rgb(100, 201, 100);
}
.Viewer .emtion_img_wrapper_2{
    background-color: rgb(157, 215, 114);
}
.Viewer .emtion_img_wrapper_3{
    background-color: rgb(253,206,23);
}
.Viewer .emtion_img_wrapper_4{
    background-color: rgb(253, 132, 70);
}
.Viewer .emtion_img_wrapper_5{
    background-color: rgb(253, 86, 95);
}

.Viewer .content_wrapper {
    width: 100%;
    background-color: rgb(236,236,236);
    border-radius: 5px;

    word-break: keep-all;
    overflow-wrap: break-word;
}

.Viewer .content_wrapper > p {
    padding: 20px;
    text-align: left;
    font-size: 20px;
    font-weight: 400;
    line-height: 2.5;
}
```

12.17) 웹 스토리지 이용하기

웹 스토리지(Web Storage) - 데이터를 브라우저에 보관하는 방법, 일종의 데이터 베이스

배포 준비하기 - 프로젝트를 배포하기 전, 타이틀, Favicon, OG 설정 진행

배포하기 - 리액트 앱을 배포하는 방법

최적화는 언제 필요할까?

1. 비용이 많이 드는 계산
2. 매우 여러번, 반복적으로 실행되는 연산

React 렌더링 최적화와 관련된 기능들 - useMemo, useCallback, React.memo ⇒ 과하면 독…

Web Storage 

- 웹 브라우저에 기본적으로 내장되어 있는 데이터베이스
- 별도의 프로그램 설치 필요 X, 라이브러리 설치 필요 X
- 그냥 자바스크립트 내장함수 만으로 접근 가능
- SessionStorage
1. 브라우저 탭 별로 데이터를 보관
2. 탭이 종료되기 전에는 데이터 유지(새로고침)
3. 탭이 종료되거나 꺼지면 데이터제
- LocalStorage
1. 사이트 주소별로 데이터 보관
2. 사용자가 직접 삭제하기 전까지 데이터 보관

```jsx
import './App.css'
import { useReducer, useRef, createContext, useEffect,useState } from 'react'
import { Routes, Route } from 'react-router-dom'
import Home from './pages/Home'
import Diary from './pages/Diary'
import New from './pages/New'
import Edit from './pages/Edit'
import Notfound from './pages/Notfound'

function reducer(state, action){
  let nextState

  switch(action.type){
    case 'INIT': 
      return action.data;
    case 'CREATE':
      { nextState = [action.data, ...state];
        break;
      }
    case 'UPDATE':
      {nextState = state.map((item)=>
        String(item.id) === String(action.data.id) 
          ? action.data 
          : item
      )
      break;
    }
    case 'DELETE':
      {nextState = state.filter(
        (item)=> String(item.id) !== String(action.id)
    )
    break
  }
    default:
      return state;
  }

  localStorage.setItem("diary", JSON.stringify(nextState))
  return nextState
}

export const DiaryStateContext = createContext()
export const DiaryDispatchContext = createContext()

function App() {
  const [isLoading, setIsLoading] = useState(true)
  const [data, dispatch] = useReducer(reducer, [])
  const idRef = useRef(3)

  useEffect( ()=>{
    const storedData = localStorage.getItem("diary")
    if(!storedData){
      setIsLoading(false)
      return 
    }

    const parseData = JSON.parse(storedData)
    if(!Array.isArray(parseData)){
      setIsLoading(false)
      return;
    }

    let maxId = 0
    parseData.forEach((item)=>{
      if(Number(item.id) > maxId){
        maxId = Number(item.id)
      }
    })

    idRef.current = maxId + 1

    dispatch({
      type:"INIT",
      data: parseData,
    })
    setIsLoading(false)
  }, [])

  //새로운 일기 추가
  const onCreate = (createdDate, emotionId, content) => {
    dispatch({
      type:"CREATE",
      data: {
        id: idRef.current++,
        createdDate,
        emotionId,
        content,
      },
    })
  }
  //기존 일기 수정
  const onUpdate = (id, createdDate, emotionId, content) => {
    dispatch({
      type:"UPDATE",
      data : {
        id, createdDate, emotionId, content
      }
    })
  }

  //기존 일기 삭제
  const onDelete = (id) => {
    dispatch({
      type:"DELETE",
      id,
    })
  }

  if(isLoading) {
    return <div>데이터 로딩중입니다 ...</div>
  }

  return (
    <>
      <DiaryStateContext.Provider value={data}>
        <DiaryDispatchContext.Provider
          value={{
            onCreate,
            onUpdate,
            onDelete,
          }}
        >
          <Routes>
            <Route path='/' element={<Home />} />
            <Route path='/new' element={<New />} />
            <Route path='/diary:id' element={<Diary />} />
            <Route path='/edit/:id' element={<Edit />} />
            <Route path='*' element={<Notfound />} />
          </Routes>
        </DiaryDispatchContext.Provider>
      </DiaryStateContext.Provider>
    </>
  )
}

export default App
```

12.18) 배포 준비하기

![Untitled](%E1%84%89%E1%85%A6%E1%86%A8%E1%84%89%E1%85%A7%E1%86%AB%2012%20%E1%84%91%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8C%E1%85%A6%E1%86%A8%E1%84%90%E1%85%B33%20%E1%84%80%E1%85%A1%E1%86%B7%E1%84%8C%E1%85%A5%E1%86%BC%20%E1%84%8B%E1%85%B5%E1%86%AF%E1%84%80%E1%85%B5%E1%84%8C%E1%85%A1%E1%86%BC%2066d9c47f68fe42deb6b80f47b353918a/Untitled.png)

12.19) 배포하기

vercel 회원가입
터미널에 vercel 다운받기

[https://emotion-diary-jfg67ewxo-kimjiwons-projects.vercel.app/](https://emotion-diary-jfg67ewxo-kimjiwons-projects.vercel.app/)