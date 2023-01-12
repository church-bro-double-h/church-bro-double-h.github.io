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
```on:click|once|capture={...}```

## Component events
- 












## 참고 사이트
<a href='https://svelte.dev/tutorial/making-an-app' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼</a>
<a href='https://ko.javascript.info/introduction-browser-events' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼</a>

