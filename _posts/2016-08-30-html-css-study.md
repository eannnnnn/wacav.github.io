---
layout: post
title: "Layout"
date: 2016-08-30 00:00:00
categories: html
tags: HTML css layout style
---

## display
>`display`는 CSS 에서 레이아웃을 제어하기 위한 가장 중요한 프로퍼티  
엘리먼트에는 엘리먼트의 유형에 따라 기본 표시값이 존재  
대부분의 엘리먼트에 대한 기본값은 `block` 이나 `inline`

## block

> `div`는 표준 블록 레벨 엘리먼트이다. 블록 레벨 엘리먼트는 `새줄에서 시작해 좌우로 최대한 늘어난다.`   
자주 볼수 있는 다른 블록 레벨 엘리먼트로 `p`와`form`이 있으며,  
HTML5 에서 새로 추가된 엘리먼트로 `header`와`footer`,`section` 등이 있다.

## inline

>`span` 은 표준 인라인 엘리먼트  
`인라인 엘리먼트(inline element)`는 단락 안에서 해당 단락의 흐름을 방해하지 않은 채로 텍스트를 감쌀 수 있다.  
링크에 사용하는 `a` 엘리먼트는 가장 흔히 볼 수 있는 inline element

## none

>`script` 와 같은 일부 특별한 엘림너트에서는 `none`을 기본값으로 사용한다.  
이 값은 자바스크립트에서 엘리먼트를 실제로 삭제하고 재생성하지 않고도 엘리먼트를 보이고 감추는 데 흔히 사용된다.

>`visibility`와 다름 `visibility : hidden` 을 설정하면 보이진 않지만 공간을 차지한다.

