---
layout: single
title: "svelte 공식 사이트 Tutorial 정리 ⓐ : Special elements"
categories: svelte
tag: [svelte, front-end]
comments: true
---

# Special elements
- svelte는 다양한 내장 요소를 재공한다. 

## <svelte:self>
- 모듈은 자기 자신을 가져올 수 없으므로 <svelte:self>를 통해 자기 자신을 사용한다. 
- 폴더가 다른 폴더를 포함할 수 잇는 tree view에 적합.

### 예시
- file에 files가 있는 경우 폴더라 Folder.svelte로 구성해야되고, 아니면 파일이라 File.svelte component를 사용해야 하는데, Folder안에서는 Forlder를 import할 수 없으므로 <svelte:self>를 통해 자기 자신을 호출.

```html
{#if expanded}
	<ul>
		{#each files as file}
			<li>
				{#if file.files}
					<svelte:self {...file}/>
				{:else}
					<File {...file}/>
				{/if}
			</li>
		{/each}
	</ul>
{/if}
```

## <svelte:component>
- element가 Component인 경우 해당 element를 사용하여 쉽게 구현 가능하다.

### 예시
- selectbox에서 옵션 선택시 binding된 변수는 options를 바꾸고, options에 해당 하는 component가 불러와지는 구조.

###### 변경 전

```html
<script>
  import RedThing from './RedThing.svelte';
  import GreenThing from './GreenThing.svelte';
  import BlueThing from './BlueThing.svelte';

  const options = [
    { color: 'red',   component: RedThing   },
    { color: 'green', component: GreenThing },
    { color: 'blue',  component: BlueThing  },
  ];

  let selected = options[0];
</script>
{#if selected.color === 'red'}
	<RedThing/>
{:else if selected.color === 'green'}
	<GreenThing/>
{:else if selected.color === 'blue'}
	<BlueThing/>
{/if}
```

###### 변경 후

```html
<svelte:component this={selected.component}/>
```

## <svelte:element>
- 조건에 따라서 DOM 요소를 rendering할 때 사용.

### 예시
- selectbox에서 옵션 선택시 binding된 변수는 options를 바꾸고, options에 해당 하는 component가 불러와지는 구조.

###### 변경 전

```html
<script>
	const options = ['h1', 'h3', 'p'];
	let selected = options[0];
</script>

<select bind:value={selected}>
	{#each options as option}
		<option value={option}>{option}</option>
	{/each}
</select>

{#if selected === 'h1'}
<h1>I'm a h1 tag</h1>
{:else if selected === 'h3'}
<h3>I'm a h3 tag</h3>
{:else if selected === 'p'}
<p>I'm a p tag</p>
{/if}
```

###### 변경 후
```html
<svelte:element this={selected}>I'm a {selected} tag</svelte:element>
```

## <svelte:window>
- DOM요소에 event listener를 추가하듯, window 객체에 event listener를 추가할 수 있다.

### 예시

```html
<svelte:window on:keydown={handleKeydown}/>
```

## <svelte:window> bindings
- window의 scrollY와 같은 특정 속성도 binding할 수 있다.

### binding 가능 속성목록
- innerWidth : 읽기 전용
- innerHeight : 읽기 전용
- outerWidth : 읽기 전용
- outerHeight : 읽기 전용
- scrollX
- scrollY
- online — window.navigator.onLine의 별칭(alias) : 읽기 전용

### 예시

```html
<svelte:window bind:scrollY={y}/>
```

## <svelte:body>
- document.body에서 발생하는 event를 수신할 수 있다. 

### 예시

```html
<svelte:body
	on:mouseenter={handleMouseenter}
	on:mouseleave={handleMouseleave}
/>
```

## <svelte:head>
- document의 head안에 요소를 삽입할 수 있다.

### 예시

```html
<svelte:head>
  <link rel="stylesheet" href="/tutorial/dark-theme.css">
</svelte:head>
```

## <svelte:options>
- compiler option을 적용할 수 있다.

