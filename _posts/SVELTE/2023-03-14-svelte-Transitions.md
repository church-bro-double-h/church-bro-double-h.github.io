---
layout: single
title: "svelte 공식 사이트 Tutorial 정리 ⑩ : Transitions & The animate directive"
categories: svelte
tag: [svelte, front-end]
comments: true
---

# Transitions

## The transition directive
- Svelte는 transition 지시자를 이용해서 UI를 부드럽게 전환할 수 있다.

### Fade 사용 예시

```html
<script>
	import { fade } from 'svelte/transition';
	let visible = true;
</script>

<label>
	<input type="checkbox" bind:checked={visible}>
	visible
</label>

{#if visible}
	<p transition:fade>
		Fades in and out
	</p>
{/if}
```

## Adding parameters
- trasition function은 parameters를 받을 수 있다.

### Fly 사용 예시

```html
<script>
	import { fly } from 'svelte/transition';
	let visible = true;
</script>

<label>
	<input type="checkbox" bind:checked={visible}>
	visible
</label>

{#if visible}
	<p transition:fly="{{ y: 200, duration: 2000 }}">
		Flies in and out
	</p>
{/if}
```
## In and out
- transition 대신 in, out, in & out 둘다 가질 수 있다.

### 예시

```html
<script>
	import { fade, fly } from 'svelte/transition';
	let visible = true;
</script>

<label>
	<input type="checkbox" bind:checked={visible}>
	visible
</label>

{#if visible}
	<p in:fly="{{ y: 200, duration: 2000 }}" out:fade>
		Flies in, fades out
	</p>
{/if}
```

## Custom CSS transitions
- 기존에 있는 것을 사용할수도 있지만 custom transition을 만들수도 있다.

## Custom JS transitions
- CSS만으로 custom transition을 만들기 힘들다면 javascript의 도움을 빌려서 만들수도 있다.

## Transition events
- 전환 효과가 시작되고 끝나는 시점에 이벤트를 발생시킬 수 있다.

### 예시

```html
<p
	transition:fly="{{ y: 200, duration: 2000 }}"
	on:introstart="{() => status = 'intro started'}"
	on:outrostart="{() => status = 'outro started'}"
	on:introend="{() => status = 'intro ended'}"
	on:outroend="{() => status = 'outro ended'}"
>
	Flies in and out
</p>
```

## Local transitions
- local이라는 옵션값을 설정하면 전환 블록 자체가 추가 또는 제거될때만 재상된다.

### 예시
- local이 없으면 show list를 체크하거나 해제할때 항목들의 이벤트에 slide효과가 들어가지만, local이 있으면 slide효과는 항목의 추가 삭제에만 국한된다. 

```html
<script>
	import { slide } from 'svelte/transition';

	let showItems = true;
	let i = 5;
	let items = ['one', 'two', 'three', 'four', 'five', 'six', 'seven', 'eight', 'nine', 'ten'];
</script>

<label>
	<input type="checkbox" bind:checked={showItems}>
	show list
</label>

<label>
	<input type="range" bind:value={i} max=10>

</label>

{#if showItems}
	{#each items.slice(0, i) as item}
		<div transition:slide|local>
			{item}
		</div>
	{/each}
{/if}

<style>
	div {
		padding: 0.5em 0;
		border-top: 1px solid #eee;
	}
</style>
```

## Deferred transitions
- Svelte에서 제공하는 transition 엔진의 강력한 기능 중 하나는 여러 요소 간에 조율하여 전환을 deferred(지연)시킬 수 있다는 것이다.
- send와 receive라는 두개의 전환을 생성하는 crossfae 함수를 사용하여 이런 요소를 구현하면 부드럽게 이동하는 것 처럼 보인다.

