---
layout: single
title: "svelte 공식 사이트 Tutorial 정리 ⑦ : Lifecycle"
categories: svelte
tag: [svelte, front-end]
comments: true
---

# Lifecycle
- 모든 컴포넌트는 생성되면서 시작되고, 소멸될때 끝나는 Lifecycle을 가진다. 이러한 Lifecycle 순간에 실행할 수 있는 함수를 svelte에서 제공한다.

## onMount
- 컴포넌트가 처음 DOM에 렌더링된 후에 실행되는 함수.

### 예시

```html
<script>
  import { onMount } from 'svelte';

  let photos = [];

  onMount(async () => {
    const res = await fetch(`/tutorial/api/album`);
    photos = await res.json();
  });
</script>
```

## onDestroy
- 컴포넌트가 파괴될때 코드를 실행하고 싶으면, oneDestory를 사용하면 된다.

### 예시
- 해당 컴포넌트가 파괴되면 interval 함수를 초기화하여 움직이지 않게 하며 메모리 누수를 방지한다.
- onDestory되지 않으면 함수가 계속 실행되어 메모리누수가 발생한다.

```html
<script>
  import { onDestroy } from 'svelte';

  let counter = 0;
  const interval = setInterval(() => counter += 1, 1000);

  onDestroy(() => clearInterval(interval));
</script>
```

## onDestroy
- 컴포넌트가 파괴될때 코드를 실행하고 싶으면, onDestory를 사용하면 된다.

## beforeUpdate and afterUpdate
- beforeUpdate : DOM이 업데이트 되기 전에 실행
- afterUpdate : DOM이 업데이트 된 후에 실행

### 예제
- 채팅 앱에서 채팅 입력으로 인한 DOM영역 변경시 스크롤링 기능 때 사용

```html
<script>
  import { tick } from 'svelte';

  let text = `Select some text and hit the tab key to toggle uppercase`;

  async function handleKeydown(event) {
    if (event.key !== 'Tab') return;

    event.preventDefault();

    const { selectionStart, selectionEnd, value } = this;
    const selection = value.slice(selectionStart, selectionEnd);

    const replacement = /[a-z]/.test(selection)
      ? selection.toUpperCase()
      : selection.toLowerCase();

    text = (
      value.slice(0, selectionStart) +
      replacement +
      value.slice(selectionEnd)
    );

    await tick();
    this.selectionStart = selectionStart;
    this.selectionEnd = selectionEnd;
  }
</script>
```

## tick
- 언제든 호출할 수 있음. 
- 예제에서 tick함수 실행시 컴포넌트 상태 업데이트시 DOM을 즉시 업데이트 하지 않고, tick 함수를 즉시 실행하여, tab을 누를 경우 dom변경으로 인해 커서가 끝으로 가지 않고, 해당 영역 그대로 다시 재지정되는 것이다.

## 참고 사이트
<a href='https://svelte.dev/tutorial/onmount' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼 - Bindings</a>

 