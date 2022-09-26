---
layout: single
title: "코코아톡 클론코딩 정리"
categories: nomadcoders
tag: [html, css, nomad]
toc: true
comments: true
--- 

## 1 [2020 UPDATE] INTRODUCTION

### 1.1 Read This First

### 1.2 Welcome

### 1.3 Software Requirements

### 1.4 Join the Challenge

### 1.5 What Makes a Website?
- 웹사이트는 단지 text 파일이다.
- 브라우저가 text를 이해해서 웹사이트를 구현해주는 것이다.

### 1.6 What is HTML
- 웹사이트는 2 or 3 가지 종류의 text(=language)로 되어 있다.
- HTML(Hyper Text Markup Language), CSS(Cascading Style Sheets), Javascript
- HYTML은 브라우저에게 content가 무엇인지 알려주는 것이다.

<span style="color:yellow"> ▷ Cascading : 사전적인 의므로 폭포라는 뜻, CSS의 서두를 담당할 정도로 철학을 담고 있다.</span> 

### 1.7 What is CSS
- CSS는 HTML과 함께 사용한다.
- CSS는 browser에게 website의 content가 어떻게 보여야 할지 알려준다.
- HTML은 뼈대만 있는 웹사이트이고, CSS는 뼈대위의 살점과 같은 것이다.

### 1.8 What is Javascript
- Website의 뇌와 같은 역할을 한다.
- interactivity(동적 상호작용)을 한다.

## 2 [2020 UPDATE] LEARNING HTML

### 2.0 Our First HTML File
- <span style="color:yellow;"> 폴더명(프로젝트명)과 파일명은 항상 소문자로 작성해야한다.</span>

### 2.1 Setup and Errors

### 2.2 Our First HTML Tage
- tag가 있고 content가 있고 tag를 닫아주면서 끝낸다.
- h1 : header number 1
- 올바른 text와 올바른 위치에 올바른 tag를 사용하면 브라우저가 이해하여 보여준다.
- 암기할 필요가 전혀 없고 이해만 하면된다.

### 2.3 More Tags and Prettier
- ul : unorder list
- ol : order list

### 2.4 Tag Attributes
- attributes : 태그에 부가적인 정보를 추가하는 것. 이미 정의된 attribute 빼고는 아무거나 선언해서 사용해도 상관은 없다.(브라우저가 이해만 못할뿐)

#### a(anchor) : 다른 웹사이트로 이동하는 방법. 사용하는데 추가적인 정보(어디로 이동)를 넣어줘야 함.
```html
  ex) <a href="http:google.com">Go to google.com</a>
```
- target(속성)
  - _self : 현재 위도우창에 그대로 링크된 웹페이지를 여는 속성
  - _blank : 새 윈도우 창을 열어서 웹페이지를 여는 속성
  - _parent : 현재 프레임의 부모 프레임에서 새 페이지 열림
  - _top : 최상위(부모) 프레임에서 열림
- self-closing tag : 자체 닫기 태그

#### img : 이미지태그
```html
  ex) <img src="이미지링크주소" />
```

### 2.5 More Tags and Head
- HTML문서의 구조를 작성하는 방법이 있다.(RULE)

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Home - My first website</title>
    </head>
    <body>

    </body>
</html>
```
- head : 외부적으로 보이지 않는 웹사이트의 환경을 설정
- body : 사용자가 볼 수 있는 content 보여줌

### 2.6 Its All About the Head
- meta 태그 : 부가적인 정보
- content, name, charset(브라우저에게 text를 어떻게 그려달라는지 말해주는 태그.(한글와 같은 경우 깨질 수 있음))
- charset="utf-8" 을 꼭 넣어줘야함.
- html 태그의 lang attribute : 사이트에서 주요 사용되는 언어가 무엇인지 검색엔진에게 알려줌. (lang="kr")
- head 안에서 브라우저 탭 이미지를 설정할 수 있다.

```html
    <head>
        <link rel="shortcut icon" sizes="16x16 32x32 64x64" href="이미지경로">
    </head>
