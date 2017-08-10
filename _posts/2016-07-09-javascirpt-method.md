---
layout: post
title: "자바스크립트 함수 몰랐던 것."
date: 2016-07-09 00:00:00
categories: dev
tags: js,javascript
---

## Javascript 

### 책을 보는중에 함수쓰는 방법을 하나더 알게됨

```
function getSize(width, height, depth){
	var area = width * height ;
	var volume =width *  height * depth;
	var sizes = [area,volume];
	return sizes; 
}

var areaOne = getSize( 1, 2, 3)[0];   //2
var volumeOne = getSize( 4, 5, 6)[1];   //120
```
이런식으로 호출하면 areaOne 은 sizes[0] 2의 값을 volumeOne 은 sizes[1]의 값인 120을 리턴 받아오는걸 알게됨

### 자주 쓸일은 없겠지만 알아두면 좋을것 같다
