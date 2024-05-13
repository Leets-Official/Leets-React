# 3주차

**강의**
[인프런] - 한입 크기로 잘라머는 리액트(React.js) : 기초부터 실전까지
(https://www.inflearn.com/course/%ED%95%9C%EC%9E%85-%EB%A6%AC%EC%95%A1%ED%8A%B8)

### 범위

섹션 8 ~ 섹션 12.5

- [ ] 8.  프로젝트2.투두리스트
- [ ] 9.  useReducer
- [ ] 10. 최적화
- [ ] 11. Context
- [ ] 12. 프로젝트3. 감정일기장

---

</br>

### 학습 내용

# State와 Hooks

1. State 란?
   1. State는 간단히 말하면 변수이다
   2. 일반 변수와 무엇이 다른가?

      1. 일반 변수는 값이 변경되어도 자동으로 화면이 리렌더링되지 않는다
      2. 그러나 state는 값이 변경되면 자동으로 리렌더링되어 화면이 바뀐다
      3. 즉, 자주 변경되는 데이터를 state 안에 담는다고 생각하면 쉽다

      🔎리렌더링이 발생하는 조건

      - state가 변경되었을 때
      - props가 변경되었을 때
      - 부모 컴포넌트가 리렌더링되면 자식 컴포넌트도 리렌더링
2. useState

   1. 함수 컴포넌트 내부에서 상태를 정의하고, 이 상태를 관리할 수 있게 해주는 hook ( State 기능을 낚아채오는 Hook)
   2. useState의 인수로는 사용할 state의 초깃값을 넘겨준다
   3. useState의 반환 값은 배열
   4. setState 함수는 비동기

   ```jsx
   const [state, setState] = useState(초기값);
   ```

3. useRef
   1. 새로운 Reference 객체를 생성하는 기능
   2. 컴포넌트가 렌더링하는 특정 DOM 요소에 접근
   3. useState와의 비교

      1. 컴포넌트 내부에서 사용할 변수를 생성한다는 점에서 동일
      2. 그러나 useRef로 생성한 변수는 값이 바뀌더라도 리렌더링을 유발하지 않음 ( useState는 값이 변경되면 컴포넌트 리렌더링)
      3. useRef로 선언된 값은 current 객체 안에 저장

      ```jsx
      const refObject = useRef();
      ```
4. useEffect

   1. 리액트 컴포넌트의 side effect를 제어하는 hook
   2. 매번 컴포넌트가 렌더링 될 때 특정 조건에 의존하여 수행(의존성 배열)
      1. Side Effect ?

         - 리액트에서는 “부수적인 효과”,”파생되는 효과” 정도로 해석 가능

         ![Untitled](State%E1%84%8B%E1%85%AA%20Hooks%2038c4a17167de491d85f2b0dd28fa9131/Untitled.png)
   3. useEffect는 언제 쓸까 ?

      1. 컴포넌트가 mount 됐을 때 ( 처음 로드되었을 때 )
      2. 컴포넌트가 update 될 때 ( 특정 props,state가 바뀔 때)
      3. 컴포넌트가 unmount 될 때 ( 사라질 때 )

      ```jsx
      useEffect(() => {}, []); // function, deps
      // [] : dependency array(deps)
      //    : deps에 특정 값을 넣게 되면 컴포넌트가
      //      mount될 때, 지정한 값이 업데이트될 때
      //      useEffect 실행
      // 배열을 생략한다면 리렌더링 될 때 마다 실행
      ```

   4. deps에 특정 값을 넣게 된다면 컴포넌트가 처음 마운트 될 때, 지정한 값이 바뀔 때, 언마운트 될 때, 값이 바뀌기 직전에 모두 호출

   5. useReducer

      1. 컴포넌트 내부에 새로운 State를 생성하는 React Hook
      2. 모든 useState는 useReducer로 대체 가능
      3. 상태 관리 코드를 컴포넌트 외부로 분리할 수 있음

      → useState를 사용하면?

      컴포넌트 내부에 상태 관리 코드를 작성해야 함

      ```jsx
      import { useReducer } from "react";

      //reducer : 번역기
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
        // dispatch : 발송하다 , 급송하다
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

      - useReducer()
        - const [ 상태, 액션을 발생시킬 함수 ] = useReducer(reducer 함수 , 초기 상태)
        - dispatch 설정
          - dispatch 함수 내부의 값은 객체 형태
          - 객체 내부에서는 상태 업데이트를 구분하는 type 사용

      <aside>
      💡 useReducer는 언제 사용하는 것이 좋을까?

      1. state의 형태가 복잡할 때
      2. 분산된 setState 로직을 한 곳에 모으고 싶을 때
      </aside>

      3. useMemo

         1. “메모이제이션” 기법을 기반으로 불필요한 연산을 최적화하는 React Hook
         2. 함수가 실행되어 반환하는 값을 캐싱하고 랜더링되어도 연산을 다시 하지 않고(랜더링 함수가 재실행되면 함수 연산도 재실행되어야 하지만 다시 하지 않음) 값을 캐싱(저장)하여 재사용

      4. React.memo

         1. 컴포넌트를 인수로 받아, 최적화된 컴포넌트로 만들어 반환

         ```jsx
         const MemoizedComponent = memo(Component);
         //     --> 반환값: 최적화된 컴포넌트. props를 기준으로 메모이제이션됨
         ```

      5. useCallback
         1. 랜더링 함수가 리랜더링 되면 함수나 변수 등도 다시 선언하게 되는데, useCallback을 사용하여 선언한 함수는 랜더링 되어도 다시 선언하지 않고 저장되어 있던 값을 재사용

# Context

1. React Context

   1. 컴포넌트 간의 데이터를 전달하는 또 다른 방법
   2. 기존의 Props가 가지고 있던 단점을 해결할 수 있음

   <aside>
   🤔 Props는 어떤 단점이 있을까?

   1. Props는 부모 → 자식으로만 데이터를 전달할 수 있음

   → Props Drilling

   </aside>

   c. Context: 데이터 보관소(객체)

   d. Context 사용을 위한 단계

   1. createContext 메서드를 사용해 context 생성

   2. 생성된 context를 가지고 context provider로 컴포넌트를 감싼다

   3. value prop을 사용해 context provider에 원하는 값을 입력한다

   4. context consumer를 통해 필요한 컴포넌트에 그 값을 불러온다

# 최적화

1. 최적화(Optimization)
   1. 웹 서비스의 성능을 개선하는 모든 행위를 일컫음

      ( 아주 단순한 것부터 아주 어려운 방법까지 매우 다양함)

   2. 일반적인 웹 서비스 최적화 방법
      - 서버의 응답 속도 개선
      - 이미지, 폰트, 코드 파일 등의 정적 파일 로딩 개선
      - 불필요한 네트워크 요청 줄임
   3. React App 내부의 최적화 방법
      - 컴포넌트 내부의 불필요한 연산 방지
      - 컴포넌트 내부의 불필요한 함수 재생성 방지
      - 컴포넌트의 불필요한 리렌더링 방지

# Page Routing

<aside>
💡 React는 CSR, SPA 방식으로 작동한다 !

</aside>

1. 페이지 라우팅이란?
   1. 경로에 따라 알맞은 페이지를 렌더링 하는 과정

      ex) /new → new 페이지 렌더링
2. 페이지 라우팅의 원리

   1. Multi Page Application(MPA)

      1. 애초에 서버가 여러 개의 페이지를 가지고 있음
      2. 많은 서비스가 사용하는 전통적인 방식
      3. 페이지 이동이 쾌적하지 못함
      4. 서버의 부하가 심해짐

      b. 서버 사이드 렌더링(SSR)

   - 서버에서 페이지를 그림
   - 사용자가 웹 페이지 접속 → 서버에서 페이지 렌더링 → 완성된 페이지 전달
   - js를 실행하지 않아도 화면을 보여줄 수 있음

   👍🏻페이지 이동이 매끄럽고 효율적

   👍🏻 검색 엔진 최적화에 유리

   👎🏻 서버 부담 증가

   👎🏻 무거운 페이지라면 오히려 CSR보다 속도가 느림

   → React.js는 이 방식을 따르지 않음

3. SPA(Single Page Application)
   - 말 그래도 페이지가 1개인 어플리케이션(.html)
   - reactJs와 같이 컴포넌트로 분리된 라이브러리나 프레임워크는 SPA에 최적화
4. CSR(Client Side Rendering)

   - 사용자 측에서 화면을 그림
   - 사용자가 웹 페이지 접속 → 프론트엔드는 화면을 그리기 위한 리소스 전달

   👍🏻 페이지에 필요한 리소스를 한번에 전달, 해당

   데이터를 통해서 다시 프론트엔드 서버와 소통없이도 렌더링이 가능

   👍🏻 초기 첫 페이지 렌더링 속도가 느림, 그러나 그 이후의 랜더링 속도는 상대적으로 빠름

   👎🏻 초기 페이지 렌더링 느림

   👎🏻 검색 엔진 최적화에 불리

   👎🏻 사용자의 하드웨어에 의존

5. 라우팅 설정하기
   1. npm i react-router-dom
   2. <BrowserRouter>로 App 컴포넌트 감싸주기
6. useNavigate()

   1. 페이지 이동할 때 사용
      1. Link의 용도와 마찬가지
      2. 하지만 Link는 클릭 시 페이지를 바로 이동하게 하는 기능을 하고 useNavigate는 조건을 만족했을 때 페이지 전환을 하도록 함

         ex) Link : 상품을 클릭하면 해당 상품에 대한 디테일 페이지로 이동

         useNavigate : 회원가입이 완료되면 메인페이지로 이동

   ```jsx
   const navigate = useNavigate();
   ```

   b. navigate 변수는 첫 번째 인자로 이동시킬 페이지의 주소를 넣거나 -1과 같은 값을 넣어 페이지 히스토리의 뒤로가기 버튼과 같은 동작을 시킬 수 있음

7. 동적 경로(Dynamic Segments)
   1. URL Parameter

      1. / 뒤에 아이템의 id를 명시

      ex) ~/product/1 ~/product/2

      ii. 아이템의 id 등의 변경되지 않는 값을 주소로 명시하기 위해 사용됨

   2. Query String
      1. ? 뒤에 변수명과 값 명시

         ex) ~/search?q=검색어

      2. 검색어 등의 자주 변경되는 값을 주소로 명시하기 위해 사용된다
