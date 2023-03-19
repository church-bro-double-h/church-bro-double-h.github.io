---
layout: single
title: "svelte 공식 사이트 Tutorial 정리 ⑨ : Motion"
categories: svelte
tag: [svelte, front-end]
comments: true
---

# Motion

## Tweened
- Svelte는 UI를 번지르르하게 animation하는 도구를 제공한다.
- 대표적으로 progress store를 tweened 하는 것이다.

### tweening animation이란?
- Inbetweening의 줄임말로 두 키프레임 사이에 인비트윈이라고 하는 중간 프레임을 만드는 것과 관련된 애니메이션 프로세스 

### tweened 옵션
- delay : 시작되기 전의 밀리초
- duration : 밀리초 또는 (from, to) => 밀리초 함수. 값의 변화가 클수록 긴 트윈을 지정
- easing : linear, quadIn, quadOut, quadInOut, cubicIn, cubicOut, cubicInOut, quartIn, quartOut, quartInOut, quintIn, quintOut, quintInOut, sineIn, sineOut, sineInOut, expoIn, expoOut, expoInOut, circIn, circOut, circInOut, elasticIn, elasticOut, elasticInOut, backIn, backOut, backInOut, bounceIn, bounceOut, bounceInOut 또한 사용자 정의 p => t 함수 [p는 진행도(0 ~ 1 사이의 값)를, t는 easing된 값]
- interpolate — 임의의 값들 간 보간에 사용할 (from, to) => t => value 함수. 기본적으로 Svelte는 숫자, 날짜 및 동일한 구조를 가진 배열과 객체 (숫자 및 날짜 또는 다른 유효한 배열과 객체만 포함하는 경우) 사이를 보간합니다.
- set 및 update 메서드에서도 이러한 옵션을 두 번째 인수로 전달하여 기본값을 덮어쓸 수 있다. set 및 update 메서드는 모두 트윈이 완료될 때 해결되는 프로미스를 반환

### 예시

```html
<script>
	import { tweened } from 'svelte/motion';
	import { cubicOut } from 'svelte/easing';

	const progress = tweened(0, {
		duration: 400,
		easing: cubicOut
	});
</script>

<progress value={$progress}></progress>

<button on:click="{() => progress.set(0)}">
	0%
</button>

<button on:click="{() => progress.set(0.25)}">
	25%
</button>

<button on:click="{() => progress.set(0.5)}">
	50%
</button>
<style>
  progress {
    display: block;
    width: 100%;
  }
</style>
```

## Spring
- 자주 변경되는 값에 더 잘 대응되는 tweened의 대안.

### 예시

```javascript
	import { spring } from 'svelte/motion';

	let coords = spring({ x: 50, y: 50 }, {
		stiffness: 0.1,
		damping: 0.25
	});

```

## 참고 사이트
<a href='https://svelte.dev/tutorial/tweened' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼 - Bindings</a>

 