```
- 검색엔진에 보여주는 설명을 설정할수도 있고, 카카오톡으로 공유시 보여지는 이미지 및 설명을 설정할 수 도 있다.

### 2.7 More Tags
- w3school 보다는 mdn 사이트를 이용하는게 좋다.
- p태그(paragrap) : 길이가 긴 문장에 사용
- abbr태그 : 텍스트에 말풍선을 줄 수 있음. : title attribute에 설명을 넣어줌.
- site태그 : 이탤릭체로 보임
- code 태그 : 코드처럼 보임
- mark 태그 : 형관펜으로 칠해짐
- strong 태그 : 텍스트를 뚱뚱하게 보이게함
- sub 태그 : 글자가 아래 쪽으로 형성
- sup 태그 : 글자가 위 쪽으로 형성
- audio 태그 : 소리를 켜줌

### 2.8 Form Tags
- Form 태그 않에 많은 태그를 넣을 수 있다.
- input 태그 type * color : 색상을 선택할 수 있음.

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Home - My first website</title>
    </head>
    <body>

    </body>
</html
```
- head : 외부적으로 보이지 않는 웹사이트의 환경을 설정
- body : 사용자가 볼 수 있는 content 보여줌

### ※ HTML 구성요소 문서
https://developer.mozilla.org/ko/docs/Web/HTML/Element

### 2.9 More Tags and IDs
- Form 태그를 더 예쁘게 만들어봄
- label 태그 : label은 input 태그랑 같이 있어야 동작함.
```html
<label for="profile">Profile Photo</label>
<input id="profile" type="file" accept=".png, .pdf"/>
```
- input 태그의 type 입력시 적절성 여부를 판단해줌.
- id
- unique identifier.
- body 안의 어떤 태그에도 해당 attribute를 넣을 수 있음.
- 각 element는 하나의 id를 가질 수 있고, 동일한 id를 넣을 수 없다.

### 2.10 Semantic HTML
- 어떤 태그들은 의미가 있고, 어떤 태그들은 의미가 없다.
- semantic : 문서를 보기만해도 그 의미를 짐작할수 있는 것.
- 아무런 의미가 없는 태그
  - div(division) 태그 : 박스라고 생각하면됨. 기본적으로 box는 양 옆에 붙어 있을 수 없음.
  - header 태그 : div를 대체할 수 있음. 동일한 박스. 그러나 프로그래머들이 header라는 걸 인식할 수 있도록 하는 태그.
  - main 태그
  - footer 태그

## 3 [2020 UPDATE] LEARNING CSS

### 3.0 How to Add CSS to HTML
- CSS를 주입하는 방법
  - HTML 파일 안에 같이 넣는다.
  - HTML과 CSS파일을 따로 둔다.
- HTML 파일에 CSS를 넣는 방법
  - head 태그 안에 sytle태그를 넣어준다.
- HTML과 CSS파일을 따로 두는 법. : HTML파일과 CSS파일을 따로 두는게 적합하다.
  - css파일을 만들고, link르 통해 css파일과 html파일과의 관계를 선언해준다.

```html
<link href="style.css" rel="stylesheet">
```

### 3.1 Writing Our First CSS Lines
- 3가지 규칙만 지키면 된다.
- CSS가 하는 일은 HTML 태그를 가리키는 일이다. = selector
  - selector는 많은 속성을 가질 수 있고, 해당 속성들을 curly bracket(중 괄호)으로 묶는다.
  - semicolon을 이용해 한 줄을 선언한다.
  - 띄어쓰기, 밑줄, 슬래쉬등을 사용하면 안된다.
### 3.2 What Does Cascading Mean
- Cascading이라는 의미처럼 HTML의 위에서 아래로 순서대로 적용된다.
- inline CSS : style태그 안에 적용하는 CSS
- external CSS : 외부 CSS파일을 Link하여 적용하는 CSS

```html
<p style="color:red; font-weight:bold;">잘못알고 있었던 지식 : inline CSS가 external CSS 보다 우선적용되는줄 알았지만, HTML문서상의 적용상의 순서 문제였다.</p>
```

### 3.3 Blocks and Inlines
- 모든 속성들을 알 필요는 없다.
- 모든 웹사이트들은 box들로 design을 한다.
- block : box들(div등 sementicTags)은 다른 box 옆에 위치하지 않는다.
  - paragraph
  - image
- inline(in the same line) : 옆에 다른 elements가 올 수 있음.
  - span
  - a

