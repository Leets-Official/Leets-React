# 4-5주차

**강의**
[인프런] - 한입 크기로 잘라머는 리액트(React.js) : 기초부터 실전까지
(https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8)

### 범위

섹션 12.5 ~ 섹션 13

---

</br>

### 학습 내용

# 감정일기장 프로젝트

프로젝트 개발 순서

1. 사람마다 다르지만 보통
   1. 페이지 라우팅 - 글로벌 레이아웃 설정 - 공통 컴포넌트 구현 - 개별 페이지 및 복잡한 기능 구현

1) 공통 컴포넌트 구현

- Button
  - Button.css : css 스타일 구현
  - Button.jsx : 부모 컴포넌트인 App.jsx의 Button 컴포넌트에 props를 전달하여
    Button 컴포넌트에서 이를 전달받아 종류별 버튼 구현
    props 값에 따라 다른 스타일을 적용 - > props의 값에 따라서 렌더링하려는
    요소의 클래스 네임을 동적으로 변경

2. home: 일기 리스트 렌더링

diary : 일기 상세 조회

new: 새로운 일기 작성

edit: 기존 일기 수정

3. 일기 관리 기능 구현하기

- App.jsx : useReducer()로 일기 데이터를 저장할 state 생성 , 임시데이터 ( mockData ) 를 만들어서 state의 초기값으로 설정
- 새로운 일기 추가 기능
  ```jsx
  function reducer(state, action) {
    switch (action.type) {
      case "CREATE":
        return [action.data, ...state];
    }
  }

  const [data, dispatch] = useReducer(reducer, mockData);
  const idRef = useRef(3);
  // 새로운 일기 추가
  const onCreate = (createdDate, emotionId, content) => {
    dispatch({
      type: "CREATE",
      data: {
        id: idRef.current++,
        createdDate,
        emotionId,
        content,
      },
    });
  };
  ```
- 기존 일기 수정

```jsx
function reducer(state, action) {
  switch (action.type) {
    case "CREATE":
      return [action.data, ...state];
    case "UPDATE":
      return state.map((item) =>
        String(item.id) === String(action.data.id) ? action.data : item
      );
  }
}

// 기존 일기 수정
const onUpdate = (id, createdDate, emotionId, content) => {
  dispatch({
    type: "UPDATE",
    data: {
      id,
      createdDate,
      emotionId,
      content,
    },
  });
};

// return 문

<button
  onClick={() => {
    onUpdate(1, new Date().getTime(), 3, "수정된 일기입니다");
  }}
>
  일기 수정 테스트{" "}
</button>;
```

- 기존 일기 삭제

```jsx
function reducer(state, action) {
  switch (action.type) {
    case "CREATE":
      return [action.data, ...state];
    case "UPDATE":
      return state.map((item) =>
        String(item.id) === String(action.data.id) ? action.data : item
      );
    case "DELETE":
      return state.filter((item) => String(item.id) !== String(action.id));
  }
}

// 기존 일기 삭제
const onDelete = (id) => {
  dispatch({
    type: "DELETE",
    id,
  });
};
```

4. Context 활용하기

- 모든 페이지가 쉽게 공급받아서 이용할 수 있도록 데이터 공급 설정

```jsx
const DiaryStateContext = createContext();
const DiaryDispatchContext = createContext();
...

<DiaryStateContext.Provider value={data}>
        <DiaryDispatchContext.Provider value={{ onCreate, onUpdate, onDelete }}>
          <Routes>
            <Route path="/" element={<Home />} />
            <Route path="/new" element={<New />} />
            <Route path="/diary/:id" element={<Diary />} />
            <Route path="/edit/:id" element={<Edit />} />
            <Route path="*" element={<Notfound />} />
          </Routes>
        </DiaryDispatchContext.Provider>
 </DiaryStateContext.Provider>
```

