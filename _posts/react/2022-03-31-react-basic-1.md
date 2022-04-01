---
title:  "React 기초 정리 1"
excerpt: "React 전반적인 특징"
categories:
  - react
---
## React란?

1. 프론트엔드 진영에는 3개의 라이브러리 OR 프레임워크가 경쟁 중
   - React, Angular, Vue 
2. React는 페이스북이 만든 사용자 UI 구축을 위한 라이브러리

## React 특징

1. JSX 문법 
   - JSX는 자바스크립트 안에서 HTML 문법을 사용해서 view를 구성할 수 있게 도와주는 자바스크립트 문법
   - Nested Element: 모든 JSX 형태의 코드는 container element 안에 포함시켜야 한다. 무언가로 감싸져야만 코드가 제대로 작동함.
```js
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
   - 컴포넌트는 자바스크립트 클래스. 참조 시 <컴포넌트명/>형식으로 쓰임. 소문자로 쓰면 <div>나 <span> 같은 HTML 태그로 해석되기 때문에 반드시 대문자로 시작해야함.


3. Virtual DOM
   - DOM 자체가 추상화 개념인데, 거기에 한번 더 추상화를 한 것이 가상 DOM
   - 가상 DOM을 사용하는 이유는, 실제 DOM을 직접 변경할 수는 있지만, 그 작업이 굉장히 값비싼 작업이기 때문에, 가상 돔에서 미리 최적화
   ![Alt text](https://miro.medium.com/max/1400/1*Vvi4_infsE8Q0uAStZmiWw.png)

## ES6 클래스 (Class)
- ES6에 새로 도입된 문법. (참고로 React.createClass() 메소드를 통해 일반적인 방법으로 컴포넌트를 만들 수도 있다.)
React를 사용할 때는 컴포넌트를 class 또는 함수로 정의할 수 있음. React 컴포넌트 class를 정의하려면 React.Component를 상속받아야 함.
```js  
  //ES6 class 예시 - Codelab 컴포넌트 만들기
  class Codelab extends React.Component {
    render() {
      return(
        <div>Codelab</div>
      );
    }
  }
```