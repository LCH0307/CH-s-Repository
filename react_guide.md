비전공자도 쉽게 이해할 수 있고 전공자도 참고할 수 있는 React의 개념과 동작 원리, 그리고 프로젝트 폴더 구조

---

# 📌 React 개념 및 프로젝트 구조 정리

React는 Facebook(현 Meta)에서 개발한 **UI 라이브러리**이다. 웹사이트를 작은 단위(컴포넌트)로 나누어 관리하고, 빠르게 화면을 업데이트할 수 있도록 도와준다. 주요 특징은 컴포넌트 기반 개발, 가상 DOM, 단방향 데이터 흐름, 상태 관리 등이다.

---

## 1. React란?

React는 웹사이트의 각 요소(버튼, 텍스트, 이미지 등)를 독립적인 **컴포넌트**로 만들어 재사용하고, 관리하기 쉽게 한다.  
또한, **Virtual DOM(가상 돔)** 기술을 사용해 변경된 부분만 업데이트하여 빠르게 렌더링되도록 최적화한다.  
이와 함께 단방향 데이터 흐름(부모 → 자식)을 통해 데이터 전달을 명확히 하며, 상태(State)를 관리하여 사용자의 동작에 따라 UI가 동적으로 바뀌게 한다.

---

## 2. React의 주요 개념

### 2.1 컴포넌트 기반 개발 (Component-Based Architecture)
- 웹사이트를 작은 재사용 가능한 단위(컴포넌트)로 나눈다.
- 컴포넌트는 독립적으로 관리되며, 여러 곳에서 반복해서 사용할 수 있다.

**예제: 버튼 컴포넌트**
```jsx
function Button({ label }) {
  return <button>{label}</button>;
}

function App() {
  return <Button label="클릭하세요!" />;
}
```
컴포넌트 하나를 만들어두면 동일한 요소를 여러 번 사용하여 코드 중복을 줄이고 유지보수를 쉽게 한다.

---

### 2.2 Virtual DOM (가상 DOM)
- React는 실제 DOM을 직접 수정하지 않고 메모리 상의 **Virtual DOM**에서 변경 사항을 계산한다.
- 새로운 Virtual DOM과 기존 Virtual DOM을 비교(Diffing Algorithm)하여 **변경된 부분만 실제 DOM에 반영(Reconciliation)** 한다.
- 이 방식은 불필요한 렌더링을 줄여 성능을 향상시킨다.

**예제: 상태 변경 시 일부만 업데이트**
```jsx
const [count, setCount] = useState(0);
<button onClick={() => setCount(count + 1)}>+1</button>;
```
버튼을 클릭하면 count 값이 변경되고, React는 변경된 부분만 실제 화면에 업데이트한다.

---

### 2.3 단방향 데이터 흐름 (One-way Data Flow) / 데이터 통신 (Props)
- 데이터는 **부모 컴포넌트에서 자식 컴포넌트로만 전달된다**. 이를 **props**라 하며, 단방향 데이터 바인딩을 의미한다.
- 자식은 전달받은 데이터를 읽기만 하고 직접 수정할 수 없다.
- 만약 자식이 부모의 데이터를 변경해야 할 경우, 부모가 상태(State)를 관리하고 자식에게 변경 함수(callback)를 전달한다.

**예제: 단방향 데이터 전달 (Props)**
```jsx
function Child({ message }) {
  return <h1>{message}</h1>;
}

function Parent() {
  return <Child message="Hello from Parent!" />;
}
```

**예제: 자식이 부모의 상태 변경 요청**
```jsx
import { useState } from "react";

function Child({ increase }) {
  return <button onClick={increase}>+1 증가</button>;
}

function Parent() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>현재 카운트: {count}</p>
      <Child increase={() => setCount(count + 1)} />
    </div>
  );
}
```
자식은 버튼 클릭 시 전달받은 `increase` 함수를 호출하고, 부모는 그 함수 내에서 상태를 변경한다.

---

### 2.4 상태 관리 (State Management)
- **State**는 컴포넌트 내부에서 데이터를 저장하고 변경할 수 있는 구조이다.
- `useState` 같은 React Hooks를 사용하면 상태가 변경될 때마다 해당 부분만 재렌더링된다.

**예제: Counter 컴포넌트**
```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>현재 카운트: {count}</p>
      <button onClick={() => setCount(count + 1)}>+1</button>
    </div>
  );
}
```
버튼 클릭 시 count 값이 증가하고, 변경된 값이 화면에 자동 반영된다.

---

### 2.5 React Hooks
- **Hooks**는 함수형 컴포넌트에서 상태 관리와 생명주기 기능을 사용할 수 있도록 도와주는 함수 모음이다.
- 대표적으로 `useState`, `useEffect`, `useReducer` 등이 있다.
- **useEffect**는 컴포넌트가 렌더링된 후 특정 작업(예: 데이터 가져오기, 구독 설정 등)을 수행하는 데 사용된다.