[5) HOME 페이지 구현](https://www.notion.so/5-HOME-6937851919454b48a8eb189931458384?pvs=21)

# 5) HOME 페이지 구현

1️⃣ UI

![Untitled](5)%20HOME%20%E1%84%91%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%8C%E1%85%B5%20%E1%84%80%E1%85%AE%E1%84%92%E1%85%A7%E1%86%AB%206937851919454b48a8eb189931458384/Untitled.png)

- Header 컴포넌트
  ```jsx
  import "./Header.css";

  const Header = ({ title, leftChild, rightChild }) => {
    return (
      <header className="Header">
        <div className="header_left">{leftChild}</div>
        <div className="header_center">{title}</div>
        <div className="header_right">{rightChild}</div>
      </header>
    );
  };

  export default Header;
  ```
- DiaryList 컴포넌트
  ```jsx
  import Button from "./Button";
  import "./DiaryList.css";
  import DiaryItem from "./DiaryItem";

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
    );
  };
  export default DiaryList;
  ```
- DiaryItem 컴포넌트

![Untitled](5)%20HOME%20%E1%84%91%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%8C%E1%85%B5%20%E1%84%80%E1%85%AE%E1%84%92%E1%85%A7%E1%86%AB%206937851919454b48a8eb189931458384/a086e4b5-8a45-4d37-ae6a-2fd56610a1c4.png)

1. image section

- emotionId에 따라 다른 이미지가 렌더링되도록 설정

```jsx
<div className={`img_section img_section_${emotionId}`}>
  <img src={getEmotionImage(emotionId)} />
</div>
```

2. info section

```jsx
<div className="info_section">
  <div className="created_date">{new Date().toLocaleDateString()}</div>
  <div className="content">일기 컨텐츠</div>
</div>
```

3. button section

- button 컴포넌트 재사용

<Button text={”수정하기”} />

2️⃣ 기능

1. Header의 < , > 화살표를 클릭했을 때 이전 달 혹은 다음 달 글씨로 바뀌도록 하기

- 날짜를 저장하는 state 생성
  ```jsx
  const [pivotDate, setPivotDate] = useState(new Date());
  ```
- “<” , “>” button 컴포넌트에 onClick 이벤트로 각각 onDecreaseMonth, onIncreaseMonth 함수를 호출하도록 함

```jsx
const onIncreaseMonth = () => {
    setPivotDate(new Date(pivotDate.getFullYear(), pivotDate.getMonth() + 1));
  };
  const onDecreaseMonth = () => {
    setPivotDate(new Date(pivotDate.getFullYear(), pivotDate.getMonth() - 1));
  };

  ....
  <Header
        title={`${pivotDate.getFullYear()}년 ${pivotDate.getMonth() + 1}월`}
        leftChild={<Button onClick={onDecreaseMonth} text={"<"} />}
        rightChild={<Button onClick={onIncreaseMonth} text={">"} />}
   />
```

2. 해당 달에 해당하는 일기 리스트만 필터링 되도록 하기

- App.jsx의 context 를 export 시키기
- Home.jsx에서 DiaryStateContext import 해와서 context가 공급하는 일기 데이터를 데이터라는 이름으로 받아오기

```jsx
const data = useContext(DiaryStateContext);
```

<aside>
🤔  데이터를 공급받을 수 있는 이유

→ App 컴포넌트 안에 context를 만들고 해당 context의 provider를 app 컴포넌트의 return문 안에 모든 페이지들을 하위 컴포넌트로 감싸도록 해주고 value props로 data를 내려보내줌

</aside>

- item.createdDate가 해당 달의 시작 일 ~ 마지막 일 사이이면 filter되어서 반환되도록 하기

  - getMonthlyData 함수를 만들고 pivotDate state에 저장된 날짜와 일기 data를 기반으로 filter 기능
    - 시작 일 : beginTime
    - 마지막 일 : endTime

  ```jsx
  const getMonthlyData = (pivotDate, data) => {
    const beginTime = new Date(
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
      0,
      23,
      59,
      59
    ).getTime();

    return data.filter(
      (item) => beginTime <= item.createdDate && item.createdDate <= endTime
    );
  };
  ```

