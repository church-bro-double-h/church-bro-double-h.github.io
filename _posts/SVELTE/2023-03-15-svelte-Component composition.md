---
layout: single
title: "svelte 공식 사이트 Tutorial 정리 ⑭ : Component composition"
categories: svelte
tag: [svelte, front-end]
comments: true
---

# Component composition

## Slots
- 컴포넌트에도 자식 요소를 포함시키기 위해 사용하는 것으로 자식요소의 위치를 지정해준다.

### 예시
- App.svelte에서 Box.svelte라는 컴포넌트를 불러와서 사용한다. 이때 App.svelte에서 자식요소를 Box.svelte로 넘겨서 꽂을 수 있도록 위치를 지정한 것이 slot이다. 

###### App.svelte

```html
<script>
  import Box from './Box.svelte';
</script>

<Box>
  <h2>Hello!</h2>
  <p>This is a box. It can contain anything.</p>
</Box>
```

###### Box.svelte

```html
<div class="box">
  <slot></slot>
</div>

<style>
  .box {
    width: 300px;
    border: 1px solid #aaa;
    border-radius: 2px;
    box-shadow: 2px 2px 8px rgba(0,0,0,0.1);
    padding: 1em;
    margin: 0 0 1em 0;
  }
</style>
```

## Slot fallbacks(대안)
- Slot에 아무것도 전달되지 않았을때 대안을 구현해 놓을 수 있다.

### 예시
- App.svelte에서 Box component를 2번 사용하였는데, 1개는 자식요소를 넣어주었고, 1개는 넣어주지 않았다.
- 자식요소를 넣어준 component는 자식요소가 셋팅되었고, 자식요소를 넣어주지 않은 component는 fallback으로 구현해놓은 부분이 셋팅되었다.

###### App.svelte

```html
<script>
  import Box from './Box.svelte';
</script>

<Box>
  <h2>Hello!</h2>
  <p>This is a box. It can contain anything.</p>
</Box>

<Box/>
```

###### Box.svelte

```html
<div class="box">
  <slot>
    <em>no content was provided</em>
  </slot>
</div>

<style>
  .box {
    width: 300px;
    border: 1px solid #aaa;
    border-radius: 2px;
    box-shadow: 2px 2px 8px rgba(0,0,0,0.1);
    padding: 1em;
    margin: 0 0 1em 0;
  }
</style>
```

## Named slots
- slot을 여러개 사용하는 경우에 slot에 이름을 명명하여 해당 이름의 slot에 자식요소를 전달시킬 수 있다.
- 개쩔고 유용한 기능이다.

### 예시
- App.svelte에서 ContactCard.svelte 파일의 slot에 자식요소를 전달하되, 이름 기준으로 전달해준다.
- 따라서 App.svelte의 span 순서가 바뀌어도 어차피 ContactCard에 이름에 맞게 셋팅되기 때문에 신기하다. 

###### App.svelte

```html
<script>
	import ContactCard from './ContactCard.svelte';
</script>

<ContactCard>
	<span slot="name">
		P. Sherman
	</span>

	<span slot="address">
		42 Wallaby Way<br>
		Sydney
	</span>
</ContactCard>
```

###### ContactCard.svelte

```html
<article class="contact-card">
  <h2>
    <slot name="name">
      <span class="missing">Unknown name</span>
    </slot>
  </h2>

  <div class="address">
    <slot name="address">
      <span class="missing">Unknown address</span>
    </slot>
  </div>

  <div class="email">
    <slot name="email">
      <span class="missing">Unknown email</span>
    </slot>
  </div>
</article>

<style>
  .contact-card {
    width: 300px;
    border: 1px solid #aaa;
    border-radius: 2px;
    box-shadow: 2px 2px 8px rgba(0,0,0,0.1);
    padding: 1em;
  }

  h2 {
    padding: 0 0 0.2em 0;
    margin: 0 0 1em 0;
    border-bottom: 1px solid #ff3e00
  }

  .address, .email {
    padding: 0 0 0 1.5em;
    background:  0 0 no-repeat;
    background-size: 20px 20px;
    margin: 0 0 0.5em 0;
    line-height: 1.2;
  }

  .address {
    background-image: url(/tutorial/icons/map-marker.svg);
  }
  .email {
    background-image: url(/tutorial/icons/email.svg);
  }
  .missing {
    color: #999;
  }
</style>

```

