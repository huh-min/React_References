# #useState

**: 컴포넌트에서 보여줘야 하는 내용이 사용자 인터렉션에 따라 바뀌어야 할 때 사용**

- React 16.8 이전 버전에서는 함수형 컴포넌트에서는 상태를 관리할 수 없었으나,

  `Hooks`라는 기능이 도입되면서 함수형 컴포넌트에서도 상태를 관리할 수 있어짐.

- useState 도 Hooks 중 하나!



### Counter.js

```
import React from 'react';

function Counter() {
  return (
    <div>
      <h1>0</h1>
      <button>+1</button>
      <button>-1</button>
    </div>
  );
}

export default Counter;
```

### App.js

```
import React from 'react';
import Counter from './Counter';

function App() {
  return (
    <Counter />
  );
}

export default App;
```



### 이벤트 설정

: Counter에서 버튼이 클릭되는 이벤트가 발생했을 때 특정 함수가 호출되도록 설정해보자.

### Counter.js

```
import React from 'react';

function Counter() {
  const onIncrease = () => {						//onIncrease , onDecrease는 화살표 함수로 구현.
    console.log('+1')
  }
  const onDecrease = () => {
    console.log('-1');
  }
  return (
    <div>
      <h1>0</h1>
      <button onClick={onIncrease}>+1</button>
      <button onClick={onDecrease}>-1</button>
    </div>
  );
}

export default Counter;
```

**화살표 함수**

: 함수를 선언하는 방식 중 또 다른 방법.

```
const add = (a, b) => {
  return a + b;
};

console.log(add(1, 2));
```

`function` 키워드 대신에 `=>` 문자를 사용해서 함수를 구현.

화살표 좌측에는 `함수의 파라미터` 화살표 우측에는 `코드 블록`

그런데 만약 위와 같이 코드 블록 내부에서 바로 return을 하는 경우는 다음과 같이 줄여서 쓸 수 있다.

```
const add = (a, b) => a + b;
console.log(add(1, 2));
```

---

함수를 만들고 button의 `onClick`으로 각 함수를 연결.

React에서 Element에 Event를 설정해줄 때에는 `onEventName = {실행하고 싶은 함수}` 형태로 해준다.

`onClick={onIncrease()}` 이렇게 하면 함수를 실행하는 형태라서 잘못된 것.

(이렇게 하면 렌더링되는 시점에서 함수가 호출됨.)



 ### 동적인 값 끼얹기

: 컴포넌트에서 동적인 값을 **State**라고 한다.

`useState`를 통해서 컴포넌트의 상태를 관리!



### Counter.js

```
import React, { useState } from 'react';			// React package에서 useState라는 함수를 불러와 준다.

function Counter() {
  const [number, setNumber] = useState(0);			// useState를 사용할 때 상태의 기본값을 파라미터로 넣어서 호출
													// 이 함수를 호출하면 배열이 반환
  const onIncrease = () => {						// 여기서 첫번째 원소는 현재 상태, 두번째 원소는 Setter 함수이다.
    setNumber(number + 1);							// Setter 함수는 파라미터로 전달 받은 값을 최신 상태로 설정해준다.
  }

  const onDecrease = () => {
    setNumber(number - 1);
  }

  return (
    <div>
      <h1>{number}</h1>								 
      <button onClick={onIncrease}>+1</button>
      <button onClick={onDecrease}>-1</button>
    </div>
  );
}

export default Counter;
```

위 예시에서 useState의 기본값은 0으로 해주었다.

첫번째 원소 number는 현재 상태

두번째 원소 SetNumber는 Setter 함수



### 함수형 업데이트 (컴포넌트 최적화)

기존에는 Setter 함수를 사용할 때, 업데이트하고 싶은 새로운 값을 파라미터로 넣어주었다.

그 대신에 기존 값을 어떻게 업데이트할 지에 대해서 함수로 등록을 하는 방식으로도 값을 업데이트할 수 있다.

### Counter.js

```
import React, { useState } from 'react';

function Counter() {
  const [number, setNumber] = useState(0);

  const onIncrease = () => {
    setNumber(prevNumber => prevNumber + 1);
  }

  const onDecrease = () => {
    setNumber(prevNumber => prevNumber - 1);
  }

  return (
    <div>
      <h1>{number}</h1>
      <button onClick={onIncrease}>+1</button>
      <button onClick={onDecrease}>-1</button>
    </div>
  );
}

export default Counter;
```



prevNumber처럼 변수를 임의로 정하여 값을 업데이트하는 방식 설정.