- Home 컴포넌트에서

```jsx
const monthlyData = getMonthlyData(pivotDate, data);
```

return 문에 DiaryList 컴포넌트에 data로 monthlyData 전달

```jsx
<DiaryList data={monthlyData} />
```

- DiaryList 컴포넌트에서

전달받은 data를 props로 받아서 map 메소드를 이용해 콜백함수를 전달하여 각각의 일기 아이템을 DiaryItem 컴포넌트로 변환해서 리스트로 렌더링. 고유한 key 값 설정 !

```jsx
<div className="list_wrapper">
  {data.map((item) => (
    <DiaryItem key={item.id} {...item} />
  ))}
</div>
```

- DiaryItem 컴포넌트에서 id, emotionId, createdDate,content를 props로 받아와서 렌더링하도록 하기

```jsx
const DiaryItem = ({ id, emotionId, createdDate, content }) => {
  return (
    <div className="DiaryItem">
      <div className={`img_section img_section_${emotionId}`}>
        <img src={getEmotionImage(emotionId)} />
      </div>
      <div className="info_section">
        <div className="created_date">
          {new Date(createdDate).toLocaleDateString()}
        </div>
        <div className="content">{content}</div>
      </div>
      <div className="button_section">
        <Button text={"수정하기"} />
      </div>
    </div>
  );
};
```

3. 이미지 section이나 info section 클릭 시 다이어리 페이지로 이동, 수정하기 버튼 클릭 시 edit 페이지로 이동하기,

새 일기 쓰기 버튼 클릭시 /new 페이지로 이동하기

- useNavigate() 사용

4. 최신순, 오래된 순에 따른 정렬

- sortType state 생성

```jsx
const [sortType, setSortType] = useState("latest");
```

- onChange 이벤트 설정 , select에 onChange 이벤트 전달

```jsx
const onChangeSortType = (e) => {
  setSortType(e.target.value);
};
```

- data 정렬
  - toSorted 메소드 활용: 원본 배열은 수정하지 않고 정렬된 새로운 배열 반환
  ```jsx
   const getSortedDate = () => {
      return data.toSorted((a, b) => {
        if (sortType === "oldest") {
          return Number(a.createdDate) - Number(b.createdDate);
        } else {
          return Number(b.createdDate) - Number(a.createdDate);
        }
      });
    };

    const sortedData = getSortedDate();

    ...

    // return 문 일부: data-> sortedData로 수정
    <div className="list_wrapper">
          {sortedData.map((item) => (
            <DiaryItem key={item.id} {...item} />
          ))}
     </div>
  ```

[6)New 페이지 구현](https://www.notion.so/6-New-485cdd77d89a46af9d80b955e836b47b?pvs=21)

# 8)Diary 페이지 구현

1️⃣UI

1. Diary 페이지 구성

![Untitled](8)Diary%20%E1%84%91%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%8C%E1%85%B5%20%E1%84%80%E1%85%AE%E1%84%92%E1%85%A7%E1%86%AB%20f1fa93c982d64ce58f88622f4e55b538/Untitled.png)

2. Header, Button 컴포넌트 재사용

3. Viewer 컴포넌트 구성

![Untitled](8)Diary%20%E1%84%91%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%8C%E1%85%B5%20%E1%84%80%E1%85%AE%E1%84%92%E1%85%A7%E1%86%AB%20f1fa93c982d64ce58f88622f4e55b538/Untitled%201.png)

4. img_section 구현

- Editor 컴포넌트의 emotionList 를 별도의 module로 분리( util → emotionList.js)
- import 해서 사용

5. 뒤로가기, 수정하기 클릭 시 이동

- useNavigate() 사용

6.  custom hook 만들기

- 현재 조회중인 일기 데이터의 날짜를 불러와서 header의 타이틀로 렌더링 , 감정 이미지, 일기 내용까지 렌더링 하도록 하기 ( 일기 데이터 불러오기 )

