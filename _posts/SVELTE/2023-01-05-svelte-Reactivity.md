---
layout: single
title: "svelte 공식 사이트 Tutorial 정리 ② : Reativity"
categories: svelte
tag: [svelte, front-end]
comments: true
---

# Reativity

## 1. Assignments
- Svelte의 심장은 어플리케이션의 상태의 Sync를 DOM과 맞추는 강력한 반응성 시스템에 있다.

### 예시 : 버튼을 누름에 따라 바로 횟수 증가
```html
<script>
  let count = 0;

  function incrementCount() {
    // event handler code goes here
    count += 1;
  }
</script>

<button on:click={incrementCount}>
  Clicked {count} {count === 1 ? 'time' : 'times'}
</button>
```
## 2. Declarations 
- Svelte는 단순히 DOM영역의 Sync만을 맞추는게 아니라, 변수끼리의 Sync도 맞춰준다.
- 반응형 변수를 선언하기 위해서 ```$:``` 라는 keyword를 사용한다.
```html
let count = 0;
$: doubled = count * 2;

<p>{count} doubled is {doubled}</p>
```
- 만약 위 구분이 그저 스크립트로만 구성되어 있었다면,
<br>스크립트를 모두 호출한 다음에 태그의 데이터가 셋팅되므로 '0 doubled is 0'이라고 표시되었을 테지만,
<br>count에 1을 선언한다면 double의 값도 sync가 맞춰저 2가 되고 화면에는 '1 doubled is 2' 라고 표시될 것이다.

## 3. Statements
- $:의 용법은 구문 사용에도 적용이 가능해서, 참조하고 있는 값이 변경되면 해당 구문이 다시 실행되는 것이다.

```html
$: console.log('the count is ' + count);

$: {
console.log('the count is ' + count);
alert('I SAID THE COUNT IS ' + count);
}

$: if (count >= 10) {
    alert('count is dangerously high!');
    count = 9;
}
```

## 4. Updating arrays and objects
- 배열과 관련된 메소드를 사용하는 경우 반응형으로 sync를 맞춰주지 못하기에 아래와 같은 방법을 사용한다.

### javascript 정석
```javascript
function addNumber() {
	numbers.push(numbers.length + 1);
	numbers = numbers;
}
```
### ES6 spread syntax
```javascript
  function addNumber() {
    numbers[numbers.length] = numbers.length + 1;
  }
```
- 동일한 규칙에 의해 pop, shift, splice 및 Map.set, Set.add와 같은 objects methods 등 또한 위와 같이 사용이 가능하다.
- 그러나 간접적인 참조변수의 할당은 반응성의 트리거를 발생시킬수 없으므로 obj = obj와 같은 형식으로 구현해야 한다.


## 참고 사이트
<a href='https://svelte.dev/tutorial/making-an-app' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼</a>