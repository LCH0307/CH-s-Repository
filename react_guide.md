
---  

### 📌 **React 개념 및 프로젝트 구조 정리**
  
## **1. React란?**
React는 Facebook(현 Meta)에서 개발한 **UI 라이브러리**로, **컴포넌트 기반 개발, 가상 DOM, 단방향 데이터 흐름** 등의 특징을 갖고 있다.

---

## **2. React의 주요 특징**
### ✅ **1) 컴포넌트 기반 (Component-Based)**
- UI를 독립적인 **컴포넌트**로 나누어 개발 및 관리 가능
- 컴포넌트는 재사용성이 뛰어나고, 유지보수가 쉬움

```jsx
function Button({ label }) {
  return <button>{label}</button>;
}

function App() {
  return <Button label="클릭하세요!" />;
}
```

---

### ✅ **2) Virtual DOM (가상 DOM)**
- 실제 DOM을 직접 변경하는 대신, **Virtual DOM에서 변경 사항을 먼저 계산한 후 최소한의 변경만 실제 DOM에 적용**
- 렌더링 성능 최적화

---

### ✅ **3) 단방향 데이터 흐름 (One-way Data Binding)**
- 부모 → 자식 방향으로만 데이터가 흐름 (`props`를 통해 전달)

```jsx
function Child({ message }) {
  return <h1>{message}</h1>;
}

function Parent() {
  return <Child message="Hello from Parent!" />;
}
```

---

### ✅ **4) 상태(State) 관리**
- `useState` 훅을 사용하여 상태를 관리

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>카운트: {count}</p>
      <button onClick={() => setCount(count + 1)}>+1</button>
    </div>
  );
}
```

---

### ✅ **5) React Hooks**
- `useState`, `useEffect`, `useReducer` 등 다양한 훅 제공

---

### ✅ **6) SPA(Single Page Application) 지원**
- React Router를 사용하여 **클라이언트 사이드 라우팅 가능**.

```jsx
import { BrowserRouter, Route, Routes } from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}
```

---

## **3. React 프로젝트 구조**
```
/my-react-app
├── /public
│   ├── index.html
│   ├── favicon.ico
│   ├── manifest.json
│   ├── robots.txt
│   ├── assets/
│
├── /src
│   ├── /components        # 재사용 가능한 UI 컴포넌트
│   ├── /pages             # 주요 페이지 컴포넌트
│   ├── /layouts           # 페이지 공통 레이아웃 관리
│   ├── /hooks             # 커스텀 훅 관리
│   ├── /store             # 상태 관리 (Redux, Zustand 등)
│   ├── /utils             # 유틸리티 함수
│   ├── /styles            # CSS, SCSS, Tailwind 설정
│   ├── /context           # React Context API를 활용한 전역 상태 관리
│   ├── App.js             # 메인 컴포넌트
│   ├── index.js           # React 엔트리 포인트
│   ├── routes.js          # React Router 설정 파일
│
├── .gitignore
├── package.json
├── README.md
├── yarn.lock / package-lock.json
└── webpack.config.js
```

---

## **4. React의 동작 흐름**
### **🔹 1) 애플리케이션 시작**
- `index.js`에서 `App.js`를 `ReactDOM.render()`를 통해 마운트

```jsx
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";

ReactDOM.createRoot(document.getElementById("root")).render(<App />);
```

---

### **🔹 2) 컴포넌트 렌더링 & Virtual DOM 생성**
- `App` 컴포넌트가 렌더링되면서 내부의 컴포넌트들이 **Virtual DOM에 생성됨**

```jsx
function App() {
  return (
    <div>
      <h1>리액트 동작 흐름</h1>
      <Counter />
    </div>
  );
}
```

---

### **🔹 3) Diffing Algorithm (변경 감지)**
- 사용자의 입력을 감지하여 **변경이 필요한 부분만 업데이트**.

```jsx
// 상태 변경 전
<h1>Count: 0</h1>

// 상태 변경 후
<h1>Count: 1</h1>
```

---

### **🔹 4) Reconciliation (조정)**
- **최소한의 DOM 업데이트 수행**
- **새로운 Virtual DOM과 기존 Virtual DOM의 차이점만 적용**

---

### **🔹 5) 실제 DOM 업데이트**
- React는 **가장 적은 DOM 업데이트를 수행**하여 성능을 향상시킴.

---

### **🔹 6) 상태 변경 및 재렌더링**
- `setState()` 또는 `useState()`를 사용하여 상태가 변경되면 **변경된 부분만 다시 렌더링됨**.

```jsx
const [count, setCount] = useState(0);

<button onClick={() => setCount(count + 1)}>+1</button>;
```

---

## **5. React의 주요 라이브러리 및 도구**
| 라이브러리 | 설명 |
|-----------|------|
| **React Router** | 클라이언트 사이드 라우팅 |
| **Redux** | 전역 상태 관리 (복잡한 상태) |
| **Zustand** | 경량 상태 관리 라이브러리 |
| **Axios / Fetch** | HTTP 요청 처리 |
| **Styled-components / Tailwind CSS** | CSS-in-JS 스타일링 |

---

## **6. React 성능 최적화 방법**
- `useMemo`, `useCallback`을 활용하여 불필요한 렌더링 방지
- `React.memo`를 사용하여 컴포넌트 메모이제이션
- 코드 스플리팅(Code Splitting) 적용 (`React.lazy`)
- Virtual DOM을 활용한 최적화

---

## **7. 결론**
- React는 **컴포넌트 기반**, **Virtual DOM**, **State 관리** 등을 통해 **빠르고 효율적인 UI 개발**을 제공.
- 동작 흐름을 이해하면 **최적화된 React 애플리케이션을 개발할 수 있음**.

---

## **📖 추천 공식 문서**
- [React 공식 문서](https://react.dev/)
- [Redux 공식 문서](https://redux.js.org/)
- [React Router 공식 문서](https://reactrouter.com/)

```

