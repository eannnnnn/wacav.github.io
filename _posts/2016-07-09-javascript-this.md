---
layout : post
title : "javascript this 키워드"
date : 2016-07-09 00:00:00
categories : javascript
tags: js,javascript,this
---

## this
- this 키워드는 함수와 객체 내부에서 주로 사용한다. 또한, 함수가 선언된 위치에 따라 this 키워드의 의미가 달라짐
이 키워드는 항상 단 하나의 객체를 참조하며, 주로 특정 시점에 함수를 실행하고 있는 객체를 가리킨다.


### 전역 볌위 내의 함수
- 스크립트의 최상위 수준에 함수를 선언하면, 이 함수는 global scope 혹은 global context에 포함된다.
- 이 컨텍스트에 속한 기본 객체는 window 객체이므로 전역 컨텍스트 내에 선언된 함수 내에서 tis 키워드를 사용하면 이 키워드는 window 객체를 가리키게 된다.  
- 아래 예제에서 this 키워드는 window 객체의 속성을 리턴하기 위한 목적으로 사용되었다.


```
function windowSize(){
	var width = this.innerWidth;
	var height = this.innerHeigth;
	return [width , height];
}
```


- 내부적으로 this 키워드는 현재 실행 중인 함수가 선언된 객체를 참조한다.


### 전역 변수
- 모든 전역 변수는 window 객체의 속성이 되므로 전역 컨텍스트에 선언된 함수 내에서는 this 키워드를 통해 전역 변수뿐만 아니라 window객체의 다른 속성들도 사용할 수 있따.
- 아래 예제에서 showWidth() 함수는 전역 범위에 선언되어 있으므로 this.width 변수는 width 변수를 가리키게 된다.


```
var width = 600;
var shape = { width : 300} ;

var showWidth = function(){
	document.write(this.width);
};

showWidth();
```


- 이 함수는 (write 메서드를 이용하여 페이지에 600이라는 값을 출력해준다.)
- 지금까지 살펴봤듯이 this 키워드가 가리키는 값은 상황에 따라 달라진다. 하지만 앞서 두개의 예제를 보고 이해하지 못한다 해서 염려할 필요는 없다. 앞으로 더 많이 보게된다.


### 객체의 메서드
- 함수가 객체의 내부에 선언되면 이 함수는 메서드가 된다.
- 메서드 내에서 `this` 키워드는 메서드를 가지고 있는 객체를 가리킨다.
- 아래예제에서 `getArea()` 메서드는 shape 객체 내부에 선언되어 있으므로 이 함수 내에서 사용하는 this 키워드는 함수가 선언된 `shape` 객체를 가리키게 된다.


```
var shape = {
	width : 600
	, height : 400
	, getArea : function(){
		return this.width * this.height;
	}
}
```


- 이 예제의 `this` 키워드는 `shape` 객체를 가리키고 있으므로, 함수 내의 구문은 다음의 코드와 동일하다고 생각 할 수 있다. `return shape.width * shape.height`
- 만일 객체 생성자를 이용하여 여러개의 객체를 생성했다면 (**그리고 각 개체가 모두 다른 값을 가지고 있다면**)
`this` 키워드는 각각의 새로운 객체를 참조한다. `getArea()` 함수를 호출하면 해당 함수가 호출된 바로 그 객체를 가리킨다.


### 메서드로서의 함수 표현식
- 만일 명명된 함수를 전역 범위에 선언한 후 이 함수를 어떤 객체의 메서드로 사용하면, 함수 내의 `this`키워드는 해당 함수를 가지고 있는 객체를 가리킨다.
- 다음 예제는 앞서 살펴본 예제와 동일한 구문을 사용하는 `showWidth()` 함수를 사용하지만, 이번에는 객체의 메서드로 대입하는 방식을 사용하였다.


```
var width = 600
	, height = {width : 300} ;

var showWidth = function(){
	document.write(this.width);  //300
}

shape.getWidth = showWidth ;
shape.getWidth();
```


- 예제의 밑에서 두 번째 줄의 코드는 `showWidth()` 함수가  shape객체의 메서드로 사용될 것이며, 그 이름은 getWidth() 함수가 될 것임을 표현한 것이다.
- getWidth() 함수가 호출됨에도 불구하고 이때의 this 키워드는 전역 컨텍스트가 아닌 `shape` 객체를 가리키게 된다.
