---
title: 数组map的方法实现
date: 2018-08-24 11:25:22
tags: Array,map
categories: js
---



   在项目中，经常会使用到数组的map,filter,reduce等方法，在享受这几个方法的便利的同时，也要去弄清楚这几个方法究底是怎么实现的，这样才能更充分的来利用它们。这一篇主要是map的实现方法：
   
   
   首先针对数组的方法，可以直接类似arr.slice()这种调用的，我们需要将这类方法写在数组的原型对象里，这样就可以直接使用实例化之后的数组来调用。那么我们给我们新创建的方法命一个名，就为consMap。先回顾一下map的用法，arr.map(function(item,i,arr),this),最后返回的是另外一个处理之后的新的数组。

----------

**代码**

```javascript
//fn为处理每一项数组的函数，context代表作用域
Array.prototype.consMap = function(fn,context){

	if(!(fn instanceof Function)){
		throw new TypeError('第一个参数需为函数')
	}
	var arr = this;   //this指代实例化的数组
	var newArr = [];
	for(var i = 0;i< arr.length;i++){
		var newValue = fn.call(context,arr[i],i,arr);
		newArr.push(newValue);
	}
	return newArr;
}
```

**验证**

```javascript
	var arr = [1,2,3]
	var newArr = arr.consMap(function(item,i,arr){
		return item + 1;
	})
	console.log(newArr);
```

**结果**

```javascript
	[2,3,4]
```

以上就是实现数组map的方法