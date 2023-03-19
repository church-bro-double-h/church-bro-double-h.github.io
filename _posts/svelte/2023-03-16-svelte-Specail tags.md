---
layout: single
title: "svelte 공식 사이트 Tutorial 정리 ⓒ : Special tags"
categories: svelte
tag: [svelte, front-end]
comments: true
---

# Special tags

## The @debug tag
- 말그대로 debugger;와 동일

### 예시

###### debugger trigger
```html
{@debug}
``` 

###### 변수 확인 : console.log보다 유용
```html
{@debug 변수명}
```

## HTML tags
- html로 바꿔주는 건데 XSS 공격에 노출될 위험이 있으므로 미사용 권장

### 예시

```html
<script>
	let string = `this string contains some <strong>HTML!!!</strong>`;
</script>

<p>{@html string}</p>
``` 

## 참고 사이트
<a href='https://svelte.dev/tutorial/debug' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼 - Bindings</a>

 