---
title:  "React 강의 정리 1"
excerpt: "React 전반적인 특징"
categories:
  - react
---
### 라이브러리 vs 프레임워크
 - 라이브러리는 개발을 위한 도구 모음
 - 프레임워크는 기반 구조까지 잡혀있음.
 - 라이브러리는 공구
 - 프레임워크는 공장

### DOM
Document Object Model
문서를 논리 트리로 표현한다.

### 순수 자바스크립트
특정 라이브러리를 사용하지 않은 자바스크립트

### 코드 샌드박스
codesandbox.io
리액트 코드 시험 가능

### CDN 
Content Delivery Network
웹에서 사용되는 다양한 리소스(컨텐츠)를 저장, 제공하는 시스템
React와 ReactDOM 모두 CDN을 통해 사용할 수 있음.
```js
<script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
```
### JSX
```js
const element = <h1>Hello, world!</h1>;
```
javascript 확장문법
자바스크립트와 html 중간영역

### Babel
JavaScript Compiler
JSX는 Babel이 이해하는 문법. JS에서는 이해하지 못함. 
JSX 사용 위해서는 Babel 주입 필요 

```js
<script>
    const rootElement = document.getElementById("root");
    const element = React.createElement("h1", {
      className: "title",
      children: ["hello1", " hello2"]
    });
    ReactDOM.render(element, rootElement);
</script>
```

type을 text/babel로 설정하면 babel에서 컴파일해줌.
```js
<script type="text/babel">
    const rootElement = document.getElementById("root");
    const element = <h1 className="title">hello1 hello2</h1>;
    ReactDOM.render(element, rootElement);
</script>
```