
title:  "React 기초 정리 4"
excerpt: "React State & Props"
categories:
  - react
---
## State
- State는 하나의 컴포넌트가 가질 수 있는 변경 가능한 데이터
- JSX내부에 {this.state.stateName}
- 초기값 설정이 필수, 생성자(constructor) 안에서 this.state ={}으로 설정.
- 다만 렌더링 된 다음엔 this.state ={}는 절대 재사용하지 말 것.
- 렌더링 이후에 값을 수정할 때에는 컴포넌트 내부에서 this.setState({})로 변경이 가능하다. 달리 말하면, 생성자에서는 사용이 안된다는 뜻. 성능이 떨어짐.
```js
class Counter extends React.Component {

//초기값 설정
   constructor(props) { /*props는 Counter가 만들어질 때 전달받을 매개변수*/
      super(props); /*super를 통해 React.Component를 먼저 실행해 접근성을 확보*/
      this.state = {
         value: 0
      }
      this.handleClick = this.handleClick.bind(this);/*this binding 해주기*/
   }

//버튼이 클릭될 때 실행될 메소드
   handleClick() {
      this.setState({ /*binding을 해주지 않으면 this가 뭔지 모른다!*/
         value: this.state.value + 1
      })
   }


   render() {
      return (
              <div>
                 <h2>{this.state.value}</h2>
                 <button onClick={this.handleClick}>Press Me</button>
              </div>
      )
   }
}

class App extends React.Component {
   render() {
      return (
              <Counter/>
      );
   }
};

ReactDOM.render(
        <App></App>,
        document.getElementById("root")
);
```

## Props
- 컴포넌트 내부의 Immutable data, 변화하지 않는 데이터(정적인 화면구성)를 처리할 때 사용됨.
- 상위 컴포넌트에서 하위 컴포넌트로 데이터를 넘겨줄 때 사용.
- JSX 내부에 {this.props.propsName}
- 컴포넌트를 사용할 때, HTML태그에 값을 전달하듯 <> 괄호 안에 propsName = "value(값)"형식으로 작성.
- this.props.children은 모든 컴포넌트가 기본적으로 갖고있는 props로서, <컴포넌트명></컴포넌트명> 사이의 값이 들어감.
```js
- //Codelab컴포넌트 (하위)
  class Codelab extends React.Component {
    render() {
      return (
        <div>
          <h1>Hello {this.props.name}</h1> /*velopert*/
          <div>{this.props.children}</div> /*여기에 보여지는 것이 바로 props.children*/
        </div>
       );
    }
  }

   //App 컴포넌트 (상위)
   class App extends React.Component {
       render() {
         return (
           <Codelab name="velopert">여기에 보여지는 것이 바로 props.children</Codelab>
         );
       }
   }
   
   ReactDOM.render(<App/>, document.getElementById('root'));
```