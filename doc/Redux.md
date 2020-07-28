# Redux

1. 하나의 객체(상태)를 가진다 => 애플리케이션의 복잡도를 낮춘다

State={}

한 곳에 집중적으로 데이터를 관리하면 조금 더 효율적일 수 있음.

2. 외부로부터 철저하게 차단! 

   => 담당 함수를 통해서만 데이터를 사용/전송 가능!

   ex. dispatch

Module Reloading

: 코드를 작성하면 자동으로 애플리케이션에 반영함.



**애플리케이션의 State를 예측 가능하게 만드는 것이 목적**







Store (은행)     			`var store = Redux.createStore(reducer);`

: 정보가 저장되는 곳

- state : 직접 접속하는 것이 금지 및 불가함

  

- reducer(함수) : state를 가공하는 가공자

  

- dispatch(함수)           `store.dispatch({type:'create', payload:{title.title, desc:desc}});`   

  **: 여기서 객체가 Action & Action이 dispatch에게 전달**

  - dispatch가 reducer를 호출할 때 두 개의 값을 전달한다.

    - store의 현재 state 값을 전달

    - action의 Data(객체)를 전달

      ```
      function reducer(state, action){ 			//파라미터로 현재 state와 disaptch를 통해서 보낸 action을 공급
      	if(action.type === 'create'){
      	var newContents = oldState.contents.concat();
      	var newMaxId = oldState.maxId+1;
      	newContents.push({id:newMaxId, title:action.})
      	}
      }
      ```

      

  -  subscribe를 이용하여 render 함수를 호출

    

- subscribe(함수) : store의 state값이 바뀔 때마다 render 함수를 호출하는 역할 => 알아서 UI가 업데이트될 수 있다. 									`store.subscribe(render);`  :  render함수를 subscribe에 등록한 코드

  

- getState(함수) : store에 있는 state에 접근하여 render에게 state 정보를 넘겨주는 역할



render

: state를 참조하여 UI를 만든다. 우리가 짤 코드 

```
function render(){
		var state = store.getState();			//store에서 state를 get 한다!
		//...
		document.querySelector('#app').innerHTML =		//innerHTML을 통해서 실제로 UI를 표현하는 부분
		<h1>web</h1>
		....
}
```

