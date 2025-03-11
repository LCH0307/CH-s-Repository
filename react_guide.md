##### React (update 250311 17:33)

## React의 주요 개념
(1) 컴포넌트(Component)
- react는 ui를 컴포넌트 단위로 나누어 개발.
- 컴포넌트는 재사용 가능하며, 독립적인 상태를 가질 수 있음.
- 컴포넌트는 크게 함수형(Function Component) 과 클래스형(Class Component) 으로 나뉨.

1) 함수형 컴포넌트
```
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```
특징
- 가볍고 빠름
- React Hooks (ustState, useEffect 등) 사용 가능

2) 클래스형 컴포넌트
```
import React, { Component } from "react";

class Greeting extends Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}
```
특징
- state 와 라이프사이클 메서드 제공
- React 16.8 이후로 함수형 컴포넌트와 Hooks 사용 권장


(2) JSX (JavaScript XML)
- React에서는 UI를 HTML처럼 작성할 수 있는 JSX 문법을 사용
```
const element = <h1>Hello, world!</h1>;
```
JSX 특징
- JavaScript와 HTML을 결합하여 가독성 향상
- Babel을 통해 일반 JavaScript로 변환

(3) Props (속성)
- Props(속성) 은 부모 컴포넌트가 자식 컴포넌트에 데이터를 전달하는 방법
```
function User(props) {
  return <h1>이름: {props.name}</h1>;
}

function App() {
  return <User name="John Doe" />;
}
```
특징
- 부모 -> 자식 데이터 전달
- 읽기 전용 (변경 불가)

(4) State (상태)
- State(상태) 는 컴포넌트 내부에서 관리되는 데이터
```
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
특징
- 컴포넌트 내부에서 관리됨
- useState 훅을 사용하여 상태 변경 가능

(5) 이벤트 핸들링 (Event Handling)
- React에서는 이벤트를 통해 사용자 입력을 처리할 수 있음.
``` 
function ButtonClick() {
  const handleClick = () => {
    alert("버튼이 클릭되었습니다!");
  };

  return <button onClick={handleClick}>클릭</button>;
}
```
특징
- onClick, onChange 등의 이벤트 사용
- 함수형 컴포넌트에서는 함수형 업데이트 사용 권장

(6) 조건부 렌더링 (Conditional Rendering)
- React에서는 조건에 따라 UI를 다르게 렌더링할 수 있음.
```
function UserStatus(props) {
  return props.isLoggedIn ? <h1>환영합니다!</h1> : <h1>로그인해주세요.</h1>;
}
```
방법
- if 문 사용
- 삼항 연산자 (? :)
- && 논리 연산자 (isLoggedIn && <Component />)

(7) 리스트 렌더링 (List Rendering)
- 배열을 map() 함수와 함께 사용하여 리스트를 렌더링할 수 있음.
```
function NameList() {
  const names = ["Alice", "Bob", "Charlie"];

  return (
    <ul>
      {names.map((name, index) => (
        <li key={index}>{name}</li>
      ))}
    </ul>
  );
}
```
Key 값 필수 (key={index})
- 리스트의 각 항목에는 key 속성을 추가해야 성능 최적화 가능.

(8) 컴포넌트 생명주긱 (Lifecycle)
- 클래스형 컴포넌트에서는 라이프사이클 메서드가 존재함.
|-----|-----|
|생명주기 단계|메서드|
|마운드(Mount)|componentDidMount()|
|업데이트(Update)|componentDiUpdatie()|
|언마운트(Unmount)|componentwillUnmount()}
- 함수형 컴포넌트에서는 useEffect 를 사용하여 생명주기를 관리
```
import { useEffect } from "react";

function MyComponent() {
  useEffect(() => {
    console.log("컴포넌트가 마운트됨");

    return () => {
      console.log("컴포넌트가 언마운트됨");
    };
  }, []);

  return <div>안녕하세요!</div>;
}
```









## React의 디렉토리 구조

- node_modules : npm install을 하여 설치된 모듈들이 위치하는 폴더
- public : static 자원 폴더, 정적 파일들을 위한 폴더
- src : 리액트를 작업할 폴더

1) public 폴더

### index.html
- 가상 DOM을 위한 html 파일.(빈 껍데기 파일)
- 메인 프로그램인 index.js에 대응되는 것으로, HTML 템플릿 파일.
- 이 파일이 직접 표시되는 것은 아니고, index.js에 의해 읽어와서 렌더링된 경과가 표시됨.

### manifest.json
- 앱 스토어없이 기기의 홈화면에 설치할 수 있는 웹 사이트

2) src 폴더
index.js
- index.html과 비슷하게 메인 파일로, 여기서 html 템플릿 밑 javascript의 컴포넌트를 조합하여 렌더링하고 실제 표시함.

```
ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```
- ReactDom.render() 안에 보여주고 싶은 component를 넣음.

- index.html에서 아래 코드와 같이 'root'를 명시했기 때문에 사용할 수 있음
```
<div id="root"></div>
```

## App.js
- 컴포넌트를 정의하는 작업 파일로, 실제로 화면에 표시되는 내용 등은 여기에서 정의됨.

## App.css
- App.js에 대한 css 파일