### 3.4 Margin Part One
- block에만 있는 특징.
- block을 inline으로 inline을 block으로 바꾸는게 가능할까???
  - css의 display property를 통해 가능.
  - block은 높이와 너비가 있고, inline은 없다.
- block이 가지고 있는 특징 3가지
  - margin : box의 border 바깥에 있는 space
  - padding
  - border
- 브라우저는 자동으로 요소들에게 속성을 준다.
  - debbuging mode를 통해 css확인시 user agent stylesheet라고 되어 있는 부분은 브라우저가 준 속성이다.

### 3.5 Margin Part Two
- 방향없이 margin을 주면 사방이 다 적용된다.
- margin : 위아래 20xp, 좌우 15px 적용
```css
body {
    margin: 20px 15px;
}
```

- margin : 위20px, 오른쪽 5px, 아래 12px, 왼쪽 9px 시계방향대로 적용
```css
body {
    margin: 20px 5px 12px 9px;
}
```
- collapsing margins : 내부 elements의 경계와 외부 block의 경계가 같을 때 margin-top, margin-bottom이 동일하게 적용되는 현상. top, bottom 에만 적용.

### 3.6 Paddings and IDs
- padding : box의 inside안에 있는 space
- margin과 동일한 방법으로 적용한다.
- id에 css를 주려면 `#id`를 사용한다.

### 3.7 Border
- border : box의 경계
- 다른종류의 border는 별로라 한 종류만 씀.
- '*' : everything

### 3.8 Classes
- 일부에만 CSS를 적용하고 싶을때 사용.

### 3.9 Inline Block
- inline인 element를 block형태로 만들어 높이를 가지게 하고, element의 옆에 다른 element를 위치할 수 있게 한다.
- 그러나 문제가 많아서 좋지 않다.

### 3.10 Flexbox Part One
- flexbox : inline-block의 문제를 해결하기 위해 나온 개념.
- 사용 원칙
  - 오직 부모 element에만 적용해야함.
  - 주축(main axis - 수직), 교차축(cross axis - 수평)
- 사용방법
  - display:flex;
  - justify-content : 속성을 통해 자식 element들을 이동시키거나 배열할 수 있음. 주축에 적용.
  - align-item : 교차축에 적용
- 새로운 용어
  - viewpoint = screen
  - vh = viewpoint height

### 3.11 Flexbox Part Two
- flex-direction : flexbox의 주축과 교차축을 바꾸기 위한 속성
  - row : 수평
  - column : 수직
  - default : row
- flex-wrap : element를 같은 줄에 위치시킬 수 있음.
- wrap-reverse, row-reverse등의 속성을 통해 위치를 조정할 수 있음.

### 3.12 Fixed
- 화면을 고정시키고 싶을때 사용
- Netflix의 메뉴와 같이 최 앞단에 위치시킴.(top, bottom, left, right등의 property를 줬을때)
```css
body {
    position: fixed;
}
```
### 3.13 Relative Absolute
- 'position: static' : 레이아웃이 박스를 처음 위치하는 곳에 두는 것
- 'position: relative' : 아주 조금 위치를 옮기고 싶을때 사용. element가 처음 위치한 곳을 기준으로 위치 조정
- 'position: absolute' : 가장 가까운 relative 부모를 기준으로 이동

### 3.14 Pseudo Selectors part One 
- 원하는 component를 선택해서 style을 apply하고 싶을때 사용
```css
div:first-child{
 background-color: #00c918;
}
div:last-child{
  background-color: #00adb5;
}
div:nth-child(even){
  background-color: #6b4003;
}
div:nth-child(odd){
  background-color: red;
}
div:nth-child(2n+1){
  background-color: yellow;
}
```
### 3.15 Combinators
- 특정 컴포넌트 안의 컴포넌트를 조절하려고 할때 사용
```css
p span{
 color: #00c918;
}
div p span{
  color: tomato;
}
/* > : 직접적인 자식관계에만 적용, 손자관계 미적용 */
div > span{
  color: teal;
}
/* + : 바로 붙어있는 형제관계 적용 */
p + span{
  color: tan;
}
/* ~ : 형제관계 적용 */
p ~ span{
  color: tan;
}
```