### 옵션
- immutable={true} — 불변 데이터를 사용하는 경우, 컴파일러는 값이 변경되었는지 여부를 간단한 참조 동등성 검사를 통해 결정
- accessors={true} — 컴포넌트의 props에 대해 getter와 setter를 추가
- namespace="..." — 이 컴포넌트가 사용될 이름공간(namespace). 가장 일반적으로 "svg"입니다.
- tag="..." — 이 컴포넌트를 컴파일할 때 사용할 이름입니다.

### 예시
- immutable 미설정시 todo 값 변경하면 해당 데이터의 변경에 따라 Todo.svelte에서 flash 함수를 호출하여 전 항목이 번쩍이도록 되어 있따.
- 따라서 immutable을 설정하여 todo object에 대해 변하지 않을 것이라는 약속을 각 component마다 해놓음으로써 변경 분에 대해서만 update가 이뤄진다. 

###### App.svelte
```html
<script>
	import Todo from './Todo.svelte';

	let todos = [
		{ id: 1, done: true, text: 'wash the car' },
		{ id: 2, done: false, text: 'take the dog for a walk' },
		{ id: 3, done: false, text: 'mow the lawn' }
	];

	function toggle(toggled) {
		todos = todos.map(todo => {
			if (todo === toggled) {
				// return a new object
				return {
					id: todo.id,
					text: todo.text,
					done: !todo.done
				};
			}

			// return the same object
			return todo;
		});
	}
</script>

<h2>Todos</h2>
{#each todos as todo}
	<Todo {todo} on:click={() => toggle(todo)}/>
{/each}
```

###### Todo.svelte
```html
<svelte:options immutable={true}/>

  <script>
    import { afterUpdate } from 'svelte';
    import flash from './flash.js';

    export let todo;

    let button;

    afterUpdate(() => {
      flash(button);
    });
  </script>

  <!-- the text will flash red whenever
       the `todo` object changes -->
  <button bind:this={button} type="button" on:click>
    {todo.done ? '👍': ''} {todo.text}
  </button>

  <style>
    button {
      all: unset;
      display: block;
      cursor: pointer;
      line-height: 1.5;
    }
  </style>

```

###### flash.js
```javascript
export default function flash(element) {
    
  requestAnimationFrame(() => {
    element.style.transition = 'none';
    element.style.color = 'rgba(255,62,0,1)';
    element.style.backgroundColor = 'rgba(255,62,0,0.2)';

    setTimeout(() => {
      element.style.transition = 'color 1s, background 1s';
      element.style.color = '';
      element.style.backgroundColor = '';
    });
  });
}
```

## <svelte:fragment>
- 컨테이너 DOM 요소를 둘러싸지 않고 이름이 지정된 slot에 contents를 배치할 수 있도록 한다.
- 문서의 흐름 layout을 유지

### 예제
- box.svelte는 div에 box라는 class를 적용하며 flex layout을 1em padding을 주고 만들었다.
- 그러나 slot의 부분은 새로운 div에 의해 만들어져 layout이 깨진다.
- 이러한 layout을 유지하기 위해 div를 svelte:fragment로 바꾼 것이다.

###### App.svelte

```html
<script>
	import Box from './Box.svelte'
</script>

<Box>
	<svelte:fragment slot="footer">
		<p>All rights reserved.</p>
		<p>Copyright (c) 2019 Svelte Industries</p>
	</svelte:fragment>
</Box>
```

###### Box.svelte

```html
<div class="box">
	<slot name="header">No header was provided</slot>
	<p>Some content between header and footer</p>
	<slot name="footer"></slot>
</div>

<style>
	.box {
		width: 300px;
		border: 1px solid #aaa;
		border-radius: 2px;
		box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.1);
		padding: 1em;
		margin: 0 0 1em 0;
		
		display: flex;
		flex-direction: column;
		gap: 1em;
	}
</style>
```

## 참고 사이트
<a href='https://svelte.dev/tutorial/svelte-self' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼 - Bindings</a>

 