7. getStringedDate 함수 모듈로 분리

- import 해서 사용

```jsx
// Diary 컴포넌트

 const title = getStringedDate(new Date(createdDate));

 ...
 return (
    <div>
      <Header
        title={`${title} 기록`}
        leftChild={<Button onClick={() => nav(-1)} text={"<뒤로 가기"} />}
        rightChild={
          <Button onClick={() => nav(`/edit/${params.id}`)} text={"수정하기"} />
        }
      />
      <Viewer emotionId={emotionId} content={content} />
    </div>
  );
```

[7) Edit 페이지 구현](https://www.notion.so/7-Edit-49ed45c1864443bfa5e2adecaa75de67?pvs=21)

# 7) Edit 페이지 구현

1️⃣ UI

1. Edit 페이지 구성

![Untitled](7)%20Edit%20%E1%84%91%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%8C%E1%85%B5%20%E1%84%80%E1%85%AE%E1%84%92%E1%85%A7%E1%86%AB%2049ed45c1864443bfa5e2adecaa75de67/Untitled.png)

2. 컴포넌트 재사용

- Header, Button, Editor import 해서 재사용

3. 뒤로가기 , 삭제하기

- useNavigate() 사용
- 삭제하기 : 팝업창 띄우기 → 확인 클릭시 삭제

```jsx
const { onDelete } = useContext(DiaryDispatchContext);
const onClickDelete = () => {
  if (window.confirm("일기를 정말 삭제할까요? 다시 복구되지 않아요!")) {
    //일기 삭제 로직
    onDelete(params.id);
    nav("/", { replace: true });
  }
};
```

4. 존재하지 않는 diary id 접근 시 팝업 띄우고 홈페이지로 이동하기

```jsx
const getCurrentDiaryItem = () => {
  const currentDiaryItem = data.find(
    (item) => String(item.id) === String(params.id)
  );

  if (!currentDiaryItem) {
    window.alert("존재하지 않는 일기입니다.");
    nav("/", { replace: true });
  }
  return currentDiaryItem;
};

const currentDiaryItem = getCurrentDiaryItem();
```

- useEffect , useState 사용

```jsx
const [curDiaryItem, setCurDiaryItem] = useState();

useEffect(() => {
  const currentDiaryItem = data.find(
    (item) => String(item.id) === String(params.id)
  );

  if (!currentDiaryItem) {
    window.alert("존재하지 않는 일기입니다.");
    nav("/", { replace: true });
  }
  setCurDiaryItem(currentDiaryItem);
}, [params.id, data]);
```

→ useEffect에 의해 컴포넌트가 마운트된 이후이거나 params의 아이디나 데이터 state가 바뀌었을 때 일기 data로부터 find 메소드를 통해 현재 우리가 수정하려고 하는 일기 아이템의 데이터를 꺼내와서 setCurrentDiaryItem이라는 함수를 통해서 state에 보관

- 작성 완료 클릭 시 수정되도록 하기
  - Edit 컴포넌트에 onSubmit 이벤트 추가
  - Context를 통해 onUpdate 함수 호출
  ```jsx
  const onSubmit = (input) => {
    if (window.confirm("일기를 정말 수정할까요? ")) {
      onUpdate(
        params.id,
        input.createdDate.getTime(),
        input.emotionId,
        input.content
      );
    }
    nav("/", { replace: true });
  };
  ```

[8)Diary 페이지 구현](https://www.notion.so/8-Diary-f1fa93c982d64ce58f88622f4e55b538?pvs=21)

# 6)New 페이지 구현

1️⃣UI

1. New Page 컴포넌트 구성

![Untitled](6)New%20%E1%84%91%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%8C%E1%85%B5%20%E1%84%80%E1%85%AE%E1%84%92%E1%85%A7%E1%86%AB%20485cdd77d89a46af9d80b955e836b47b/Untitled.png)

2. New Page - Editor 컴포넌트 구성

