---
layout: single
title: "svelte 공식 사이트 Tutorial 정리 ⑥ : Bindings"
categories: svelte
tag: [svelte, front-end]
comments: true
---

# Bindings

## Text inputs
- Svelte안에서 일반적인 데이터 흐름의 규칙은 Top-Down(부모 엘리먼트가 자식 엘리먼트에게 props를 셋팅하고, 그 이후 변경되거나 수정되지 않는다.)방식이다.
- 그러나 때로는 해당 규칙이 깨져야할 필요가 있다. props를 수정하면 해당 props를 참조하고 있는 엘리먼트들의 값 또한 수정하기 위해서 bind를 쓴다.

### 예시

```html
<script>
	let name = 'world';
</script>

<input bind:value={name}>

<h1>Hello {name}!</h1>
```

## Numeric inputs
- input type이 number나 range라면 알아서 형변환 해줌.

### 예시
```html
<script>
  let a = 1;
  let b = 2;
</script>
<input type=number bind:value={a} min=0 max=10>
<input type=range bind:value={a} min=0 max=10>

<p>{a} + {b} = {a + b}</p>

```

## CheckBox inputs
- input type이 checkbox인 경우 상태 토글일때가 있다. 이럴 경우 bind를 쓴다.

### 예시
```html
<input type=checkbox bind:checked={yes}>
```

## Group inputs
- input type이 radio이거나, checkbox이면 bind:group 을 사용하여 동일한 name의 component에 대해서 같은 value 변수를 binding 할 수 있다.
- ```bind:group={변수명}``` 형태로 사용할수 있는데, 변수명은 당연하게도 미리 선언되어 있어야 한다.(초기값은 기왕이면 radion나 checkbox의 default값이 낫지 않을까...)
- 아무 엘리먼트에나 사용하려고 하면 아래와 같은 오류 발생
![ncloud 메인화면](../../assets/images/svelte/6-1.png)

### 예시
```html
<label>
  0	<input type=radio bind:group={scoops} name="scoops" value={1}>
  One scoop
</label>

<label>
  <input type=radio bind:group={scoops} name="scoops" value=2>
  Two scoops
</label>

<label>
  <input type=radio bind:group={scoops} name="scoops" value="3">
  Three scoops
</label>

```

## Textarea inputs
- text input과 같이 ```bind:value```를 동일하게 textarea 엘리먼트에서도 사용할 수 있다.
- bind:value는 또한 동일하게, 변수명과 attribute의 label을 일치시킴으로써 shorthand할 수 있다.

```html
<script>
  let value = `Some words are *italic*, some are **bold**`;
</script>

<textarea bind:value={value} />
```

```html
<textarea bind:value />
```

## Select bindings
- ```bind:value```는 select 엘리먼트에서도 사용할수 있다.
- option은 string보다는 object로 선택된 항목에 대한 object 정보를 bind:value를 통해 변수를 binding하고, 해당 object data를 다른 곳에서 사용하는 방식이다.
- binding변수가 초기화될때까지는 undefined로 남아있기 때문에 잘 고려해서 개발해야한다.

## Select multiple
- select 엘리먼트는 multiple attribute를 가질 수 있고, 이에 대한 처리도 bind:value로 가능하다.

```html
<select multiple bind:value={flavours}>
	{#each menu as flavour}
		<option value={flavour}>
			{flavour}
		</option>
	{/each}
</select>
```
## Contenteditable bindings
- contenteditable attribute가 true인 엘리먼트는 textContent와 innerHTML binding을 지원한다.

### 예시
```html
<script>
	let html = '<p>Write some text!</p>';
</script>

<div
	contenteditable="true"
	bind:innerHTML={html}
></div>

<pre>{html}</pre>

```
### contenteditable이란?
- 사용자가 요소를 편집할 수 있는지 여부의 attribute
- <a href="https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/contenteditable" taget="_blank">contenteditable - MDN 설명</a>

## Each block bindings
- each문 안의 properties에 대한 binding도 가능하다.
- 이 경우 input 태그는 배열로 변형이 되는데, 변형되지 않는 데이터를 선호한다면 이 방법을 피하고, event handler로 처리해야 한다.

### 예시

```html
{#each todos as todo}
<div class:done={todo.done}>
  <input
    type=checkbox
    bind:checked={todo.done}
  >

  <input
    placeholder="What needs to be done?"
    bind:value={todo.text}
  >
</div>
{/each}
```
### 더 알아가기

```html
<div class:done={todo.done}>
```
- 이 구문은 Svelte에서 클래스를 동적으로 추가하는 방법 중 하나이다. 
- class: 접두사는 클래스를 추가하기 위한 것으로, done이 클래스 이름이 됩니다. {todo.done}은 boolean 값으로, todo 객체의 done 속성 값에 따라서 클래스가 추가되거나 추가되지 않습니다.
- 예를 들어, todo.done이 true인 경우에는 <div> 요소에 done 클래스가 추가되고, false인 경우에는 제거됩니다.
- 이를 통해, 조건부 클래스 추가/제거를 쉽게 처리할 수 있습니다.

## Media elements(안쓰일듯)
- audio와 video elements는 몇가지 bind에 사용할 수 있는 특성을 가지고 있다. 해당 page 참조.
- <a href="https://svelte.dev/tutorial/media-elements" taget="_blank">Media elements - Svelte Tutorials</a>

## Dimensions(안쓰일듯)
- 모든 블록레벨의 elements는 bind하여 사이즈를 조절할수 있다.
- <a href="https://svelte.dev/tutorial/dimensions" taget="_blank">Dimensions - Svelte Tutorials</a>

## Component bindings
- DOM elements의 특성을 bind하듯, component의 props 또한 bind할 수 있다.
- 부모 component에서 값 변경시 bind된 데이터는 자식 component의 값도 변경시킨다.

### 예시
```html
<Keypad bind:value={pin} on:submit={handleSubmit}/>
```

## Binding to component instance
- component의 instance에도 그들 스스로 bind할 수 있다. 

### 예시

```html
<script>
	let field;
</script>

<InputField bind:this={field} />
```

## 참고 사이트
<a href='https://svelte.dev/tutorial/text-inputs' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼 - Bindings</a>

 