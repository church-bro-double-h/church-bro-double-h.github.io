---
layout: single
title: "어플리케이션 개발환경 구축을 위한 cloud 환경설정 - 목표설정"
categories: cloud
tag: [cloud, ncloud, svelte, sveltekit]
comments: true
---

# cloud 환경구성

## 목표
- sveltekit application : sveltekit 서비스가 가능한 서버 만들기
- gitlab application : 소스 버전관리를 위한 gitlab 만들기
- nexus application : svelte library관리를 위한 nexus repository 만들기
- jenkins application : 배포 및 CI/CD를 위한 jenkins 만들기
- kubernetes 운영 : 위 application들은 모두 kubernetes로 관리하기
- docker 이미지 만들기 

## 접근법
- 개발 소스를 올리려면 먼저 서버 환경이 준비되어야 합니다.
- 여러개의 컨테이너가 필요하므로 kubernetes를 띄우는게 좋겠다라는 생각을 하였습니다.
- 각각의 어플리케이션이 컨테이너에서 실행될텐데, 각각의 pod를 만들어서 띄우는게 좋을지 고민해봤을대, sveltekit application의 배포가 자주 일어날 것이므로, sveltekit application은 pod를 따로 두고, gitlab, nexus, jenkins는 동일한 pod에서 구현하는 것으로 할 예정입니다.
- 또한 위 개발환경은 추후 폐쇄망 사용을 위해 docker image 떠서 보관토록 하겠습니다.

## 다음 post 목표
- ncloud환경에서 kubernetes service cluster를 생성
- 2개의 pod를 생성하고 각각 1 / 3개의 container를 생성

★ 해당 블로그는 끝없는 시행착오의 과정입니다. 문과 출신 개초보 프로삽질러 개발자라 용어의 사용이 정확하거나 적합하지 않을 수 있습니다. 혹시 잘못된 부분은 댓글 달아주시면 확인 후 시정토록 하겠습니다. 많이 배우겠으니 많은 지식의 공유가 이루어졌으면 좋겠습니다. 그리고 개발을 시작하는 분들에게도 작게나마 도움이 되길 바랍니다.
