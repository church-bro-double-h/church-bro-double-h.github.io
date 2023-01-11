
---
layout: single
title: "이벤트, 이벤트 핸들러, 이벤트 리스너"
categories: javascript
tag: [front-end, javascript, event, event-handler, event-listener]
comments: true
---

## 이벤트
- HTML events : HTML events are "things" that happen to HTML elements. → HTML 구성요소들에게 발생하는 것들
- HTML allows event handler attributes, with JavaScript code, to be added to HTML elements.

## 이벤트 핸들러
- 이벤트가 발생했을 때 그 처리를 담당하는 실행 함수
- 이벤트 발생시 이벤트 리스너에 연결된 이벤트 핸들러가 실행됨.

## 이벤트 리스너
- 특정한 이벤트에 대해서 일어날 동작을 정의
- 지정된 타입의 이벤트가 특정 요소에서 발생하면, 웹브라우저는 그 요서에 등록된 이벤트 리스너를 실행시킴
- 이벤트 리스너와 이벤트 핸들러를 합쳐 이벤트 리스너라고 하기도 함.

|   이벤트   |  이벤트 리스너<br>(이벤트 속성)  |           이벤트핸들러            |
|:-------:|:---------------------:|:---------------------------:|
|  click  |        onclick        |  var click = function() {}  |

## 참고 사이트
<a href='https://codedragon.tistory.com/5743' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># 코드드래곤님의 블로그</a>
<a href='https://www.w3schools.com/js/js_events.asp' target='_blank' style="color:blue; font-size:12px; font-weight:bold;"># w3school</a>
