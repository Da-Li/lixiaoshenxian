---
layout: detail_tmp
title: JavaScript中的坑
intor: JavaScript中的坑-声明变量
categories: JavaScript
---

#JavaScript中的坑# 


--- 
>JavaScript 的历史原因决定JavaScript有许多问题，和让人容易忽略的地方。但都是重要的。

###1.  var 声明变量###

#### 声明提升(hoisting) ####
	
先看一段代码

	var v = 'hoisting';
	function test_hoisting(){
		console.log(v);
		var v = 'hoisted';
	}

结果是什么呢：`undefined`.
因为 `声明提升`的原因 以上代码 和下面的代码 同理。
	
	var v = 'hoisting';
	function test_hoisting(){
		var v;
		console.log(v);
		v = 'hoisted';
	}

function作用域里的变量 遮盖了上层作用域变量，声明又被提升 所以就会出现`undefined`

> `声明提升`:是JavaScript 所有声明默认的行为（包括`function`） 提升的范围就是当前作用域的顶部。
 JavaScript 只是提升声明，并不提升初始化。 

 再看下面的代码：

	
	
	
	var test_hoisting2 = 3;

	function test_hoisting2(){

	}
	console.log(typeof test_hoisting2);

结果是 `number`为什么？

之前说过`function` 也会提升。由于在 `JavaScript`中 `function`是一等公民，`function` 会先提升. 
**函数的声明 比 变量的声明 具有高的优先级。** 
所以 `function test_hoisting2` 优先提升，被 `var test_hoisting2`覆盖。

>关于变量提升的问题都大同小异，在实际开发中要避免这个特性，把变量定义在顶部。就会避免出现不必要的问题。  

在 Chrome 里有个奇怪的问题：
	console.log(typeof name);
	var name = "Chrome";
	console.log(typeof name); 

经过上面示例，我们期待的结果是 `undefined` `string`. 但是结果却都是 `string`.如果我们再试一次，将`name`换成 其他的 `name2` 就是我们预期的结果了.原因是 
**Chrome**
可能初始化 `name` 导致我们使用时，已经声明完成，所以就是`string`了 
