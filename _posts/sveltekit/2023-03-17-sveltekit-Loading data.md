---
layout: single
title: "sveltekit 공식 사이트 Tutorial 정리 ③ : Page data"
categories: svelte
tag: [svelte, sveltkit, front-end, back-end]
comments: true
---

# Loading data

## Page data
- app의 각 page는 +page.svelte 파일과 +page.server.js 파일에 load 함수를 선언할 수 있다.
- 해당 모듈은 server에서만 실행된다.


### sveltekit의 핵심적인 역할 3가지

#### Routing
- 들어오는 요청에 어떤 루트가 일치하는지 결정한다.

#### Loading
- route에 필요한 데이터를 가져온다.

#### Rendering
- 서버에서 HTML을 생성하거나 Browser에서 DOM을 update 시킨다.






## 참고 사이트
<a href='https://learn.svelte.dev/tutorial/page-data' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼</a>