### 예시
```html
<script>
	import { quintOut } from 'svelte/easing';
	import { crossfade } from 'svelte/transition';

	const [send, receive] = crossfade({
		duration: d => Math.sqrt(d * 200),

		fallback(node, params) {
			const style = getComputedStyle(node);
			const transform = style.transform === 'none' ? '' : style.transform;

			return {
				duration: 600,
				easing: quintOut,
				css: t => `
					transform: ${transform} scale(${t});
					opacity: ${t}
				`
			};
		}
	});

	let uid = 1;

	let todos = [
		{ id: uid++, done: false, description: 'write some docs' },
		{ id: uid++, done: false, description: 'start writing blog post' },
		{ id: uid++, done: true,  description: 'buy some milk' },
		{ id: uid++, done: false, description: 'mow the lawn' },
		{ id: uid++, done: false, description: 'feed the turtle' },
		{ id: uid++, done: false, description: 'fix some bugs' },
	];

	function add(input) {
		const todo = {
			id: uid++,
			done: false,
			description: input.value
		};

		todos = [todo, ...todos];
		input.value = '';
	}

	function remove(todo) {
		todos = todos.filter(t => t !== todo);
	}

	function mark(todo, done) {
		todo.done = done;
		remove(todo);
		todos = todos.concat(todo);
	}
</script>

<div class='board'>
	<input
		placeholder="what needs to be done?"
		on:keydown={e => e.key === 'Enter' && add(e.target)}
	>

	<div class='left'>
		<h2>todo</h2>
		{#each todos.filter(t => !t.done) as todo (todo.id)}
			<label
				in:receive="{{key: todo.id}}"
				out:send="{{key: todo.id}}"
			>
				<input type=checkbox on:change={() => mark(todo, true)}>
				{todo.description}
				<button on:click="{() => remove(todo)}">remove</button>
			</label>
		{/each}
	</div>

	<div class='right'>
		<h2>done</h2>
		{#each todos.filter(t => t.done) as todo (todo.id)}
			<label
				class="done"
				in:receive="{{key: todo.id}}"
				out:send="{{key: todo.id}}"
			>
				<input type=checkbox checked on:change={() => mark(todo, false)}>
				{todo.description}
				<button on:click="{() => remove(todo)}">remove</button>
			</label>
		{/each}
	</div>
</div>

<style>
	.board {
		display: grid;
		grid-template-columns: 1fr 1fr;
		grid-gap: 1em;
		max-width: 36em;
		margin: 0 auto;
	}

	.board > input {
		font-size: 1.4em;
		grid-column: 1/3;
	}

	h2 {
		font-size: 2em;
		font-weight: 200;
		user-select: none;
		margin: 0 0 0.5em 0;
	}

	label {
		position: relative;
		line-height: 1.2;
		padding: 0.5em 2.5em 0.5em 2em;
		margin: 0 0 0.5em 0;
		border-radius: 2px;
		user-select: none;
		border: 1px solid hsl(240, 8%, 70%);
		background-color:hsl(240, 8%, 93%);
		color: #333;
	}

	input[type="checkbox"] {
		position: absolute;
		left: 0.5em;
		top: 0.6em;
		margin: 0;
	}

	.done {
		border: 1px solid hsl(240, 8%, 90%);
		background-color:hsl(240, 8%, 98%);
	}

	button {
		position: absolute;
		top: 0;
		right: 0.2em;
		width: 2em;
		height: 100%;
		background: no-repeat 50% 50% url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24'%3E%3Cpath fill='%23676778' d='M12,2C17.53,2 22,6.47 22,12C22,17.53 17.53,22 12,22C6.47,22 2,17.53 2,12C2,6.47 6.47,2 12,2M17,7H14.5L13.5,6H10.5L9.5,7H7V9H17V7M9,18H15A1,1 0 0,0 16,17V10H8V17A1,1 0 0,0 9,18Z'%3E%3C/path%3E%3C/svg%3E");
		background-size: 1.4em 1.4em;
		border: none;
		opacity: 0;
		transition: opacity 0.2s;
		text-indent: -9999px;
		cursor: pointer;
	}

	label:hover button {
		opacity: 1;
	}
</style>
```

## Key blocks
- 값이 변경될 때 해당 내용을 파괴하고 다시 만든다.
- 이는 값이 바뀔때 유용하다.

### 예시

```html
<script>
  import { fly } from 'svelte/transition';

  let number = 0;
</script>

<div>
  The number is:
  {#key number}
  <span style="display: inline-block" in:fly={{ y: -20 }}>
			{number}
		</span>
  {/key}
</div>
<br />
<button
  on:click={() => {
number += 1;
}}>
Increment
</button>

```


## 참고 사이트
<a href='https://svelte.dev/tutorial/transition' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼 - Bindings</a>

 