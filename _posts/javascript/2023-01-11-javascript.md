---
layout: single
title: "비동기처리, Promise, Async & Await"
categories: javascript
tag: [front-end, javascript, Promise, Async, Await]
comments: true
---

## 비동기처리
- 특정 코드의 연산이 끝날 때까지 코듸의 실행을 멈추지 않고 다음 코드를 먼저 실행하는 자바스크립트의 특성
- 예시) ajax, setTimeout

## Promise
- 자바스크립트에서 비동기 처리에 사용되는 객체로, 통신시 Api를 제공한다고 볼 수 있다.

### Promise의 상태
- Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태
- Fulfilled(이행) : 비동기 처리가 완료되어 promise가 결과 값을 반환해준 상태
- Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태

### Promise의 기본문법
```javascript
function getData() {
  return new Promise(function(resolve, reject) {
    $.get('url 주소/products/1', function(response) {
      // 응답이 오면 
      if (response) {
        resolve(response);
      }
      // 아니면 거절
      reject(new Error("Request is failed"));
    });
  });
}

// 위 $.get() 호출 결과에 따라 'response' 또는 'Error' 출력
getData().then(function(data) {
  console.log(data); // response 값 출력
}).catch(function(err) {
  console.error(err); // Error 출력
});
```
### Promise의 특징
- 여러개의 프로미서 연결이 가능하다.

```javascript
var userInfo = {
  id: 'test@abc.com',
  pw: '****'
};

function parseValue() {
  return new Promise({
    // ...
  });
}
function auth() {
  return new Promise({
    // ...
  });
}
function display() {
  return new Promise({
    // ...
  });
}

getData(userInfo)
  .then(parseValue)
  .then(auth)
  .then(diaplay);
```

### Promise의 예외처리
- catch()를 사용하여 해결

```javascript
// catch()로 오류를 감지하는 코드
function getData() {
  return new Promise(function(resolve, reject) {
    resolve('hi');
  });
}

getData().then(function(result) {
  console.log(result); // hi
  throw new Error("Error in then()");
}).catch(function(err) {
  console.log('then error : ', err); // then error :  Error: Error in then()
});
```

## Async & Await
- 비동기 처리방식인 콜백 함수와 Promise의 단점을 보완한 비동기 처리 패턴 중 가장 최근에 나온 문법
- 개발자가 코드를 읽고 이해하기 편하도록 구현된 패턴

### 기본문법
- 1단계 : 함수 앞에 async라는 예약어를 붙임.
- 2단계 : 함수 내부 로직 중 HTTP 통신을 하는 비동기처리 코드 앞에 await를 붙임.(꼭 프로미스 객체를 반환해야 함.)

```javascript
async function 함수명() {
  await 비동기_처리_메서드_명();
}
```

### 예시

```javascript
function fetchUser() {
  var url = 'https://jsonplaceholder.typicode.com/users/1'
  return fetch(url).then(function(response) {
    return response.json();
  });
}

function fetchTodo() {
  var url = 'https://jsonplaceholder.typicode.com/todos/1';
  return fetch(url).then(function(response) {
    return response.json();
  });
}

async function logTodoTitle() {
  var user = await fetchUser();
  if (user.id === 1) {
    var todo = await fetchTodo();
    console.log(todo.title); // delectus aut autem
  }
}
```

### 예외처리
- try catch 사용

```javascript
async function logTodoTitle() {
  try {
    var user = await fetchUser();
    if (user.id === 1) {
      var todo = await fetchTodo();
      console.log(todo.title); // delectus aut autem
    }
  } catch (error) {
    console.log(error);
  }
}
```

## 참고 사이트
<a href='https://joshua1988.github.io/web-development/javascript/javascript-asynchronous-operation/' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># 캡틴판교님의 블로그</a>