### 3.16 Pseudo Selectors part Two
- 다양한 선택자들이 있고, 이를 적절히 사용할 수 있다.
- <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes" target="_blacnk">Pseudo Selectors 설명 사이트 이동</a>
- <a href="https://developer.mozilla.org/ko/docs/Web/CSS/Attribute_selectors" target="_blacnk">Attribute Selectors 설명 사이트 이동</a>
```css
input:required {
 border-color: #00c918;
}
/* placeholder가 unsersname인것 */
input[placeholder="username"] {
  color: tomato;
}
/* placeholder에 name이 포함인 것*/
input[placeholder~="name"] {
  color: tomato;
}
/* > : 직접적인 자식관계에만 적용, 손자관계 미적용 */
div > span{
  color: teal;
}
/* + : 바로 붙어있는 형제관계 적용 */
p + span{
  color: tan;
}
/* ~ : 형제관계 적용 */
p ~ span{
  color: tan;
}
```

### 3.17 States
- 상태에 대한 스타일을 변화시킬 수 있다.
```css
/* 버튼 눌렀을때 상태 */
button:active {
 border-color: #00c918;
}
/* 버튼에 포인트가 갔을때 상태 */
button:hover {
  border-color: #00c918;
}
/* 버튼에 키보드의 focusing이 이루어졌을때 상태 */
button:focus {
  border-color: #00c918;
}
/* 링크를 방문했을때 상태 */
a:visited {
  border-color: #00c918;
}
/* form 아래 focus가능한 컴포넌트가 focus 됐을때 상태변화*/
form{
  border: 1px solid salmon;
  display: flex;
  flex-direction: column;
  padding:20px;
}
form:focus-within{
  background-color: darkblue;
}
/* form이 덮어지면 input에 적용 */
form:hover input{
  background-color: darkblue;
}

div > span{
  color: teal;
}
/* + : 바로 붙어있는 형제관계 적용 */
p + span{
  color: tan;
}
/* ~ : 형제관계 적용 */
p ~ span{
  color: tan;
}
```

### 3.18 Recap
- 복습 및 추가 Pseudo selector
```css
/* placeholder style change */
input::placeholder {
 border-color: #00c918;
}
/* 문장을 드래그했을때 선택박스 style change */
p::selection {
  border-color: #00c918;
}
/* 첫번째 글자 style change */
p::first-letter {
  color: #00c918;
}
```

### 3.19 Colors and Variables
- 사람들이 이름을 지어놓은 컬러 종류가 있다.
- color에는 3가지 종류가 있다.
  - name
  - color code
  - rgb

```css
/* root에 style을 변수 선언 --변수명(띄어쓰기있다면-로 변환) */
:root{
  --main-color:#fcc200;
}
/* 변수를 사용할때는 var(--변수명) */
p {
  background-color: var(--main-color);  
}
a {
  color: var(--main-color);
}
```

## 4 ADVANCED CSS

### 4.0 Transitions
- CSS가 심화되어 동적인 부분을 할 수 있게 되었다.
- 어떤 상태에서 다른 상태로의 "변화"를 애니메이션으로 만드는 방법
- transition이라는 속성은 state가 없는 element에 붙어야 함 ex)hover가 없는 속성
- transition: 무엇을 얼마나 특성, 무엇을 얼마나 특성
- transition: all 모든 것을 변화
```css
a {
  color:wheat;
  background-color: tomato;
  text-decoration: none;
  padding: 3px 5px;
  border-radius: 5px;
  font-size: 55px;
  transition: background-color 10s ease-in-out;
}

a:hover {
  color: tomato;
  background-color: wheat;
}
```

### 4.1 Transitions part Two
- ease-in-out : 기본적으로 브라우저에게 어떻게 변할지 알려주는 속성
- <a href="https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes" target="_blacnk" >Pseudo Selectors 설명 사이트 이동</a>
- cubic-bezier는 아주 강력해서 나만의 커브를 만들수 있게 함

### 4.2 Transformations
- element를 변화시킴
```css
img {
  border:10px solid black;
  border-radius: 50%;
  transform: rotateY(85deg);  
}
```
- rotateY, rotateX, rotateZ : 축을 기준으로 기울임
- scale(2,2) : 배율
- translateX : 축을 기준으로 이동
- skew(50deg) : 기울이기
- 다른 element에 영향을 주지 않음. 다른 요소의 box를 변화시키지 않고 이동시킬 때 사용 
- CSS에 있는 모든 애니메이션은 GPU에 의해 돌아감