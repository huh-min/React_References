# Javascript 비동기 처리 

![img](https://i.imgur.com/hh3Mawr.png)

### 동기적 처리

: 하나의 작업이 끝날 때까지 다른 작업이 불가능하기 때문에 기다려야함.

### 비동기적 처리 (asynchronous)

: 흐름이 멈추지 않고 동시에 여러 작업을 처리할 수 있다. 또한 기다리는 과정에서 다른 함수도 호출할 수 있다.

(원하는 때에 동작이 시작하도록 가능하다)

대표적인 함수 `setTimeout`



### 콜백 함수

: 함수 타입의 값을 파라미터로 넘겨줘서 파라미터로 받은 함수를 특정 작업이 끝나고 호출을 해주는 것을 의미.

간단하게 나중에 호출할 함수를 의미



다음과 같은 작업들은 주로 비동기적으로 처리.

- **Ajax Web API 요청**

  : 만약 서버쪽에서 데이터를 받와아야 할 때, 요청을 하고 서버에서 응답을 할 때 까지 대기를 해야 되기 때문에 작업을 비동기적으로 처리.

- **파일 읽기**

  : 주로 서버 쪽에서 파일을 읽어야 하는 상황에는 비동기적으로 처리.

- **암호화/복호화**

  : 암호화/복호화를 할 때에도 바로 처리가 되지 않고, 시간이 어느정도 걸리는 경우가 있기 때문에 비동기적으로 처리.

- **작업 예약**

  : 단순히 어떤 작업을 몇 초 후에 스케쥴링 해야 하는 상황에는, setTimeout 을 사용하여 비동기적으로 처리.

  

## Promise

프로미스는 비동기 작업을 조금 더 편하게 처리 할 수 있도록 ES6 에 도입된 기능. 

이전에는 비동기 작업을 처리 할 때에는 콜백 함수로 처리를 해야 했는데, 콜백 함수로 처리를 하게 된다면 비동기 작업이 많아질 경우 코드가 쉽게 난잡해짐.

숫자 n 을 파라미터로 받아와서 다섯번에 걸쳐 1초마다 1씩 더해서 출력하는 작업을 setTimeout 으로 구현해보자.

```javascript
function increaseAndPrint(n, callback) {
  setTimeout(() => {
    const increased = n + 1;
    console.log(increased);
    if (callback) {
      callback(increased);
    }
  }, 1000);
}

increaseAndPrint(0, n => {
  increaseAndPrint(n, n => {
    increaseAndPrint(n, n => {
      increaseAndPrint(n, n => {
        increaseAndPrint(n, n => {
          console.log('끝!');
        });
      });
    });
  });
});
```

이런 식의 코드를 Callback Hell (콜백지옥) 이라고 한다.

 비동기적으로 처리해야 하는 일이 많아질수록, 코드의 깊이가 계속 깊어진다.

이를 방지하기 위해서 **Promise**를 사용.



### Promise 만들기

Promise 는 다음과 같이 만든다.

```javascript
const myPromise = new Promise((resolve, reject) => {
  // 구현..
})
```

Promise 는 성공 할 수도 있고, 실패 할 수도 있다.

성공 할 때에는 resolve 를 호출해주면 되고, 실패할 때에는 reject 를 호출해주면 된다. 

지금 당장은 실패하는 상황은 고려하지 않고, 1초 뒤에 성공시키는 상황에 대해서만 구현을 해보자.

```javascript
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve(1);
  }, 1000); //1000ms = 1s
});

myPromise.then(n => {
  console.log(n);
});
```

resolve 를 호출 할 때 특정 값(예시에서는 1)을 파라미터로 넣어주면, 이 값을 작업이 끝나고 나서 사용 할 수 있다. 

작업이 끝나고 나서 또 다른 작업을 해야 할 때에는 Promise 뒤에 `.then(...)` 을 붙여서 사용.

이번에는, 1초뒤에 실패되게끔 해보자.

```javascript
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject(new Error());
  }, 1000);
});

myPromise
  .then(n => {
    console.log(n);
  })
  .catch(error => {
    console.log(error);
  });
```

실패하는 상황에서는 `reject` 를 사용하고, `.catch` 를 통하여 실패했을시 수행 할 작업을 설정 할 수 있다.

이제, Promise 를 만드는 함수를 작성해보자.

```javascript
function increaseAndPrint(n) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const value = n + 1;
      if (value === 5) {
        const error = new Error();
        error.name = 'ValueIsFiveError';
        reject(error);
        return;
      }
      console.log(value);
      resolve(value);
    }, 1000);
  });
}

increaseAndPrint(0).then((n) => {
  console.log('result: ', n);
})
```

![img](https://i.imgur.com/S4bDqHz.png)