다른 속성은 [여기](https://developer.mozilla.org/ko/docs/Web/CSS/display) 를 참고하자.

- 블록 레벨 엘리먼트의 `width`를 설정하면 컨테이너의 좌우 가장자리로 늘어나지 않게 할 수 있다.
- 그런 다음 좌우 마진을 `margin : 0 auto` 로 설정해 해당 엘리먼트를 컨테이너 안에서 가로 중앙에 오게 할 수 있다.
- 엘리먼트는 지정한 너비를 차지하고, 나머지 공간은 무잔에 균등하게 나눠질 것이다.
- 이 경우 브라우저 창이 작을경우 가로 스크롤바가 생긴다.

#### 이럴경우
- 이러한 상황에서 `width ` 대신 `max-width` 를 사용하면 브라우저가 작은 창을 처리하는 방식을 개선할 수 있다.

```CSS
.simple {
    width: 500px;
    margin : 20px auto;
}
.fancy {
    width: 500px;
    margin : 20px auto;
    padding: 50px;
    border-width: 10px;
}
```

위 코드를 사용하면 `simple` 이적용된 블록과 `fancy` 가 적용된 블록의 크기가 다르다.
이건 엘리먼트의 테두리와 패딩이 지정된 너비 이상으로 엘리먼트를 늘리기 때문.

- 위 같은 문제를 해결하기 위해 `box-sizing` 이라는 새로운 CSS 프로퍼티가 생김
- `box-sizing`을 지정하면 해당 엘리먼트의 패딩과 테두리가 더는 블록의 너비를 늘리지 않는다.
- 모든 엘리먼트가 항상 이렇게 동작하도록

```CSS
* {
  -webkit-box-sizing: border-box;
     -moz-box-sizing: border-box;
          box-sizing: border-box;
}
```
- 위 처럼 선언 해도 괜찮은 방법이다.
>`box-sizing`은 다소 근래에 생긴 프로퍼티라서 지금 당장은 예제에서 한 것처럼  
`-webkit-`이나` -moz- `접두사를 붙여야 합니다. 이 기법은 특정 브라우저에서 실험적인 기능들을 활성화하는 데 사용됩니다.   
이 기법은 IE8+에서만 사용할 수 있다는 점도 염두에 두세요.  

## 좀 더 복잡한 레이아웃
> `position` 에 대해 알아보자

- `position` 프로퍼티에는 다양한 값을 설정할 수 있으며,
- 각 값의 이름은 제대로 지어지지 않아서 기억하기가 불가능하다.
- `position : static` 은 기본값.`position : static`이 설정된 엘리먼트는 특별한 방식으로 위치가 지정된게 아니다.
- 정직(static) 엘리먼트는 *위치가 지정된 것이 아니라고* 표현하며,
- `static`이 아닌 다른 값으로 지정된 엘리먼트에 대해 *위치가 지정됐다* 고 표현한다.

```CSS
.relative1 {
  position: relative;
}
.relative2 {
  position: relative;
  top: -20px;
  left: 20px;
  background-color: white;
  width: 500px;
}
```
- `relative` 는 별도의 프로퍼티를 지정하지 않는 이상 static 과 동일하게 동작
- 상대위치가 지정된 엘리먼트에 `top`나 `right`,`left`,`bottom` 을 지정하면 기본 위치와 다르게 위치가 조정된다.
- 다른 콘텐츠는 해당 엘리먼트에서 남긴 공백에 맞춰 들어가게끔 조정되지 않음

### fixed

- 고정(fixed)는 Viewport 에 상대적으로 위치가 지정된다.
- 페이지가 스크롤 되더라도 늘 같은 곳에 위치한다.
- `relativew`와 마찬가지로 `top`이나 `right`,`left`,`bottom` 프로퍼티가 사용된다.
- 모바일 브라우저의 경우 고정 엘리먼트 지원이 불안정하다. [이와 관련된 사항은 이곳에서](http://bradfrostweb.com/blog/mobile/fixed-position/)

## absolute

- `absolute`는 가장 다루기 까다로운 위치 지정 값
- `absolute`는 뷰포트에 상대적으로 위치가 지정되는게 아니라 *가장 가까운 곳에 위치한 조상 엘리먼트* 에 상대적으로 위치가 지정
- `fixed`와 비슷하게 동작
- 절대 위치가 지정된 엘리먼트가 기준으로 삼는 조상 엘리먼트가 없으면 `body`를 기준으로 삼고 페이지 스크롤에 따라 움직임
- *위치가 지정된* 엘리먼트는 `position`이 `static`으로 지정되지 않은 엘리먼트를 가리킨다.

## 예제
```HTML
<html>
<head>
  <style>
    .container {
      position: relative;
      background-color: black;
    }
    nav {
      position: absolute;
      left: 0px;
      width: 200px;
      background-color: yellow;
    }
    section {
      /* position is static by default */
      margin-left: 200px;
      background-color: #6bacce;
    }
    footer {
      position: fixed;
      bottom: 0;
      left: 0;
      height: 70px;
      background-color: white;
      width: 100%;
      background-color: green;
    }
    body {
      margin-bottom: 120px;
    }
  </style>
</head>
<body>
  <div class="container">
    <nav>
      목록
    </nav>
    <section>
      section에 지정한 margin-left 스타일은 nav가 들어갈 공간을 만들어줌.
    </section>
  </div>
  <footer>
    고정 헤더나 푸터를 사용한다면 그것들이 들어갈 공간을 마련해 줘야 한다.
  </footer>
</body>
</html>
```

해당 코드가 적용된건 [여기서](http://codepen.io/ParkChong/pen/qaWbgk) 확인 할 수 있다.


## float

- 레이아웃을 잡는데 사용하는 또 하나의 CSS 프로퍼는 `float`이다.
- `clear` 프로퍼티는 `float`의 동작 방식을 제어하는 데 중요하다.
- `float`은 번역하면 띄우다 라는 뜻이고 정렬하기 위해 사용하는 속성
- 문서에 사진과 그림이 있을때 그림을 왼쪽이나 오른쪽으로 띄워 정렬하거나
- 각 엘리먼트를 오른쪽이나 왼쪽으로 정렬하여 사용할 수 있음.
- 하지만 `float` 을 사용하지 않은 엘리먼트와 겹쳐 보이거나 가려질수 있으므로
- `clear`가 필요하다.
- `float : left` 를 했다면 `clear : left`로 왼쪽에 떠있는 엘리먼트를 비우자 오른쪽이나 양쪽도 가능
- 만약 사진을 `float` 으로 띄웠다면 `div`의 컨테이너 바깥으로 넘어갈 수도 있다.
- 이런 경우에는 `overlow : auto` 를 해주면 띄운 크기만큼 `div` 컨테이너를 늘려준다
- ie 6 같은 경우 ~~지원하고싶지않지만~~ `overflow : auto ; zoom : 1; ` 을 넣어주자. ~~그냥 최신버전을 사용하라고 하자~~

## 퍼센트 너비

- 퍼센트는 특정 엘리먼트를 담고 있는 블록에 상대적인 측정 단위이다.
- 퍼센트는 이미지에 쓰기에 아주 좋다.
- `width : 50%` 를 하면 항상 컨테이너 너비의 50% 만 차지하는 이미지를 만들 수 있다.


## 반응형 디자인

> @media

```CSS
@media screen and (min-width:600px) {
  nav {
    float: left;
    width: 25%;
  }
  section {
    margin-left: 25%;
  }
}
@media screen and (max-width:599px) {
  nav li {
    display: inline;
  }
}
```

- @media 쿼리를 이용하자
- screen 의 크기에 따라 레이아웃 구성을 다르게 하는 방법을 구현할 수 있다.

# 예제

```HTML
<html>
  <head>
    <style>
      body{
        margin-bottom : 150px;
      }
      footer {
        position : fixed;
        bottom : 0;
        left : 0;
        height : 100px;
        background-color : yellow;
        width : 100%;
      }

      @media screen and (min-width:600px){
      nav {
        float : left ;
        width : 25%;
        background-color : yellow;
      }
      section {
        margin-left : 25%;
        background-color : aquamarine;
      }
      }
      @media screen and (max-width:599px){
      nav {
        background-color : yellow;
      }
      nav li{
        display : inline;
      }
      section {
        background-color : aquamarine;
      }
      }
    </style>
  </head>
  <body>
    <div class="container">
      <nav>
        <ul>
          <li>apple</li>
          <li>banana</li>
          <li>kiwi</li>
        </ul>
      </nav>
      <section> 브라우저 크기를 바꿔보세요!</section>
      <section>메뉴가 어디론가 이동될 거에요!</section>
      <section>가나다라...</section>
    </div>
    <footer><p>이곳은 footer 입니다.</p></footer>
  </body>
</html>
```


해당 결과는 [여기서확인](http://codepen.io/ParkChong/pen/GjKkJQ) 하길 바란다.


## inline-block

- 브라우저 너비를 채우고 알맞게 줄바꿈되는 박스 그리드를 만들 수 있다
- `inline-block` 을 사용하면 만들기가 쉽다.
- `inline-block` 은 `inline`이랑 비슷하지만 너비와 높이를 지정할 수 있다.

> 아래 두개의 코드는 힘든방법과 덜힘든? 방법이다. 결과는 같다.

```CSS
.box {
  float: left;
  width: 200px;
  height: 100px;
  margin: 1em;
}
.after-box {
  clear: left;
}
```

```CSS
.box2 {
  display: inline-block;
  width: 200px;
  height: 100px;
  margin: 1em;
}
```

- `inline-block` 엘리먼트는 `vertical-align` 프로퍼티의 영향을 받는다.
- 각 컬럼의 너비를 설정할 필요가 있다.
- HTML의 각 컬럼 사이에 공백이 있으면 컬럼 간에 틈이 생긴다.


## flexbox

- `flexbox` 레이아웃 모드는 최근에 상당히 많이 바뀌었기 때문에 각 브라우저 마다 다른식으로 구현됨.

```CSS
.container {
  display: -webkit-flex;
  display: flex;
}
nav {
  width: 200px;
}
.flex-column {
  -webkit-flex: 1;
          flex: 1;
}
```
를 사용하면 앞선 예제처럼 만들 수 있다.

```CSS
.container {
  display: -webkit-flex;
  display: flex;
}
.initial {
  -webkit-flex: initial;
          flex: initial;
  width: 200px;
  min-width: 100px;
}
.none {
  -webkit-flex: none;
          flex: none;
  width: 200px;
}
.flex1 {
  -webkit-flex: 1;
          flex: 1;
}
.flex2 {
  -webkit-flex: 2;
          flex: 2;
}
```

- `.container`는 `flexbox` 선언
- `.initial`이 적용된 컨테이너는 200px까지 늘어나며 여유공간이 없으면 100px 까지 줄어듬
- `.none` 은 항상 200px 를 유지
- `.flex1` 나머지 너비의 1/3 을 채운다.
- `.flex2` 나머지 너비의 2/3 을 채운다.


```CSS
.vertical-container {
  height: 300px;
  display: -webkit-flex;
  display:         flex;
  -webkit-align-items: center;
          align-items: center;
  -webkit-justify-content: center;
          justify-content: center;
}
```

하면 CSS에서도 수직 중앙에 쉽게둘 수 있다.



공부한곳 : [http://ko.learnlayout.com/frameworks.html](http://ko.learnlayout.com/frameworks.html)
