---
layout: single
title: "svelte 공식 사이트 Tutorial 정리 ① : Introduction"
categories: svelte
tag: [svelte, front-end]
comments: true
---

# Introduction

## 1. Adding data
- Script에서 선언한 변수를 Markup에서 사용할 수 있다.
- {변수명}

```html
<script>
  let name = 'world';
</script>
 
<h1>Hello {name}!</h1>
```

- 놀랍게도 {}(중괄호)가 갖는 의미는 단순히 변수를 사용한다라는 의미보다는 해당 {}(중괄호)안에서 Javascript를 사용할 수 있다는 점에 있는게 아닌가 싶다.
  따라서 아래와 같은 소스의 구현도 가능한 것이다.

```html
<h1>Hello {name.toUpperCase()}</h1>
``` 

## 2.Dynamic attributes
- 중괄호는 엘리먼트의 속성을 조작할 수 있다.

```html
<script>
  let src = '/tutorial/image.gif';
</script>

<img src={src}>
```
- 변수명과 속성명이 동일하다면 아래와 같이 쓸수도 있다.

```html
<script>
  let src = '/tutorial/image.gif';
  let alt = 'this is alt';
</script>

<img {src} {alt}>
```

## 3.Styling
- 일반 HTML파일처럼 Style태그를 가질 수 있다.

```html
<p>This is a paragraph</p>

<style>
  p {
    color:purple;
    font-family: 'Comic Sans MS', cursive;
    font-size: 2em; 
  }
</style>
```
## 4.Nested components
- 원하는 컴포넌트를 다른 파일로부터 끼워넣을 수 있다.
- nest의 사전적 의미 : 4. [동사][전문 용어] (큰 단위의 정보 속에 작은 단위의 정보를) 끼워 넣다
※ 이후 '컴포넌트를 끼워 넣다'라고 표현

App.svelte 존재
Nested.svelte 존재

```html
<script>
  import Nested from './Nested.svelte'
</script>

<p>This is a paragraph.</p>
<Nested/>

<style>
  p {
    color: purple;
    font-family: 'Comic Sans MS', cursive;
    font-size: 2em;
  }
</style>
```
### ★규칙★ 
- 이때 유저가 정의한 컴포넌트와 HTML태그를 구분하기 위해 <span style="color:red">첫글자를 대문자로 </span> 명명하여야 한다.

## 5. Making an App
- 원하는 text-editor에서 작업할 수 있도록 빌드 툴을 설치해줘야 되는데, svelte에서는 SvelteKit을 추천한다. Vite를 통해 번들링을 한다.
- SvelteKit을 설치하기 위해서는 원하는 디렉토리로 이동하여 아래와 같은 npm 구문을 써준다.

```console
npm create svelte@latest myapp
```
### 유용한 Tool 안내 페이지
<a href="https://sveltesociety.dev/tools">community-maintained integrations.</a>

### SvelteKit 개발환경 셋팅 안내 페이지
<a href="https://svelte.dev/blog/svelte-for-new-developers">Svelte for new developers</a>

### Client-side component API
<a href="https://svelte.dev/docs#run-time-client-side-component-api">component API</a>


## 참고 사이트
<a href='https://svelte.dev/tutorial/making-an-app' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼</a>