## Checking for slot content
- slot에 컨텐츠를 전달받았는지에 따라 wapper(div 등 감싸는 것)의 class를 적용/미적용, 혹은 {#if}{/if}문 등의 표현식을 사용하고 싶을때 ```{$$slots.전달 컨텐츠의 name}```을 사용함으로써 알수 있다. 
- ```$$slots``` 은 부모 component로부터 전달된 slots의 이름을 key로 갖는 객체이다. 전달된게 없으면 항목이 없다.

### 예시
- App.svelte에서 Project.svelte component 2번, Commnet.svelte component를 1번 사용한다.
- Project component 안에 slot name을 comments로 명명한 자식 컨텐츠를 넣고, 그 안에 Comment component를 다시 넣었다.
- 이때 첫번째 Project component에는 comments라는 자식요소를 넣었지만, 두번쩨 Project component에는 slot에 전달될 contents를 넣지 않았다.
- 따라서 Proejct.svelte에 기술된 $$slots.comments의 값 여부에 따라 class 적용 및 if문에 따라 element를 노출한다.

###### App.svelte

```html
<script>
  import Project from './Project.svelte'
  import Comment from './Comment.svelte'
</script>

<h1>
  Projects
</h1>

<ul>
  <li>
    <Project
      title="Add TypeScript support"
      tasksCompleted={25}
      totalTasks={57}
    >
      <div slot="comments">
        <Comment name="Ecma Script" postedAt={new Date('2020-08-17T14:12:23')}>
        <p>Those interface tests are now passing.</p>
        </Comment>
      </div>
    </Project>
  </li>
  <li>
    <Project
      title="Update documentation"
      tasksCompleted={18}
      totalTasks={21}
    />
  </li>
</ul>

<style>
  h1 {
    font-weight: 300;
    margin: 0 1rem;
  }

  ul {
    list-style: none;
    padding: 0;
    margin: 0.5rem;
    display: flex;
  }

  @media (max-width: 600px) {
    ul {
      flex-direction: column;
    }
  }

  li {
    padding: 0.5rem;
    flex: 1 1 50%;
    min-width: 200px;
  }
</style>
```

###### Comment.svelte

```html
<script>
  export let name;
  export let postedAt;

  $: avatar = `https://ui-avatars.com/api/?name=${name.replace(/ /g, '+')}&rounded=true&background=ff3e00&color=fff&bold=true`;
</script>

<article>
  <div class="header">
    <img src={avatar} alt="" height="32" width="32">
    <div class="details">
      <h4>{name}</h4>
      <time datetime={postedAt.toISOString()}>{postedAt.toLocaleDateString()}</time>
    </div>
  </div>
  <div class="body">
    <slot></slot>
  </div>
</article>

<style>
  article {
    background-color: #fff;
    border: 1px #ccc solid;
    border-radius: 4px;
    padding: 1rem;
  }

  .header {
    align-items: center;
    display: flex;
  }

  .details {
    flex: 1 1 auto;
    margin-left: 0.5rem
  }

  h4 {
    margin: 0;
  }

  time {
    color: #777;
    font-size: 0.75rem;
    text-decoration: underline;
  }

  .body {
    margin-top: 0.5rem;
  }

  .body :global(p) {
    margin: 0;
  }
</style>
```
###### Project.svelte

```html
<script>
  export let title;
  export let tasksCompleted = 0;
  export let totalTasks = 0;
</script>

<article class:has-discussion={$$slots.comments}>
  <div>
    <h2>{title}</h2>
    <p>{tasksCompleted}/{totalTasks} tasks completed</p>
  </div>
  {#if $$slots.comments}
  <div class="discussion">
    <h3>Comments</h3>
    <slot name="comments"></slot>
  </div>
  {/if}
</article>

<style>
  article {
    border: 1px #ccc solid;
    border-radius: 4px;
    position: relative;
  }

  article > div {
    padding: 1.25rem;
  }

  article.has-discussion::after {
    content: '';
    background-color: #ff3e00;
    border-radius: 10px;
    box-shadow: 0 2px 4px rgba(0,0,0,0.2);
    height: 20px;
    position: absolute;
    right: -10px;
    top: -10px;
    width: 20px;
  }

  h2,
  h3 {
    margin: 0 0 0.5rem;
  }

  h3 {
    font-size: 0.875rem;
    font-weight: 500;
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }

  p {
    color: #777;
    margin: 0;
  }

  .discussion {
    background-color: #eee;
    border-top: 1px #ccc solid;
  }
</style>
```

## Slot props
- let이라는 지시어를 사용하여 부모 component ↔ 자식 component 사이에 값을 전달하며 공유할 수 있다.


### 예시
- Hoverable.svelte에서 이벤트 handler에 따라 hovering이라는 변수의 값이 바뀐다.
- 해당 값은 부모 component인 App.svelte에서 ```let:hovering={active}```라고 정의된 active에 값이 전달 및 셋팅된다.
- App.svelte는 active값에 따라 class를 적용하거나 elements를 노출한다.
- Named slots에서도 props 할 수 있다.

###### App.svelte

```html
<script>
  import Hoverable from './Hoverable.svelte';
</script>

<Hoverable let:hovering={active}>
  <div class:active>
    {#if active}
    <p>I am being hovered upon.</p>
    {:else}
    <p>Hover over me!</p>
    {/if}
  </div>
</Hoverable>

<Hoverable let:hovering={active}>
  <div class:active>
    {#if active}
    <p>I am being hovered upon.</p>
    {:else}
    <p>Hover over me!</p>
    {/if}
  </div>
</Hoverable>

<Hoverable let:hovering={active}>
  <div class:active>
    {#if active}
    <p>I am being hovered upon.</p>
    {:else}
    <p>Hover over me!</p>
    {/if}
  </div>
</Hoverable>

<style>
  div {
    padding: 1em;
    margin: 0 0 1em 0;
    background-color: #eee;
  }

  .active {
    background-color: #ff3e00;
    color: white;
  }
</style>
```

###### Hoverable.svelte

```html
<script>
  let hovering;

  function enter() {
    hovering = true;
  }

  function leave() {
    hovering = false;
  }
</script>

<div on:mouseenter={enter} on:mouseleave={leave}>
  <slot hovering={hovering}></slot>
</div>
```




## 참고 사이트
<a href='https://svelte.dev/tutorial/slots' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼 - Bindings</a>

 