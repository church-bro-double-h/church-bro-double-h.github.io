---
layout: single
title: "svelte 공식 사이트 Tutorial 정리 ⑧ : Store"
categories: svelte
tag: [svelte, front-end]
comments: true
---

# Store
- 어플리케이션 계층 구조에 속하지는 않지만, 때때로 다양하고 연관없는 component 또는 일반적인 javascript 모듈에서 접근 가능한 값이 필요할 수가 있다.
- svelte에서는 store라는 module이 이러한 기능을 제공해준다. 한마디로 여러개의 component에서 공통적으로 참조하는 값에 대해서, 저장해놓는 것이다.

## Writable stores
- 쓰기 가능한 저장소로 subscribe(:값을 가져오는 것), set(:값을 셋팅하는 것), update(:값을 수정하는 것.) 3가지 method를 제공한다.

### 예시
- store.js에서 count라는 store를 export한다. 
- Decrementer.svelte, Incrementer.svelte, Resetter.svelte에서 해당 store를 import하여 value를 조작한다.
- count store를 subscribe하는 App.svelte에서 저장된 값을 그대로 사용 표현한다.

###### App.svelte 

```html
<script>
  import { count } from './stores.js';
  import Incrementer from './Incrementer.svelte';
  import Decrementer from './Decrementer.svelte';
  import Resetter from './Resetter.svelte';

  let countValue;

  count.subscribe(value => {
    countValue = value;
  });
</script>

<h1>The count is {countValue}</h1>

<Incrementer/>
<Decrementer/>
<Resetter/>
```

###### Decrementer.svelte

```html
<script>
	import { count } from './stores.js';

	function decrement() {
		count.update(n => n - 1);
	}
</script>

<button on:click={decrement}>
	-
</button>
```

###### Incrementer.svelte

```html
<script>
  import { count } from './stores.js';

  function increment() {
    count.update(n => n + 1);
  }
</script>

<button on:click={increment}>
  +
</button>
```

###### Resetter.svelte

```html
<script>
  import { count } from './stores.js';

  function reset() {
    count.set(0);
  }
</script>

<button on:click={reset}>
  reset
</button>
```

###### stores.js

```javascript
import { writable } from 'svelte/store';

export const count = writable(0);
```

## Auto-subscriptions
- 이전 방식은 subscribe 하고 unsubscribe를 하지 않음으로 메모리 누수가 발생되는 버그가 생긴다.
- 따라서 onDestory를 통해 unsubscribe를 해줌으로써 해당 버그를 해결할수 있는데, 

### 예시
- store.js에서 count라는 store를 export한다.
- Decrementer.svelte, Incrementer.svelte, Resetter.svelte에서 해당 store를 import하여 value를 조작한다.
- count store를 subscribe하는 App.svelte에서 저장된 값을 그대로 사용 표현한다.
- $와 store 이름을 접두사로 사용하여 store 값을 참조할 수 있습니다. 예시 : ```$count```
- Auto-subscriptions은 component의 최상위 scope에서 선언(또는 가져온)된 store 변수에 대해서만 작동
- $로 시작하는 이름은 store 값으로 가정됩니다. $는 예약어로, $ 접두사로 자신의 변수를 선언하는 것을 Svelte가 방지

## Readable stores
- 다른 사람에 의해 쓰기가 가능하지 않은 값(가령 마우스위치나 지리적위치)에 대해서 사용

### 예시
- readable(첫번째인자, function start(set){ return function stop(){}}; )
- 첫번째 인자 : 초기값
- 두번째 인자 start함수로 set을 callback으로 받고, store가 처음 subscribe될때 호출된다.
- stop 함수를 return 하는데, 구독이 해제될때 호출된다.
```javascript
 readable(new Date(), function start(set) {
  const interval = setInterval(() => {
    set(new Date());
  }, 1000);

  return function stop() {
    clearInterval(interval);
  };
});
```

## Derived stores
- 파생된 저장소라는 느낌으로, 하나 또는 그 이상의 다른 store를 기초로 하여 만들어지는 store를 말한다.

### 예시

```javascript
export const elapsed = derived(
	time,
	$time => Math.round(($time - start) / 1000)
);
```

## Custom stores
- subscribe 메서드를 올바르게 구현하면 어떤 객체든 store가 될 수 있다. 
- 앞선 예제에서 다수의 .svelte를 통해 로직을 구현했다면, 아래와 같은 방법으로 한번에 구현할수도 있다.

### 예제

###### App.svelte

```html
<script>
	import { count } from './stores.js';
</script>

<h1>The count is {$count}</h1>

<button on:click={count.increment}>+</button>
<button on:click={count.decrement}>-</button>
<button on:click={count.reset}>reset</button>
```
###### store.js

```javascript
import { writable } from 'svelte/store';

function createCount() {
	const { subscribe, set, update } = writable(0);

	return {
		subscribe,
		increment: () => update(n => n + 1),
		decrement: () => update(n => n - 1),
		reset: () => set(0)
	};
}

export const count = createCount();
```

## Store bindings
- writable store라면 binding이 가능하고, 값 변경 또한 가능하다.

### 예제

```html
<input bind:value={$name}>

<button on:click="{() => $name += '!'}">
	Add exclamation mark!
</button>
```

## 참고 사이트
<a href='https://svelte.dev/tutorial/writable-stores' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼 - Bindings</a>

 