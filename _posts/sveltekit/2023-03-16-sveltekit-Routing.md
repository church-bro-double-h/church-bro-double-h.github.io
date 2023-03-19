---
layout: single
title: "sveltekit 공식 사이트 Tutorial 정리 ② : Routing"
categories: svelte
tag: [svelte, sveltkit, front-end, back-end]
comments: true
---

# Routing

## Pages
- 파일 시스템 기반 Routing을 사용.
- Route는 src/routes 디렉토리 내에 있다.
- 각 Directory가 +page.svelte 파일을 포함하고 있다면 앱에서 route를 생성한다.

### 개발 방법
- src/routes/ 아래 폴더를 만들고 해당 폴더에 +page.svelte라는 파일을 추가 하면 됨.

## Layouts
- app의 다른 route들은 종종 공통적인 UI를 공유한다. 각 +page.svelte 에서 반복하는 대신, 같은 directory 내 모든 route에 적용되는 +layout.svelte component를 사용할 수 있다.

### 개발 방법
- 같은 directory 내에 모든 route에 적용되는 +layout.svelte component 생성
- +layout.svelte 파일에 반복되는 element 구현
- <slot/> 을 정의한 곳에 page 내용이 렌더링됨.
- +layout.svelte 파일은 형제 및 하위 route에 적용되며 중첩이 가능하다.

## Route parameter
- 폴더명을 변수로 둬서 동적으로 routing을 할 수도 있다.

### 개발방법
- ```src/routes/blog/[(변수명)]/+page.svelte```

### Multiple route 예시
- ```src/routes/blog/[(변수명)]x[(변수명)]/+page.svelte```



## 참고 사이트
<a href='https://learn.svelte.dev/tutorial/pages' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼</a>