---
layout: single
title: "svelte 공식 사이트 Tutorial 정리 ⑪ : Animations"
categories: svelte
tag: [svelte, front-end]
comments: true
---

# The animate directive
- 전환하지 않는 요소에 대한 모션을 적용할때 animation 지시자를 사용한다.

### 예시

```html
<script>
    import { flip } from 'svelte/animate';
</script>
<label
  in:receive="{{key: todo.id}}"
  out:send="{{key: todo.id}}"
  animate:flip="{{duration: 200}}"
>

```

## 참고 사이트
<a href='https://svelte.dev/tutorial/animate' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼 - Bindings</a>

 