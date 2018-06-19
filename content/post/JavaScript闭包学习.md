---
title: "JavaScript闭包学习"
date: 2018-06-13T20:07:25+08:00
draft: true
---

<!--more-->
#### 变量作用域

```js
	function fun1(){
		var foo = "jack";
	}
	//引用报错 ReferenceError: foo is not defined
	console.log(foo);
```
局部变量，当定义该变量的函数调用结束时，该变量就会被垃圾回收机制回收而销毁。

#### 闭包定义
1. 定义在函数内部的函数
2. 使用其他函数定义的变量，并使这个变量不被销毁  
`我们来看一个简单的闭包`

	``` js
		function fun1(){
			var foo = "foo";
			function fun2(){
				alert(name);
			}
			return fun2;
		}
		
		var f = fun1();
		f();// foo
	```

*上面的fun2就是一个简单的闭包，我们来看看它的有哪些特征*
`fun2定义在函数fun1里面，并且引用了fun1中定义的name变量`
`通过return 将闭包返回到函数fun1外部，这样我们就可以在函数外部使用函数内部定义的变量了`
**可以说闭包是连接函数内部和函数外部的桥梁**

#### 闭包可以用来做什么
- 单例模式

	```js
	let Singleton = (function(){
		let instance;
	    function createInstance(){
			return new Object("I am the instance");
		}
		return {
			getInstance: function(){
				if(!instance){
					instance = createInstance();
				}
				return instance;
			}
		};
	})();
	
	let s1 = Singleton.getInstance();
	let s2 = Singleton.getInstance();
	console.log(s1 === s2);
	```
- 模块化开发

 ```js
 
	 function coolModule(){
	    let something = 'cool';
	    let arr = ["Google","Apple","Microsoft"];
	
	    function doSomething(){
	        console.log(something);
	    }
	
	    function doAnother(){
	        console.log(arr.join("-"));
	    }
	
	    return {
	        doSomething,
	        doAnother
	    }
	}
	
	let cool = coolModule();
	cool.doSomething();
	cool.doAnother();
 ```

#### 使用闭包应该注意的地方
1. 不要再闭包中引用循环变量


