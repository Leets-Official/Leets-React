# 1주차

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

# 1주차 리액트

[https://www.notion.so](https://www.notion.so)

# 0. 초기 설정

- 크롬에서 f12  //개발자 도구
    - console창 //프롬프트를 이용해 자바스크립트 앤진을 실행시킬 수 있음.
    
    ![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled.png)
    
- vscode로 자바스크립트
    - html로 크롬에서 실행. “./”이라는 건 현재 경로라는 뜻. script로 꼭 연결해줘야 함.
    
    ![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%201.png)
    
    - html 코드 창에서 crtl+shift+p 누르고 live server 치면 크롬 브라우저가 코드를 웹페이지로 보여줌 (맨 밑의 port를 누르면 라이브 서버 꺼짐. → 웹페이지 종료)
    
    ![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%202.png)
    
    ![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%203.png)
    
    - 웹페이지에서 개발자 도구(f12)-console보면 자바스크립트의 chapter3가 잘 작동중인 걸 볼 수 있음

![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%204.png)

# 01. 자바스크립트 기본

### 변수

- let
    
    초기화 하든 말든 값을 바꿀 수 있음
    

### 상수

- const
    
    초기화 이후에 값을 바꿀 수 없음 (반드시 초기화를 해줘야 함)
    
- 변수 명명 규칙
    - $, _를 제외한 기호는 사용할 수 없음
    - 숫자로 시작할 수 없음
    - 예약어를 사용할 수 없음
    - 의미 있는 변수명으로 짓기

# 03. Node.js 기초

- 자바스크립트를 범용적으로 만들어준 것이 Node.js
- node.js 설치됐는지 확인 방법: 터미널 → node -v
- npm 설치됐는지 확인 방법: 터미널 → npm -v
- 패키지: node.js에서 사용하는 프로그램의 단위 ex) 쇼핑몰 패키
- 새 패키지 만들기: vscode → 파일 열기 → ctrl+J (터미널) → npm init
    
    잘 생성 됐다면 아래처럼 설정 파일이 자동으로 생성
    

![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%205.png)

- 패키지 안에 새로운 js 파일 만들고 node로 출력: node 파일이름.js
- 파일 이름이 길어질수록 복잡 → package.json 파일에서 start 추가

![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%206.png)

### 모듈 시스템

- 모듈: 각각 기능을 담은 js 파일 하나
- 모듈을 생성하고, 불러오고, 사용하는 등의 모듈을 다루는 다양한 기능을 제공하는 시스템
- CJS(Common JS 모듈 시스템)
    
    module.exports {함수: 내보낼 값};
    

### 라이브러리

프로그램을 개발할 때 필요한 다양한 기능들을 미리 만들어 모듈화 해 놓은 것

# 04.React.js

1. 컴포넌트를 기반으로 UI를 표현한다
2. 화면 업데이트 구현이 쉽다
    1. 선언형 프로그래밍 (과정 빼고 목적만 선언)
3. 화면 업데이트가 빠르게 처리된다 

- 리액트로 만든 웹페이지는 react app이라고 부름
- 리액트 앱 만들기

![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%207.png)

![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%208.png)

![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%209.png)

- 위와 같이 react app 폴더가 따로 만들어짐
    
    
    ![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%2010.png)
    
- 위와 같이 터미널에서 npm i로 라이브러리를 따로 모두 설치해줘야 초기 작업 완료
- react app 실행: npm run dev

![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%2011.png)

- 단축어

![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%2012.png)

- 함수 컴포넌트: 아래와 같이 html 태그를 반환할 수 있는 함수를 말함
    
    이때 함수 컴포넌트의 이름은 반드시 대문자로 시작해야 함 
    

![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%2013.png)

- 새로운 컴포넌트를 작동 시키고 싶으면 아래와 같이 <Header />를 써줘야 함 (main.jsx에서 <app />이 있기에 작동하기 때문)
    
    → Header: 자식 컴포넌트, App: 부모 컴포넌트 (Root 컴포넌트)
    
    따라서 다른 컴포넌트를 추가시키고 싶다면 무조건 App 컴포넌트의 자식으로 들어가야 함 
    

![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%2014.png)

- 모듈화를 위해 컴포넌트는 따로 scr아래에 components라는 폴더를 만들어 그 안에 구현
    1. App.jsx에 import Header from './components/Header'; 추가
        
        ![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%2015.png)
        
    2. Header.jsx 파일 따로 만들어 함수 적고 export default Header; 추가 

![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%2016.png)

- JSX(JavaScript Extensions): 확장된 자바스크립트의 문법. html과 자바 스크립트를 혼용해서 사용할 수 있게 해줌
    
    아래와 같이 변수 선언해서 html 태그와 혼용해서 쓰는 등
    

![변수, 연산식, 삼항연산자 모두 가능](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%2017.png)

변수, 연산식, 삼항연산자 모두 가능

![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%2018.png)

- JSX 주의사항
    1. 중괄호 내부에는 자바스크립트 표현식만 넣을 수 있음 (if문 for문 등 안됨)
    2. 숫자, 문자열, 배열 값만 화면에 랜더링 가능 (true나 undefined null, 객체 등은 안됨)
    3. 모든 태그는 닫혀있어야 함 (/)
    4. 최상위 태크는 무조건 하나여야 함 
- 아래의 if문과 return은 똑같은 기능을 수행함 (편한 거로 골라서)

![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%2019.png)

![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%2020.png)

- 스타일 추가 방법
    - 직접 리턴문 안에 추가 (주의: background-color가 아니라 대문자로 이어써야 함)
        
        ![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%2021.png)
        
        ![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%2022.png)
        
    - css 파일 따로 만들기
        1. 컴포넌트 파일 안에 Main.css 파일 만들어서 작성
            
            ![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%2023.png)
            
        2. Main.jsx에서 css 불러오고(import "./Main.css";), 적용할 곳에 className 작성(<div className="logout">로그아웃</div>)
        
        ![Untitled](1%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1%20%E1%84%85%E1%85%B5%E1%84%8B%E1%85%A2%E1%86%A8%E1%84%90%E1%85%B3%20fa36c7dbaec8483e8d7e8dc534c65891/Untitled%2024.png)
---

</br>

### 질문