![Untitled](6)New%20%E1%84%91%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%8C%E1%85%B5%20%E1%84%80%E1%85%AE%E1%84%92%E1%85%A7%E1%86%AB%20485cdd77d89a46af9d80b955e836b47b/Untitled%201.png)

- 오늘의 감정을 나타내는 EmotionItem 컴포넌트를 Editor 컴포넌트에서 일일이 emotionId와 emotionName을 전달하는 방식보다는 Editor 컴포넌트 외부에 emotionList 변수를 만들어 , 이 변수에 배열로 데이터만 따로 저장해둔 다음 map 메소드로 리스트로 렌더링 시키는 것이 좋음

```jsx
const emotionList = [
  {
    emotionId: 1,
    emotionName: "완전 좋음",
  },
  {
    emotionId: 2,
    emotionName: "좋음",
  },
  {
    emotionId: 3,
    emotionName: "그럭저럭",
  },
  {
    emotionId: 4,
    emotionName: "나쁨",
  },
  {
    emotionId: 5,
    emotionName: "끔찍함",
  },
];

.
.
.
// return 문 일부
 <section className="emotion_section">
    <h4>오늘의 감정</h4>
    <div>
      {emotionList.map((item) => (
      <EmotionItem key={item.emotionId} {...item} />
      ))}
     </div>
  </section>
```

- EmotionItem에 cursor 시 해당 감정 색으로 배경색 변화시키기
  - isSelected props 전달
  - EmotionItem 컴포넌트에서 className 추가
  ```jsx
  const EmotionItem = ({ emotionId, emotionName, isSelected }) => {
    return (
      <div
        className={`EmotionItem ${
          isSelected ? `EmotionItem_on_${emotionId}` : ""
        }`}
      >
        <img className="emotion_img" src={getEmotionImage(emotionId)} />
        <div className="emotion_name">{emotionName}</div>
      </div>
    );
  };
  ```
- textarea, 취소하기, 작성완료 버튼 구현
  - 버튼 컴포넌트 재사용
  ```jsx
   <section className="content_section">
          <h4>오늘의 일기</h4>
          <textarea placeholder="오늘은 어땠나요?" />
    </section>
    <section className="button_section">
          <Button text={"취소하기"} />
          <Button text={"작성완료"} type={"POSITIVE"} />
     </section>
  ```

2️⃣기능

1. 뒤로 가기 버튼 클릭시 페이지 이동

- useNavigate() 사용
- 인수로 -1 전달

2. <오늘의 날짜 section>

- state 를 하나의 객체 형태로 만들어서 input state에 보관

```jsx
 const [input,setInput] = useState({
    createdDate : new Date(),
    emotionId : 3,
    content: ""
  });

  ...

 <input  value={input.createdDate} type="date" />
```

→ input 태그는 Date 객체로 설정된 값을 이해하지 못함

→문자열로 변환해서 넣어줘야 함( 문자열 변환 함수 추가)

```jsx
const getStringedDate = (targetDate) => {
  // 날짜 -> YYYY-MM-DD
  let year = targetDate.getFullYear();
  let month = targetDate.getMonth() + 1;
  let date = targetDate.getDate();

  if (month < 10) {
    month = `0${month}`;
  }
  if (date < 10) {
    date = `0${date}`;
  }

  return `${year}-${month}-${date}`;
};
```

- 오늘의 날짜를 선택했을 때 해당 날짜로 바꿔주기
  - 이벤트핸들러 onChangeInput

```jsx
const onChangeInput = (e) => {
  console.log(e.target.name); // 어떤 요소에 입력이 들어온건지
  console.log(e.target.value); // 입력된 값이 무엇인지

  setInput({
    ...input,
    [e.target.name]: e.target.value,
  });
};
```

→ Date 객체가 아닌 문자열이 저장되는 문제 발생

→ Date 객체로 바꿔줘야 함

```jsx
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
```

3. <오늘의 감정 section>

- 감정 클릭 시 emotionId 변화

