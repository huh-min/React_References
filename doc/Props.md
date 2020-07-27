## Props

: Properties의 줄임말. 우리가 어떠한 값을 컴포넌트에게 전달해줘야 할 때 props 사용!

**구조 이해 하기**

```
[App.js]

import React from 'react';
import Hello from './Hello';

function App() {
  return (
    <Hello name="react" />
  );
}

export default App;
```

: App.js에서 Hello 컴포넌트의 name props를 사용하는 모습.

```
[Hello.js]

import React from 'react';

function Hello(props) {
  return <div>안녕하세요 {props.name}</div>
}

export default Hello;
```

: Hello.js 에서 function형 호출에서 파라미터를 props로 설정 => 이를 통해 컴포넌트에게 Props 전달

(이때 Props는 객체 형태로 전달되며 만약 naem 값을 조회하고 싶다면 props.name을 조회하면 된다.)



**고려해봐야할 부분**은 Hello.js의 Props중 naem을 App.js에서 정의해주었고, 

이 값을 가져오는 문법이 파라미터로 Props를 받는 **매개** 역할 &  {props.name}로 **조회**하게 한다 .



## 객체 비구조화 할당 방식 (구조분해 문법)

: 객체 안에 있는 값을 추출해서 변수 혹은 상수로 바로 선언.

```
example.1

const object = { a: 1, b: 2 };

const { a, b } = object;

console.log(a); // 1
console.log(b); // 2
```

object 객체 안에는 a, b (key) 와 1,2 (value) 가 존재.

이 객체 안에 있는 값만 추출하여 object 변수로 선언

```
example.2

const object = { a: 1, b: 2 };

function print({ a, b }) {
  console.log(a);
  console.log(b);
}

print(object);
```

**React 에서 객체 비구조화 할당 방식**

```
원본 Code

import React from 'react';

function Hello(props) {
  return <div style={{ color: props.color }}>안녕하세요 {props.name}</div>
}

export default Hello;
```

: color props에 접근하기 위해 props.color로 조회

```
변화 Code

import React from 'react';

function Hello({ color, name }) {
  return <div style={{ color }}>안녕하세요 {name}</div>
}

export default Hello;
```

: 파라미터에서 객체를 가져온 모습이며, JSX 내부에서 사용할 때 color, name으로 조회가 가능하다.



- defaultProps로 기본값 설정

  : 컴포넌트에 props를 지정하지 않았을 때 기본적으로 사용할 값을 설정하고 싶다면 컴포넌트에 ```defaultProps```라는 값을 설정.

  ```
  import React from 'react';
  
  function Hello({ color, name }) {
    return <div style={{ color }}>안녕하세요 {name}</div>
  }
  
  Hello.defaultProps = {
    name: '이름없음'
  }
  
  export default Hello;
  ```

  : Hello.js의 defaultProps 중 name을 이름없음으로 설정한 모습.

  

- Props.children

  : 컴포넌트 태그 사이에 넣은 값을 조회하고 싶을 때 ```Props.children``` 를 조회.

  ```
  Ex)
  
  import React from 'react';
  
  function Wrapper() {
    const style = {
      border: '2px solid black',
      padding: '16px',
    };
    return (
      <div style={style}>
  
      </div>
    )
  }
  
  export default Wrapper;
  ------------------------------------------------------------
  import React from 'react';
  import Hello from './Hello';
  import Wrapper from './Wrapper';
  
  function App() {
    return (
      <Wrapper>
        <Hello name="react" color="red"/>
        <Hello color="pink"/>
      </Wrapper>
    );
  }
  
  export default App;
  ```

  : App.js에서 function형으로 컴포넌트를 호출하여 Wrapper를 return하고 있다.

  Wrapper 태그 내부에는 Hello 컴포넌트가 존재하는데, 위의 코드대로 출력을 한다면 Hello 컴포넌트가 보이지 않는다.

  **이 때** Wrapper 컴포넌트의 태그 사이에 넣은 값을 조회하기 위한 것이 ```props.children```이다.  

  수정된 코드는 다음과 같다.

  ```
  import React from 'react';
  
  function Wrapper({ children }) {
    const style = {
      border: '2px solid black',
      padding: '16px',
    };
    return (
      <div style={style}>
        {children}
      </div>
    )
  }
  
  export default Wrapper;
  ```

  