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