```jsx
 <EmotionItem
      onClick={() =>
        onChangeInput({
           target: {
           name: "emotionId",
           value: item.emotionId,
            },
       })
      }


 // EmotionItem 컴포넌트에 div 에 onClick 전달
```

4. <오늘의 일기 section >

```jsx
<section className="content_section">
  <h4>오늘의 일기</h4>
  <textarea
    name="content"
    value={input.content}
    onChange={onChangeInput}
    placeholder="오늘은 어땠나요?"
  />
</section>
```

- onSubmit 기능
- 새 일기 작성 완료 클릭 시 페이지 이동
- 뒤로 가기 눌렀을 때 new 페이지로 접근하지 못하도록 방지

```jsx
const onSubmit = (input) => {
  onCreate(input.createdDate.getTime(), input.emotionId, input.content);

  nav("/", { replace: true });
};
```

[웹 스토리지 이용](https://www.notion.so/6577c6bee5734fbdaa9e164445e6e032?pvs=21)

# 웹 스토리지 이용

1. 웹 스토리지(Web Storage)

⚠️새로운 일기 작성 → 페이지 새로고침 → 일기 데이터 초기화됨

→ 추가한 일기 데이터는 실제로 react state에 보관 . State 또한 내부적으로는 js 변수에 저장된 값이나 다름 없음

→ 새로고침하면 state 값 초기화

😃외부 데이터베이스로부터 저장된 State 값 꺼내오기 (mysql, mongoDB보다 간편한 web storage 사용)

- 데이터를 브라우저에 보관하는 방법, 일종의 데이터 베이스. 웹 브라우저에 기본적으로 내장되어 있음.
- 별도의 프로그램 설치 필요 x, 라이브러리 설치 필요 x
- 그냥 자바스크립트 내장 함수만으로 접근 가능
- ex) 값을 저장: localStorage.setItem(key,value);
          값을 꺼냄: localStorage.getItem(key)
- SessionStorage
- LocalStorage

![Untitled](%E1%84%8B%E1%85%B0%E1%86%B8%20%E1%84%89%E1%85%B3%E1%84%90%E1%85%A9%E1%84%85%E1%85%B5%E1%84%8C%E1%85%B5%20%E1%84%8B%E1%85%B5%E1%84%8B%E1%85%AD%E1%86%BC%206577c6bee5734fbdaa9e164445e6e032/Untitled.png)

- 적용하기

```jsx
// App 컴포넌트

function reducer(state, action) {
  let nextState;
  switch (action.type) {
    case "CREATE": {
      nextState = [action.data, ...state];
      break;
    }
    case "UPDATE": {
      nextState = state.map((item) =>
        String(item.id) === String(action.data.id) ? action.data : item
      );
      break;
    }
    case "DELETE": {
      nextState = state.filter((item) => String(item.id) !== String(action.id));
      break;
    }
    default:
      return state;
  }

  localStorage.setItem("diary", JSON.stringify(nextState));
  return nextState;
}
```

2. 배포 준비하기

- 페이지 타이틀 설정하기
- Favicon 설정하기
  - 이미지 불러와서 index.html 의 link태그의 href 변경
- 오픈 그래프 태그 설정하기
  - 웹사이트의 링크를 공유할 때 썸네일,제목 등의 정보를 노출하는 것
  - index.html 에 meta 태그 추가
  ```jsx
  <meta property="og:title" content="감정 일기장"/>
  <meta property="og:dsecription" content="나만의 작은 감정 일기장"/>
  <meta property="og:image" content="thumbnail.png"/>
  ```
- 프로젝트 빌드

3. 배포하기

- 리액트 앱을 배포하는 방법
  - 현존 유명 클라우드 서비스: AwS, GCP, Vercel, Netlify, Firebase 등
  - Vercel : 프론트엔드 개발자를 위한 클라우드 서비스. React.js의 확장판 개념인 Next.js를 개발하는 회사
- 명령어
  - npm install -g vercel
  - vercel login
