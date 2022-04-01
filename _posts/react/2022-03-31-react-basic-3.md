---
title:  "React 기초 정리 3"
excerpt: "React 앱 폴더 분석"
categories:
  - react
---
## src 폴더
index.js와 App.js 의 동작 방식이 중요

1. index.js
```js
    import React from 'react';
    import ReactDOM from 'react-dom';
    import './index.css';
    import App from './App';
    import reportWebVitals from './reportWebVitals';

    ReactDOM.render(
    <React.StrictMode>
    <App />
    </React.StrictMode>,
    document.getElementById('root')
    );
    
    reportWebVitals();
```
App.js 에서 생성된 리액트 코드를 index.js에서 불러온 후, public에 있는 index.html 의 'id = root'인 곳에다가 넣는 동작 수행
  - <App /> : html 코드를 사용, 모든 리액트 파일들은 전부 html 코드 처럼 사용할 수 있음
  - html 코드를 여러 개의 리액트 파일로 분할해서 작업 가능
2. App.js
```js
    import logo from './logo.svg';
    import './App.css';
    
    function App() {
        return (
            <div className="App">
                <header className="App-header">
                    <img src={logo} className="App-logo" alt="logo" />
                    <p>
                        Edit <code>src/App.js</code> and save to reload.
                    </p>
                    <a
                        className="App-link"
                        href="https://reactjs.org"
                        target="_blank"
                        rel="noopener noreferrer"
                    >
                        Learn React
                    </a>
                </header>
            </div>
        );
    }
    
    export default App;
```
React 코드를 생성하는 부분
1) App 클래스를 생성한 후, 리액트 컴포넌트를 상속 (-> 리액트 컴포넌트 메소드를 사용 가능)
   - render() = 리액트 컴포넌트 메소드
   - 화면에 html 뷰를 생성해주는 역할
   - return 값은 html 코드로 바뀌게됨
2) App 클래스를 export 문법을 이용해서 내보냄

