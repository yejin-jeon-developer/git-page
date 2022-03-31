---
title:  "React 기초 정리"
excerpt: "React 사용법"
categories:
  - react
---
React 시작하기
1. 리액트를 작업할 때 webpack 이나 parcel 같은 번들러를 이용해서 작업
2. 리액트 파일은 JSX 문법으로 작성되거나 최신 JS 문법으로 작성되기 때문에, babel 을 사용해서 브라우저 호환성을 생각해야함

React 특징
1. JSX 문법 
   - JSX는 자바스크립트 안에서 HTML 문법을 사용해서 view를 구성할 수 있게 도와주는 자바스크립트 문법
```
class HelloMessage extends React.Component {
  render() {
    return (
      <div>
        Hello {this.props.name}
      </div>
    );
  }
}
```

2. Component 기반
   - 리액트는 컴포넌트 기반 라이브러리
   - 코드의 재사용성과 유지보수성을 증가


3. Virtual DOM
   - DOM 자체가 추상화 개념인데, 거기에 한번 더 추상화를 한 것이 가상 DOM
   - 가상 DOM을 사용하는 이유는, 실제 DOM을 직접 변경할 수는 있지만, 그 작업이 굉장히 값비싼 작업이기 때문에, 가상 돔에서 미리 최적화
   ![Alt text](https://miro.medium.com/max/1400/1*Vvi4_infsE8Q0uAStZmiWw.png)