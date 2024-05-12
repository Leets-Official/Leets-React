### UI 구현하기

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/dee95337-fab8-4558-af4b-30f82fe8884f/Untitled.png)

**Controller.jsx**

```jsx
const Controller = () => {
    return (
      <div>
        <button>-1</button>
        <button>-10</button>
        <button>-100</button>
        <button>+100</button>
        <button>+10</button>
        <button>+1</button>
      </div>
    );
  };
  
  export default Controller;
```

**Viewer.jsx**

```jsx
const Viewer = () => {
    return (
      <div>
        <div>현재 카운트 :</div>
        <h1>0</h1>
      </div>
    );
  };
  
  export default Viewer;
```

**App.jsx**

```jsx
import "./App.css";
import Viewer from "./components/Viewer";
import Controller from "./components/Controller";
import { useState } from "react";

function App() {
  return (
    <div className="App">
      <h1>Simple Counter</h1>
      <section>
        <Viewer  />
      </section>
      <section>
        <Controller  />
      </section>
    </div>
  );
}

export default App;
```

### 기능 구현하기

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/6dab8ff1-04b3-4bd4-896e-5ce7d5c37755/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/259b8663-41b4-4f36-923f-2d04f0169649/Untitled.png)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/3401e3c5-9089-4b06-8bef-1363c46053d5/Untitled.png)

App.jsx에 useState를 넣어서 기능을 구현하자!

**Controller.jsx**

```jsx
const Controller = ({ onClickButton }) => {
    return (
      <div>
        <button
          onClick={() => {
            onClickButton(-1);
          }}
        >
          -1
        </button>
        <button
          onClick={() => {
            onClickButton(-10);
          }}
        >
          -10
        </button>
        <button
          onClick={() => {
            onClickButton(-100);
          }}
        >
          -100
        </button>
        <button
          onClick={() => {
            onClickButton(100);
          }}
        >
          +100
        </button>
        <button
          onClick={() => {
            onClickButton(10);
          }}
        >
          +10
        </button>
        <button
          onClick={() => {
            onClickButton(1);
          }}
        >
          +1
        </button>
      </div>
    );
  };
  
  export default Controller;
```

**Viewer.jsx**

```jsx
const Viewer = ({ count }) => {
    return (
      <div>
        <div>현재 카운트 :</div>
        <h1>{count}</h1>
      </div>
    );
  };
  
  export default Viewer;
```

**App.jsx**

```jsx
import "./App.css";
import Viewer from "./components/Viewer";
import Controller from "./components/Controller";
import { useState } from "react";

function App() {
  const [count, setCount] = useState(0);

  const onClickButton = (value) => {
    setCount(count + value);
  };

  return (
    <div className="App">
      <h1>Simple Counter</h1>
      <section>
        <Viewer count={count} />
      </section>
      <section>
        <Controller onClickButton={onClickButton} />
      </section>
    </div>
  );
}

export default App;
```

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/7eb4d9b5-ca71-4d98-8b97-22b122996a8c/9c32b778-ab1c-414a-bddb-cac7c60ac08f/Untitled.png)