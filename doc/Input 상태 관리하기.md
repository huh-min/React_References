# Input 상태 관리하기 (with. useState)

### InputSample.js

```javascript
import React from 'react';

function InputSample() {
  return (
    <div>
      <input />
      <button>초기화</button>
      <div>
        <b>값: </b>
      </div>
    </div>
  );
}

export default InputSample;
```

### App.js

```javascript
import React from 'react';
import InputSample from './InputSample';

function App() {
  return (
    <InputSample />
  );
}

export default App;
```

**onChange Event(e)**

: 이벤트에 등록하는 함수에서는 이벤트 객체`e`를 파라미터로 받아와서 사용할 수 있다. 

이 객체의 `e.target`은 이벤트가 발생한 DOM인 input DOM을 가리키게 된다.

이 DOM의 `value` 값, 즉 `e.target.value`를 조회하면 현재 input에 입력한 값이 무엇인지 알 수 있다.

이 값을 `useState`로 관리. 

### InputSample.js

```javascript
import React, { useState } from 'react';

function InputSample() {
  const [text, setText] = useState('');

  const onChange = (e) => {
    setText(e.target.value);
  };

  const onReset = () => {
    setText('');
  };

  return (
    <div>
      <input onChange={onChange} value={text}  />				** input의 상태를 관리할 때 input 태그의 value 값도 설정해주는 것이 중요
      <button onClick={onReset}>초기화</button>						 -> 상태가 바뀌었을 때 input의 내용도 업데이트 된다.
      <div>
        <b>값: {text}</b>
      </div>
    </div>
  );
}

export default InputSample;
```

# Input 상태 관리하기 (여러 개 Input 상태 관리하기)

: input에 `name`을 설정하고 이벤트가 발생하였을 때 이 값을 참조하는 것.

`useState`에서는 문자열이 아니라 객체 형태의 상태를 관리해주어야 한다.



### InputSample.js

```javascript
import React, { useState } from 'react';

function InputSample() {
  const [inputs, setInputs] = useState({
    name: '',
    nickname: ''
  });

  const { name, nickname } = inputs; // 비구조화 할당을 통해 값 추출

  const onChange = (e) => {
    const { value, name } = e.target; // 우선 e.target 에서 name 과 value 를 추출
    setInputs({
      ...inputs, // 기존의 input 객체를 복사한 뒤
      [name]: value // name 키를 가진 값을 value 로 설정
    });
  };

  const onReset = () => {
    setInputs({
      name: '',
      nickname: '',
    })
  };


  return (
    <div>
      <input name="name" placeholder="이름" onChange={onChange} value={name} />
      <input name="nickname" placeholder="닉네임" onChange={onChange} value={nickname}/>
      <button onClick={onReset}>초기화</button>
      <div>
        <b>값: </b>
        {name} ({nickname})
      </div>
    </div>
  );
}

export default InputSample;
```

**react state에서 객체를 수정해야할 때**

`inputs[name]=value;` 

이런식으로 수정하면 **안된다!**

**새로운 객체를 만들어서 새로운 객체에 변화를 주고, 이를 상태로 사용해주어야 한다**

```
const onChange = (e) => {			  // onChange 함수를 통해서 
    const { value, name } = e.target; // 우선 e.target 에서 name 과 value 를 추출
    setInputs({
      ...inputs, // 기존의 input 객체를 복사한 뒤
      [name]: value // name 키를 가진 값을 value 로 설정
    });
  };
```

### `...` 문법 (Spread)

: 배열이나 객체 개념에서 해당 개념의 내용을 모두 ''펼쳐서'' 기존 객체를 복사해주는 역할

(불변성을 지킨다!)

**=> 불변성을 지켜주어야만 React 컴포넌트에서 상태가 업데이트가 됐음을 감지할 수 있고, 이에 따라 필요한 리렌더링이 진행된다.**

#### 만약에 `inputs[name]=value` 이런식으로 기존 상태를 직접 수정하게 되면, 값을 바꿔도 리렌더링이 되지 않는다.

(컴포넌트 업데이트 성능 최적화와 매우 관련이 깊다.)





























