---
layout: single
title: "svelte 공식 사이트 Tutorial 정리 ⑬ : Advanced styling"
categories: svelte
tag: [svelte, front-end]
comments: true
---

# Advanced styling

## The class directive
- 다른 attribute와 마찬가지로 class들을 javascript attribute를 가지고 명시할 수 있다.

### 예시
- selected라는 class는 표현식이 true인 경우 추가되고, false인 경우에 제거된다.

###### 변경전

```html
<button
  class="{current === 'foo' ? 'selected' : ''}"
  on:click="{() => current = 'foo'}"
>foo</button>
```

###### 변경후

```html
<div class:big>
  <!-- ... -->
</div>
```

## inline styles
- 동적으로 styling 할수도 있다.

### 예시
- style attribute 안에 color 및 opaciti의 value를 동적변수로 할당하여, 변수값 변화에 따라 동적으로 Styling 할 수 있다.

```html
<script>
  let bgOpacity = 0.5;
  $: color = bgOpacity < 0.6 ? '#000' : '#fff';
</script>

<input type="range" min="0" max="1" step="0.1" bind:value={bgOpacity} />

<p style="color: {color}; --opacity: {bgOpacity};">This is a paragraph.</p>

<style>
  p {
    font-family: "Comic Sans MS", cursive;
    background: rgba(255, 62, 0, var(--opacity));
  }
</style>
```

## The style directive
- style 지시어를 사용하여 구문을 단축할 수 있고, 오류를 줄일 수도 있다.

### 예시
- style attribute 안에 color 및 opaciti의 value를 동적변수로 할당하여, 변수값 변화에 따라 동적으로 Styling 할 수 있다.

###### 변경 전

```html
<p style="color: {color}; --opacity: {bgOpacity};">This is a paragraph.</p>
```
###### 변경 후

```html
<p style:color style:--opacity={bgOpacity}>This is a paragraph.</p>
```


## 참고 사이트
<a href='https://svelte.dev/tutorial/classes' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼 - Bindings</a>

 