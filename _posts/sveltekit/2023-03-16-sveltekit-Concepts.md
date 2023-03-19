---
layout: single
title: "sveltekit 공식 사이트 Tutorial 정리 ① : Concepts"
categories: svelte
tag: [svelte, sveltkit, front-end, back-end]
comments: true
---

# Concepts

## What is SvelteKit?
- Svelte : component Framework
- Sveltekit : 제품수준의 App Framework
- 기본적으로 server side rendering. SPA로 전환 가능.

### 특징
- 라우팅
- 서버 사이드 렌더링
- 데이터 가져오기
- 서비스 워커
- TypeScript 통합
- 사전 렌더링
- 싱글 페이지 앱
- 라이브러리 패키징
- 최적화된 제품 빌드
- 다양한 호스팅 제공 업체에 배포

## Project structure

### package.json
- 프로젝트 종속성 및 Sveltekit CLI와 상호작용하는 다양한 스크립트 명시
- "type" : "module" - .js 파일이 기본적으로 네이티브 Javascript모듈로 처리된다는 것을 의미

### svelte.config.js
- 프로젝트 구성을 포함.
- <a href='https://kit.svelte.dev/docs/configuration' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Configuration Document</a> 

#### Configuration 설정값 설명

##### adapter ★★★
- vite build할때 실행되는 것으로 서로 다른 플랫폼에 대한 출력물이 어떻게 변화 하는지 결정
- <a href='https://kit.svelte.dev/docs/adapters' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Adapters Document</a>

##### alias ★
- import 문의 값을 대체하기 위해 사용되는 별칭 정의하는 격체

##### appDir ★
- paths.assets에 대한 상대 경로로 빌드된 js 및 css 파일 및 가져온 자산이 제공되는 디렉토리

##### csp
- 컨텐츠 보안 정책 구성. resource를 load할 수 있는 위치를 제한하여 사용자를 XSS 공격으로부터 보호하는데 도움

##### csrf
- 크로스 사이트 요청 위조 공격(Cross-site request forgery, CSRF)에 대한 보호 기능

##### embedded ★★
- 현재 프로젝트 app이 더 큰 app에 포함되어 잇는지 여부로 해당 value가 true 면 부모에 대한 navigation 관련 event listener를 추가하고, 위치 경로 명에서 유추하는 대신 서버에서 매개변수 전달

##### env
- 환경 변수 구성 

##### files
- 프로젝트 내에서 각각의 파일을 찾을 수 있는 경로에 대한 설정
```
assets?: string;
DEFAULT "static"
정적 파일을 찾을 수 있는 경로입니다. 보통 CSS, 이미지, 폰트 등의 파일이 해당 경로에 위치합니다.

hooks?: string;
DEFAULT "src/hooks"
SvelteKit에서 사용하는 hook 파일들이 위치하는 경로입니다.

lib?: string;
DEFAULT "src/lib"
재사용 가능한 함수와 클래스 등의 모듈이 위치하는 경로입니다.

output?: string;
DEFAULT "build"
빌드된 애플리케이션의 출력 경로입니다. 빌드 시 생성된 파일들은 해당 경로에 위치합니다.

routes?: string;
DEFAULT "src/routes"
사이트의 페이지와 API 엔드포인트를 정의하는 파일들이 위치하는 경로입니다.

serviceWorker?: string;
DEFAULT "src/service-worker.ts"
Service Worker 파일이 위치하는 경로입니다. Service Worker를 사용하지 않으려면, 이 값을 null로 설정하세요.

setup?: string;
DEFAULT "src/setup"
페이지가 렌더링되기 전에 실행되는 스크립트들이 위치하는 경로입니다.

template?: string;
DEFAULT "src/app.html"
사이트의 HTML 템플릿 파일이 위치하는 경로입니다. 이 파일은 페이지에 대한 초기 HTML을 제공합니다.
```

##### inlineStyleThreshold
- HTML의 head 안에 <style> 블록 내부에 있는 inline CSS의 파일 최대 길이를 지정함으로써 page에서 필요한 모든 CSS 파일 중 이 값보다 작은 팡르은 병합되어 style블록 안에 inline으로 삽입

###### 장점
- 초기 요청수가 줄어들어 First Contentful Paint 점수 향상
- 신중하게 사용

###### 단점 
- HTML 출력이 더 커지고 브라우저 캐시 효과가 감소

##### moduleExtensions
- SvelteKit이 모듈로 처리할 파일 확장자들의 배열

##### outDir
- SvelteKit에서 개발 및 빌드 중에 파일을 작성하는 디렉토리 
- 이 디렉토리는 버전 관리에서 제외

##### output
- 빌드 출력 형식과 관련된 옵션

##### paths
- app 파일이 제공되는 절대경로.

##### prerender
- 

##### serviceWorker
- 

##### typescript
- 

##### version
- 

### src
- app의 source code 구현
- src/app.html은 page template(%sveltekit.head%와 %sveltekit.body%를 적절히 대체)
- src/routes : app의 route 정의

### static
-  배포할때 포함해야하는 assets 포함.

## Server and client
- Sveltekit 앱은 server와 client 두가지 개별적인 entities가 함께 작동
- Server : 요청을 응답으로 바꿈
- Client : browser에서 load 되는 javascript



## 참고 사이트
<a href='https://learn.svelte.dev/tutorial/introducing-sveltekit' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># Svelte 공식사이트 튜토리얼</a>