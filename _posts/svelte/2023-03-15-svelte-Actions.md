---
layout: single
title: "svelte 공식 사이트 Tutorial 정리 ⑫ : Actions"
categories: svelte
tag: [svelte, front-end]
comments: true
---

# Action
- 엘리먼트 레벨의 라이프사이클 함수입니다. 다음과 같은 경우에 유용하다.
  - 타사 라이브러리와의 인터페이스
  - 지연 로딩되는 이미지
  - 툴팁
  - 사용자 정의 이벤트 핸들러 추가

## The use directive
- use라는 지시자를 썼는데, 다른 js에 있는 함수 엘리먼트에 적용하였다.

### 예시
- App.svelte의 div에 click-outside.js의 함수를 적용하는 예시.
###### App.svelte

```html
<script>
  import { clickOutside } from "./click_outside.js";

  let showModal = true;
</script>

<div class="box" use:clickOutside on:outclick={() => (showModal = false)}>
Click outside me!
</div>
```

###### click_outside.js

```javascript
export function clickOutside(node) {
	const handleClick = (event) => {
		if (!node.contains(event.target)) {
			node.dispatchEvent(new CustomEvent("outclick"));
		}
	};

	document.addEventListener("click", handleClick, true);

	return {
		destroy() {
			document.removeEventListener("click", handleClick, true);
		}
	};
}

```

## Adding parameters
- use를 사용할때 parameter를 넘길수도 있다.

### 예시
- longpress.js의 longpress 함수를 호출할때 duration을 parameter로 넘겨서 함수 기능이 추가되었다.  

###### App.svelte
```html
<script>
	import { longpress } from './longpress.js';

	let pressed = false;
	let duration = 2000;
</script>

<label>
	<input type=range bind:value={duration} max={2000} step={100}>
	{duration}ms
</label>

<button use:longpress={duration}
	on:longpress="{() => pressed = true}"
	on:mouseenter="{() => pressed = false}"
>press and hold</button>


```

###### click_outside.js
```javascript
export function longpress(node, duration) {
	let timer;
	
	const handleMousedown = () => {
		timer = setTimeout(() => {
			node.dispatchEvent(
				new CustomEvent('longpress')
			);
		}, duration);
	};
	
	const handleMouseup = () => {
		clearTimeout(timer)
	};

	node.addEventListener('mousedown', handleMousedown);
	node.addEventListener('mouseup', handleMouseup);

	return {
		update(newDuration) {
			duration = newDuration;
		},
		destroy() {
			clearTimeout(timer);
			node.removeEventListener('mousedown', handleMousedown);
			node.removeEventListener('mouseup', handleMouseup);
		}
	};
}

```

## 참고 사이트
<a href='https://svelte.dev/tutorial/actions' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼 - Bindings</a>

 