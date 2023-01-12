---
layout: single
title: "svelte 공식 사이트 Tutorial 정리 ④ : Logic"
categories: svelte
tag: [svelte, front-end]
comments: true
---

# Logic

## 1. If blocks
- HTML은 로직적인 표현을 사용할수 없지만 조건문과 반복절을 스벨트는 할 수 있다.(JSP처럼...)
- {#if (조건)} : 조건문 열고 조건문 선언
- {/if} : 조건문 닫기

### 예시

#### App.svelte
```html
<script>
  let user = { loggedIn: false };

  function toggle() {
    user.loggedIn = !user.loggedIn;
  }
</script>

{#if user.loggedIn}
<button on:click={toggle}>
  Log out
</button>
{/if}

{#if !user.loggedIn}
<button on:click={toggle}>
  Log in
</button>
{/if}
```

## 2. else blocks
- 상호적으로 독점적인 조건으로 로직이 동작해야 하는 경우 else문을 사용하는게 깔끔한데 아래와 같이 구현 가능하다.
- {:else} : 중간에 있는 svelte구문은 {:머시기}로 구현 가능.

### 예시

#### App.svelte
```html
<script>
  let user = { loggedIn: false };

  function toggle() {
    user.loggedIn = !user.loggedIn;
  }
</script>

{#if user.loggedIn}
<button on:click={toggle}>
  Log out
</button>
{:else}
<button on:click={toggle}>
  Log in
</button>
{/if}
```
#### svelte syntax 설명
- ```#``` : 해당 문자는 언제나 block의 시작을 가리킨다.
- ```/``` : 해당 문자는 언제나 block의 끝을 가리킨다.
- ```:``` : 해당 문자는 언제나 block의 계속되는 태그 가리킨다.

## 3. Else-if blocks
- 다중 조건은 else if로 연결할 수 있다.

```html
<script>
	let x = 7;
</script>

{#if x > 10}
	<p>{x} is greater than 10</p>
{:else if 5 > x}
	<p>{x} is less than 5</p>
{:else}
	<p>{x} is between 5 and 10</p>
{/if}
```

## 4. Each blocks
- 만약에 데이터 목록의 반복 출력을 필요로 한다면 each구문을 사용하면 된다.
- index를 사용하고 싶다면 두번째 인자를 넣으면 된다.

```html
<script>
  let cats = [
    { id: 'J---aiyznGQ', name: 'Keyboard Cat' },
    { id: 'z_AbfPXTKms', name: 'Maru' },
    { id: 'OUtn3pvWmpg', name: 'Henri The Existential Cat' }
  ];
</script>

<h1>The Famous Cats of YouTube</h1>

<ul>
  {#each cats as cat, i}
  <li><a target="_blank" href="https://www.youtube.com/watch?v={cat.id}" rel="noreferrer">
    {i + 1}: {cat.name}
  </a></li>
  {/each}
</ul>
```

- 더 간단하게 구현 예시

```html
<ul>
    {#each cats as { id, name }, i}
        <li>
            <a target="_blank" href="https://www.youtube.com/watch?v={id}" rel="noreferrer">
                {i + 1}: {name}
            </a>
        </li>
    {/each}
</ul>
```

## 5. Keyed each blocks
- each문의 key가 어떻게 설정되어 있는지 이해가 필요하다.

### 예시

#### App.svelte 변경전
```html
<script>
	import Thing from './Thing.svelte';

	let things = [
		{ id: 1, name: 'apple' },
		{ id: 2, name: 'banana' },
		{ id: 3, name: 'carrot' },
		{ id: 4, name: 'doughnut' },
		{ id: 5, name: 'egg' },
	];

	function handleClick() {
		things = things.slice(1);
	}
</script>

<button on:click={handleClick}>
	Remove first thing
</button>

{#each things as thing}
	<Thing name={thing.name}/>
{/each}

```

#### Things .svelte
```html
<script>
  const emojis = {
    apple: "🍎",
    banana: "🍌",
    carrot: "🥕",
    doughnut: "🍩",
    egg: "🥚"
  }

  // the name is updated whenever the prop value changes...
  export let name;

  // ...but the "emoji" variable is fixed upon initialisation of the component
  const emoji = emojis[name];
</script>

<p>
  <span>The emoji for { name } is { emoji }</span>
</p>

<style>
  p {
    margin: 0.8em 0;
  }
  span {
    display: inline-block;
    padding: 0.2em 1em 0.3em;
    text-align: center;
    border-radius: 0.2em;
    background-color: #FFDFD3;
  }
</style>
```

#### App.svelte 변경 후
```html
<script>
	import Thing from './Thing.svelte';

	let things = [
		{ id: 1, name: 'apple' },
		{ id: 2, name: 'banana' },
		{ id: 3, name: 'carrot' },
		{ id: 4, name: 'doughnut' },
		{ id: 5, name: 'egg' },
	];

	function handleClick() {
		things = things.slice(1);
	}
</script>

<button on:click={handleClick}>
	Remove first thing
</button>

{#each things as thing (thing.id)}
    <Thing name={thing.name}/>
{/each}

```
### 해설
- 첫번째 항목 삭제 버튼 클릭시 한줄이 지워지고 내용과 이모지가 일치하여야 되지만, 예상과는 다르게 불일치하게 된다.
- 그 이유는 JS output 탭으로 비교해보면 그렇게 구현되어 있다는 것을 알 수 있다. 따라서 svelte에서는 원하는 id에 맞게 구현될 수 있도록 key라는 기능을 넣었다.

## 6. Await blocks

### Await란?
- Await를 이해하기 위해서는 Promise 객체를 알아야 하고, Promise 객체를 이해하기 위해서는 Javascript에서의 비동기 처리를 이해해야 한다.
- Await 설명 관련 게시물 이동 : <a href='https://church-bro-double-h.github.io/javascript/javascript/' target='_blank' style="color:blue; font-size:12px; font-weight:bold;">비동기처리, Promise, Async & Await</a> 

### 예시

```html
<script>
	async function getRandomNumber() {
		const res = await fetch(`/tutorial/random-number`);
		const text = await res.text();

		if (res.ok) {
			return text;
		} else {
			throw new Error(text);
		}
	}
	
	let promise = getRandomNumber();

	function handleClick() {
		promise = getRandomNumber();
	}
</script>

<button on:click={handleClick}>
	generate random number
</button>

{#await promise}
	<p>...waiting</p>
{:then number}
	<p>The number is {number}</p>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}

```

### reject하고 싶지 않은 경우
- 아래와 같이 구현

```html
{#await promise then number}
	<p>the number is {number}</p>
{/await}
```

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













## 참고 사이트
<a href='https://svelte.dev/tutorial/making-an-app' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼</a>