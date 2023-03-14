---
layout: single
title: "svelte 공식 사이트 Tutorial 정리 ⑤ : Event"
categories: svelte
tag: [svelte, front-end]
comments: true
---

# Events

## DOM events
- ```on:``` 이라는 지시어를 통해 어떤 이벤트도 엘리먼트에 부여할 수 있다. 
- DOM events 종류보기 : <a href='https://www.w3schools.com/jsref/dom_obj_event.asp' target='_blank' style="color:blue; font-size:12px; font-weight:bold;">W3Schools</a>

### 예시

```html
<script>
	let m = { x: 0, y: 0 };

	function handleMousemove(event) {
		m.x = event.clientX;
		m.y = event.clientY;
	}
</script>

<div on:mousemove={handleMousemove}>
	The mouse position is {m.x} x {m.y}
</div>

<style>
	div { width: 100%; height: 100%; }
</style>
```

## Inline handlers
- 이벤트 헨들러를 Inline 구문으로 선언할수도 있다.
- 이벤트 핸들러 설명 관련 게시물 이동 : <a href='https://church-bro-double-h.github.io/javascript/javascript-2/' target='_blank' style="color:blue; font-size:12px; font-weight:bold;">이벤트, 이벤트 핸들러, 이벤트 리스너</a>

### 예시

```html
<script>
	let m = { x: 0, y: 0 };

</script>

<div on:mousemove="{e => m = { x: e.clientX, y: e.clientY }}">
	The mouse position is {m.x} x {m.y}
</div>

<style>
	div { width: 100%; height: 100%; }
</style>
```

## Event modifiers
- DOM이벤트 핸들러에 수식어 그들의 행동을 변경하는 수식어(한정어)를 가질 수 있다.

### once 예시
- 이벤트가 단 한번만 실행됨.

```html
<script>
	function handleClick() {
		alert('no more alerts')
	}
</script>

<button on:click|once={handleClick}>
	Click me
</button>
```

### The full list of modifiers
- preventDefault : calls event.preventDefault() before running the handler. Useful for client-side form handling, for example.
- stopPropagation : calls event.stopPropagation(), preventing the event reaching the next element
- passive : improves scrolling performance on touch/wheel events (Svelte will add it automatically where it's safe to do so)
- nonpassive : explicitly set passive: false
- capture : fires the handler during the capture phase instead of the bubbling phase (MDN docs)
- once : remove the handler after the first time it runs
- self : only trigger handler if event.target is the element itself
- trusted : only trigger handler if event.isTrusted is true. I.e. if the event is triggered by a user action.

### modifier는 함께 쓸 수도 있다.

```shell
  on:click|once|capture={...}
```

## Component events
- 컴포넌트 안에 있는 이벤트는 전달되어 모체에서 사용할수 있다. 그렇게 하기 위해서는 event Dispatcher를 만들어야 한다. 

### 방법

1. svelte의 Class를 불러와서 함수에 사용한다.
###### Component.svelte

```html
<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  function sayHello() {
    dispatch('message', {
      text: 'Hello!'
    });
  }
</script>
<button on:click={sayHello}>
	Click to say hello
</button>
```
- 클릭하면 sayHello라는 이벤트를 호출한다. sayHello 이벤트는 전달해주는데 message라는 이벤트에 {text: 'Hello!'}를 전달해준다.

2. 컴포넌트를 사용하는 모체에서 컴포넌트를 생성할때 아래와 같이 구현

```html
<script>
	import Inner from './Inner.svelte';

	function handleMessage(event) {
		alert(event.detail.text);
	}
</script>

<Inner on:message={handleMessage}/>
```
- 이벤트 이름은 바꿀수 있다. 가령 on:message를 on:alertMessage로 바꾸고, dispatch('alertMessage' 어쩌구저쩌구)라고 사용할수 있다.

## Event forwarding
- 불행스럽게도 DOM event와 component 이벤트는 Bubbling이 되지 않는다.
- 3개의 component가 있다. App.svelte에서는 Outer.svelte를 불러오고, Outer.svelte는 Inner.svelte를 불러온다.
- 이때 Inner.svelte안에 있는 컴포넌트 이벤트를 사용하려면 Outer.svelte에서도 dispatch를 사용해줘야 한다.
- 하지만 너무 많은 소스를 입력해줘야 하기때문에 svelte에는 on:message 이벤트 지시자에 값이 없는 경우 '모든 message 이벤트를 전달'한다는 동일한 약어를 제공합니다.

★ Bubbling이란?
- 버블링(bubbling)은 DOM 이벤트 처리 중 하위 요소에서 발생한 이벤트가 상위 요소로 전달되는 현상을 말합니다. 즉, 하위 요소에서 이벤트가 발생하면 이벤트가 가장 하위의 요소에서 시작해서 조상 요소로 올라가면서 발생하는 것입니다. 예를 들어, div 요소 안에 button 요소가 있는 경우, 버튼을 클릭하면 버튼에서 click 이벤트가 발생합니다. 이때 이벤트는 버튼에서 시작해서 div 요소로 올라가면서 발생합니다. 이렇게 상위 요소로 전달되는 이벤트를 버블링 이벤트(bubbling event)라고 합니다. 이러한 버블링 현상은 이벤트 처리 과정에서 이벤트 전파를 편리하게 해주지만, 이벤트가 불필요하게 상위 요소까지 전파되는 경우도 있어서 성능 문제를 일으킬 수도 있습니다.

### dispatch 사용 예

```html
<script>
	import Inner from './Inner.svelte';
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	function forward(event) {
		dispatch('message', event.detail);
	}
</script>

<Inner on:message={forward}/>
```
### 줄인 예

```html
<script>
	import Inner from './Inner.svelte';
</script>

<Inner on:message/>
```
## DOM event forwarding
- 앞서 기술한 바와 동일한 원리로 DOM 이벤트에 대해서도 전달(forwarding)하여 사용할수 있다.

###### CustomButton.svelte
```html
<button on:click>
	Click me
</button>
```

###### App.svelte

```html
<script>
	import CustomButton from './CustomButton.svelte';

	function handleClick() {
		alert('Button Clicked');
	}
</script>

<CustomButton on:click={handleClick}/>
```
- CustomButton.svelte에 있는 button에 on:click이벤트가 있고, App.svelte에서 CustomButton 컴포넌트를 불러올때 on:click 이벤트를 그대로 forwarding하여 사용한 예시이다.




## 참고 사이트
<a href='https://svelte.dev/tutorial/dom-events' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼</a>
<a href='https://ko.javascript.info/introduction-browser-events' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼</a>

