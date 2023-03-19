---
layout: single
title: "svelte 공식 사이트 Tutorial 정리 ⓑ : Module context"
categories: svelte
tag: [svelte, front-end]
comments: true
---

# Module context

## Sharing code
- 가끔 약간의 코드를 개개의 component instance 밖에서 실행할 필요가 있다.
- 이를 위해 ```<script context="module">```블록을 선언하여 이 블록에 포함된 코드는 구성요소가 인스턴스화될 때가 아니라 모듈이 처음 평가될때 한번 실행된다.

### 예시
- App.svelte에서 AudioPlayer라는 component를 다수 사용하고 있는데 하나의 component에서 current라는 변수를 넘겨서 구성요소간 communicate 한다. 

###### App.svelte

```html
<script>
  import AudioPlayer from './AudioPlayer.svelte';
</script>

<!-- https://musopen.org/music/9862-the-blue-danube-op-314/ -->
<AudioPlayer
  src="https://sveltejs.github.io/assets/music/strauss.mp3"
  title="The Blue Danube Waltz"
  composer="Johann Strauss"
  performer="European Archive"
/>

<!-- https://musopen.org/music/43775-the-planets-op-32/ -->
<AudioPlayer
  src="https://sveltejs.github.io/assets/music/holst.mp3"
  title="Mars, the Bringer of War"
  composer="Gustav Holst"
  performer="USAF Heritage of America Band"
/>
```

###### AudioPlayer.svelte

```html
<script context="module">
  let current;
</script>

<script>
  export let src;
  export let title;
  export let composer;
  export let performer;

  let audio;
  let paused = true;

  function stopOthers() {
    if (current && current !== audio) current.pause();
    current = audio;
  }
</script>

<article class:playing={!paused}>
  <h2>{title}</h2>
  <p><strong>{composer}</strong> / performed by {performer}</p>

  <audio
    bind:this={audio}
    bind:paused
    on:play={stopOthers}
    controls
    {src}
  ></audio>
</article>

<style>
  article {
    margin: 0 0 1em 0; max-width: 800px;
  }
  h2, p {
    margin: 0 0 0.3em 0;
  }
  audio {
    width: 100%; margin: 0.5em 0 1em 0;
  }
  .playing {
    color: #ff3e00;
  }
</style>
```

## Exports
- 위와 같은 방식으로 함수 또한 export할 수 있다.

### 예시
- App.svelte에서 AudioPlayer라는 component를 다수 사용하고 있는데 하나의 component에서 current라는 변수를 넘겨서 구성요소간 communicate 한다.

###### App.svelte

```html
<script>
  import AudioPlayer, { stopAll } from './AudioPlayer.svelte';
</script>

<button on:click={stopAll}>
  stop all audio
</button>

```

###### AudioPlayer.svelte

```html
<script context="module">
  const elements = new Set();

  export function stopAll() {
    elements.forEach(element => {
      element.pause();
    });
  }
</script>
```

## 참고 사이트
<a href='https://svelte.dev/tutorial/sharing-code' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼 - Bindings</a>

 