**예제: useEffect 사용**
```jsx
import { useState, useEffect } from "react";

function DataFetcher() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch("https://api.example.com/data")
      .then((response) => response.json())
      .then((result) => setData(result));
  }, []); // 빈 배열을 넣어 최초 렌더링 시 한 번 실행

  return <div>{data ? JSON.stringify(data) : "로딩 중..."}</div>;
}
```
Hooks를 사용하면 클래스형 컴포넌트의 복잡한 생명주기 메서드 없이도 유연하게 기능을 구현할 수 있다.

---

### 2.6 스타일링 방법
React에서는 여러 가지 방법으로 스타일(CSS)을 적용할 수 있다.

#### 2.6.1 일반 CSS 파일 사용
별도의 CSS 파일을 만들어 `className`을 이용해 스타일을 적용한다.
```css
/* styles.css */
.button {
  background-color: blue;
  color: white;
}
```
```jsx
import "./styles.css";

function Button() {
  return <button className="button">클릭</button>;
}
```

#### 2.6.2 인라인 스타일 적용
컴포넌트 내부에서 직접 스타일을 지정할 수 있다.
```jsx
function Button() {
  return <button style={{ backgroundColor: "blue", color: "white" }}>클릭</button>;
}
```

#### 2.6.3 CSS-in-JS (Styled-Components)
JavaScript 코드 내에서 스타일을 작성하는 방법이다. 별도의 라이브러리(styled-components 등)를 사용한다.
```bash
npm install styled-components
```
```jsx
import styled from "styled-components";

const StyledButton = styled.button`
  background-color: blue;
  color: white;
`;

function App() {
  return <StyledButton>클릭</StyledButton>;
}
```
이 방식은 컴포넌트와 스타일을 한 파일에 작성할 수 있어 관리가 용이하다.

---

## 3. React 프로젝트 폴더 구조

React 프로젝트는 다음과 같이 여러 폴더와 파일로 구성된다. 각 폴더는 특정 역할을 수행하여 프로젝트를 체계적으로 관리할 수 있게 한다.

```
/my-react-app
├── /public                 // 정적인 파일 (HTML, 이미지 등)
│   ├── index.html          // React가 실행되는 HTML 파일
│   ├── favicon.ico         // 아이콘 파일
│   ├── manifest.json       // 웹 애플리케이션 설정
│   ├── robots.txt          // 검색 엔진 크롤링 설정
│   ├── assets/             // 기타 정적 파일
│
├── /src                    // React 소스 코드
│   ├── /components         // 재사용 가능한 UI 컴포넌트
│   ├── /pages              // 주요 페이지 컴포넌트
│   ├── /layouts            // 페이지 공통 레이아웃 관리
│   ├── /hooks              // 커스텀 Hooks 관리 (반복되는 로직을 함수화)
│   ├── /store              // 전역 상태 관리 (Redux, Zustand 등)
│   ├── /utils              // 유틸리티 함수 (데이터 포맷, API 호출 등)
│   ├── /styles             // CSS, SCSS, Tailwind 등 스타일 파일
│   ├── /context            // React Context API를 활용한 전역 상태 관리
│   ├── App.js              // 메인 컴포넌트 (전체 앱 구조)
│   ├── index.js            // React 엔트리 포인트 (DOM에 마운트)
│   ├── routes.js           // React Router 설정 파일
│
├── .gitignore              // Git에서 제외할 파일 목록
├── package.json            // 프로젝트 설정 및 종속성 목록
├── README.md               // 프로젝트 설명 및 실행 방법
├── yarn.lock or            // 패키지 버전 관리 파일
│    package-lock.json     
└── webpack.config.js       // Webpack 설정 파일 (필요에 따라 구성)
```

