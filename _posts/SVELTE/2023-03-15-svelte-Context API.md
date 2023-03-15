---
layout: single
title: "svelte 공식 사이트 Tutorial 정리 ⑮ : Context API"
categories: svelte
tag: [svelte, front-end]
comments: true
---

# Context API
- Context API는 데이터와 함수를 props로 계속 전달하거나 많은 이벤트를 dispatch하지 않고 component끼리 '대화'할 수 있는 메커니즘을 제공.

## setContext and getContext
- ```setContext(key, context)```를 호출하면 어떤 자식 컴포넌트든 ```const context = getContext(key)```로 컨텍스트를 검색할 수 있다.
- 컨텍스트 객체는 원하는 대로 어떤 것이든 될 수 있다.
- 라이프사이클 함수와 마찬가지로 setContext 및 getContext는 컴포넌트 초기화 중에 호출해야 한다.
- 기술적으로 어떤 값을 키로 사용할 수 있으나 문자열을 사용하면 다른 컴포넌트 라이브러리가 같은 키를 실수로 사용할 수 있어서, Symbol(): 을 사용하여 고유키를 맵핑하는게 좋다.

### Context와 Store의 차이
- Store는 앱의 모든 부분에서 사용이 가능하지만 Context는 해당 component와 하위 component에서만 사용이 가능.
- Context는 한 component의 상태가 다른 component의 상태에 영향을 미치지 않고 여러 인스턴스의 component를 사용하는데 유용하다.
- 두 가지를 함께 사용할수도 있어, 시간이 지남에 따라 변경되는 값은 store로 표현해야 한다.

#### 예시
```javascript
const { these, are, stores } = getContext(...);
```

## 참고 사이트
<a href='https://svelte.dev/tutorial/slots' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼 - Bindings</a>

 