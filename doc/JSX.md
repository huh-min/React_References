```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(<App />, document.getElementById('root'));
```

**ReactDOM.render**

: 브라우저에 있는 실제 DOM 내부에 리액트 컴포넌트를 렌더링 하겠다.

위의 코드에서는 ```ID```가 ```root``` 인 DOM을 선택.

React 컴포넌트가 렌더링 될 때에는 렌더링된 결과물이 위 div 내부에 렌더링 된다.



***JSX** 기본 규칙

1. JSX란?

   : react에서 생김새를 정의할 때  사용하는 문법. Java Script XML

   - react 컴포넌트 파일에서 XML 형태로 코드를 작성하면 babel이 JSX를 Javascript로 변환해 준다.

2. 태그 꼭 닫아주기
   - 태그와 태그 사이에 내용이 들어가지 않을 때는 **SelfClosing** 태그라는 것을 사용.
3. 두 개 이상의 태그는 무조건 하나의 태그로 감싸져야 한다.
   - **Fragment** '<>' 사용!
     - 태그를 이름 없이 작성한 형태. 브라우저 상에서 별도의 엘리먼트로 나타나지 않음!

4. JSX 안에 자바스크립트 값 사용 방식

```
function App() {
  const name = 'react';
  return (
    <>
      <Hello />
      <div>{name}</div>
    </>
  );
}
```

- name이라는 변수를 보여주기 위하여 return에서는 {name} 처리를 해준다.

5. Style & className

   - **JSX**에서 태그에 style 과 CSS class를 설정하는 방법은 HTML 에서 설정하는 방법과 다르다!

   - 인라인 스타일은 객체 형태로 작성. 이 때 ```background-color```와 같은 ```-```로 구분하는 것은 ```backgroundColor``` 처럼 camelCase로 네이밍해줘야한다.

   - ```
     function App() {
       const name = 'react';
       const style = {
         backgroundColor: 'black',
         color: 'aqua',
         fontSize: 24, // 기본 단위 px
         padding: '1rem' // 다른 단위 사용 시 문자열로 설정
       }
     
       return (
         <>
           <Hello />
           <div style={style}>{name}</div>
         </>
       );
     }
     ```

   -  CSS class를 설정할 떄에는 ```class=```가 아닌 ```className=```으로 설정 해줘야 한다.

   - ```javascript
     return (  //App.js
         <>
           <Hello />
           <div style={style}>{name}</div>
           <div className="gray-box"></div>
         </>
     ```

     ```
     .gray-box {  //App.css
       background: gray;
       width: 64px;
       height: 64px;
     }
     ```

     

6. 주석

   : JSX 내부의 주석은 ```{/* form */} ``` 의 형태로 작성한다.

   추가로 열리는 태그 내부에서는 ```//이런형태``` 로 주석 작성이 가능하다.

