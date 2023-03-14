---
layout: single
title: "1단계 개발환경 구축"
categories: microFrontend
tag: [microFrontend, ncloud, svelte, sveltekit, nexusRepository]
comments: true
---

## 목표
- IntelliJ 설치(Visual Studio Code 가능 - 유용한 기능 사용의 차이만 존재)
- nodeJS설치
- svelte 프로젝트 설치

## 진행순서

### ① IntelliJ 설치
- Sveltekit 플러그인 등 사용을 위해 설치
- VSC(Vissual Studio Code)도 가능하지만, VCS(Version Control System)을 가시적으로 편리하게 사용하며, 개발 편리성 및 소스 통합성을 위해 IntelliJ로 개발 진행
- <a href='https://www.jetbrains.com/ko-kr/idea/download/#section=windows' target='_blank' style="color:blue; font-weight:bold;">IntelliJ 설치페이지 이동</a>
- 최신버전 설치 후 진행(2023.3.1 버전에서 sveltekit 플러그인 설치시 지원이 안된 문제가 있어서 23년 초창기 EAP 버전을 이용했었다능..)

### ① node.js 설치
- svelte, vite, 기타 패키지를 용이하게 설치하기 위함.
- <a href='https://nodejs.org/ko/' target='_blank' style="color:blue; font-weight:bold;">node.js 설치페이지 이동</a>
- 최신버전 LTS 다운로드 후 설치
#### 정상설치여부 결과  
![nodejs 정상설치 확인](../../assets/images/microFrontend/2-1.png) 

### ② sveltekit 패키지 다운로드 및 설치

#### 진행순서

##### 1단계 - 패키지 다운로드 및 설치
- 원하는 경로로 가서 powershell창을 켜서 명령어 입력
```shell
  npm create svelte@latest kjbMobileWeb
```
- NPM(Node Package Manager)라는 친구한테 npmjs.com 이 주소에 있는 package를 생성(create)할건데
- svelte라는 패키지의 latest(최신버전)을 설치할꺼고  
- 프로젝트의 이름은 kjbMobileWeb 으로 할꺼야!
- 그럼 아래와 같이 어떤 프로젝트를 원하는지 질문을 던진다.
![nodejs 정상설치 확인](../../assets/images/microFrontend/2-2.png)

###### 선택사항
- 질문 : 어떤 svelte 앱 템플릿을 원해?
(본인은 목표한 바와 같이 1개의 Main 프로젝트, 여러개의 Process 프로젝트(TASK를 slot으로 사용하는), 여러 개의 TASK Library, 여러개의 컴포넌트 Library를  
  - Sveltekit demo app : 어느 정도 예시가 포함된 템플릿
  - Skeleton project : 기본적인 뼈대만 있는 템플릿
  - Library project :  library용 프로젝트

- 질문 : 어떤 svelte 앱 템플릿을 원해?
  - Sveltekit demo app : 어느 정도 예시가 포함된 템플릿
  - Skeleton project : 기본적인 뼈대만 있는 템플릿
  - Library project :  library용 프로젝트

- 질문 : 어떤 svelte 앱 템플릿을 원해?
  - Yes, using JavaScript with JSDoc comments
  - Skeleton project : 기본적인 뼈대만 있는 템플릿
  - Library project :  library용 프로젝트














★ 해당 블로그는 끝없는 시행착오의 과정입니다. 문과 출신 개초보 프로삽질러 개발자라 용어의 사용이 정확하거나 적합하지 않을 수 있습니다. 혹시 잘못된 부분은 댓글 달아주시면 확인 후 많이 배우며 시정조치 하겠습니다.. 그리고 개발을 시작하는 분들에게도 작게나마 도움이 되길 바랍니다.


