### 각 폴더의 역할
- **public/**  
  정적인 파일과 HTML 템플릿이 위치한다.  
- **src/components/**  
  버튼, 헤더, 푸터 등 재사용 가능한 UI 컴포넌트들을 모아둔다.  
- **src/pages/**  
  각 페이지별 컴포넌트를 구성하며, React Router와 연동되어 화면 전환을 관리한다.  
- **src/layouts/**  
  모든 페이지에서 공통적으로 사용하는 레이아웃(헤더, 푸터 등)을 관리한다.  
- **src/hooks/**  
  자주 사용되는 로직을 재사용 가능한 함수(Hook)로 만들어 관리한다.  
- **src/store/**  
  전역 상태 관리 라이브러리(Redux, Zustand 등)를 이용해 복잡한 상태를 중앙에서 관리한다.  
- **src/utils/**  
  여러 컴포넌트에서 공통으로 사용되는 유틸리티 함수(예: 날짜 포맷, API 호출 함수 등)를 작성한다.  
- **src/styles/**  
  CSS 파일, SCSS, 또는 Tailwind 설정 파일 등을 관리하여 전체적인 스타일을 통일시킨다.  
- **src/context/**  
  Context API를 활용하여 전역 상태를 간단하게 관리하는 경우, 관련 코드를 모아둔다.  
- **src/App.js**  
  애플리케이션의 최상위 컴포넌트로, 전체 구조와 라우팅 등을 정의한다.  
- **src/index.js**  
  React 애플리케이션의 시작점이며, `ReactDOM.createRoot`를 통해 `App` 컴포넌트를 HTML의 특정 요소에 마운트한다.  
- **src/routes.js**  
  React Router 설정을 통해 여러 페이지로의 경로를 정의한다.

---

## 4. React의 동작 흐름

### 4.1 애플리케이션 실행
- `index.js`에서 React 애플리케이션이 시작된다.
- `App.js` 컴포넌트를 `ReactDOM.createRoot`를 통해 HTML의 `root` 요소에 렌더링한다.

**예제: index.js**
```jsx
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";

ReactDOM.createRoot(document.getElementById("root")).render(<App />);
```

---

### 4.2 컴포넌트 렌더링 및 Virtual DOM 생성
- `App.js` 내의 여러 컴포넌트들이 렌더링되며, 이에 따라 **Virtual DOM**이 생성된다.
- Virtual DOM은 메모리 상에 존재하며, 실제 DOM과 비교할 준비를 한다.

**예제: App.js**
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

### 4.3 변경 감지 및 실제 DOM 업데이트
- 사용자의 상호작용(예: 버튼 클릭)으로 상태(State)가 변경되면 새로운 Virtual DOM이 생성된다.
- React는 이전 Virtual DOM과 새 Virtual DOM을 비교(Diffing)하여 **변경된 부분만 실제 DOM에 업데이트**한다.
- 이 과정을 **Reconciliation**이라 하며, 업데이트에 필요한 최소한의 작업만 수행하여 성능을 최적화한다.

**예제: 상태 변경**
```jsx
const [count, setCount] = useState(0);
<button onClick={() => setCount(count + 1)}>+1</button>;
```

---

### 4.4 이벤트 처리와 상태 업데이트
- 사용자가 이벤트(예: 클릭)를 발생시키면, 해당 이벤트 핸들러가 실행되어 상태가 변경된다.
- React는 변경된 상태에 따라 해당 컴포넌트 또는 자식 컴포넌트만 재렌더링하여 효율적으로 화면을 업데이트한다.

**예제: 버튼 클릭 이벤트**
```jsx
function Button() {
  function handleClick() {
    alert("버튼이 클릭되었습니다!");
  }

  return <button onClick={handleClick}>클릭</button>;
}
```

---

## 5. 추가 기능 및 성능 최적화

### 5.1 조건부 렌더링 (Conditional Rendering)
- 특정 조건에 따라 컴포넌트를 표시하거나 숨길 수 있다.
- `if` 문, `&&` 연산자, 삼항 연산자를 사용하여 조건부로 렌더링을 제어한다.

**예제: 삼항 연산자 사용**
```jsx
function LoginButton({ isLoggedIn }) {
  return <button>{isLoggedIn ? "로그아웃" : "로그인"}</button>;
}
```

---

### 5.2 리스트 렌더링 (List Rendering)
- 배열 데이터를 `map()` 함수를 통해 컴포넌트로 변환하여 화면에 표시한다.
- 각 리스트 항목에는 고유한 `key` 값을 부여하여 성능 최적화 및 상태 관리에 도움을 준다.

**예제: 이름 목록 렌더링**
```jsx
function NameList() {
  const names = ["철수", "영희", "민수"];

  return (
    <ul>
      {names.map((name, index) => (
        <li key={index}>{name}</li>
      ))}
    </ul>
  );
}
```

---

### 5.3 성능 최적화 방법
- **useMemo**와 **useCallback**: 컴포넌트의 불필요한 재렌더링을 방지.
- **React.memo**: 컴포넌트를 메모이제이션하여 props가 변경되지 않으면 재렌더링하지 않음.
- **코드 스플리팅 (Code Splitting)**: `React.lazy`와 `Suspense`를 사용하여 초기 로딩 속도를 향상.
- Virtual DOM 기반 업데이트를 통해 변경된 부분만 렌더링하여 성능을 극대화.

---

## 6. 결론

React는 **컴포넌트 기반**으로 웹사이트를 만들고 관리하는 데 매우 효과적이다.  
- **컴포넌트**를 사용하여 코드의 재사용성과 유지보수를 용이하게 하고,  
- **Virtual DOM**을 통해 화면 업데이트를 최적화하며,  
- **단방향 데이터 흐름(Props)**과 **상태 관리(State)**를 통해 복잡한 UI 동작을 쉽게 제어할 수 있다.  
- 또한, 다양한 **Hooks**, **Context API**, **Redux 등**을 활용하여 확장성이 뛰어난 웹 애플리케이션을 구축할 수 있다.

프로젝트 폴더 구조는 기능별로 체계적으로 구성되어 있어, 비전공자도 쉽게 이해할 수 있으며 전공자도 참고하여 확장 및 유지보수가 용이하다.

---

## 📖 추천 공식 문서

- [React 공식 문서](https://react.dev/)
- [Redux 공식 문서](https://redux.js.org/)
- [React Router 공식 문서](https://reactrouter.com/)

