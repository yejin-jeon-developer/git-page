---
title:  "React 기초 정리"
excerpt: "React 전반적인 특징"
categories:
  - react
---
React란?
1. 프론트엔드 진영에는 3개의 라이브러리 OR 프레임워크가 경쟁 중
   - React, Angular, Vue 
2. React는 페이스북이 만든 사용자 UI 구축을 위한 라이브러리

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