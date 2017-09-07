```js
function foo () {
	var v1 = 1;
	var v2 = 2;
	
	return function () {
		console.log(v1);
	}
}

var bar = foo();
console.dir(bar);
```

打印出来一个匿名函数

```js
ƒ anonymous()
arguments: null
caller: null
length: 0
name: ""
prototype: {constructor: ƒ}__proto__: ƒ ()[[FunctionLocation]]: 
[[Scopes]]: Scopes[2]
0 Closure (foo)
v1: 1
Global {type: "global", object: Window, name: ""}
```

这里Closure Scope中保存了v1，因为原函数中返回的函数中只调用了v1，所以保存了v1。（大概可以这样理解）


类似的还有事件绑定中的情况：

```js
function foo() {
	var v1 = 1;
	var v2 = 2;
	
	document.addEventListener(document, function () {
		v1++;
		console.log(v1);
	});
}

var bar = foo();
console.dir(bar); //结果发现bar什么也没有，因为这是绑定在事件监听上的
```

要用getEventListeners来获取

```js
getEventListeners(document);
```

然后就会发现和上面的例子一样，也有一个属于CLosure的Scope，里面同样只有被colosure调用的v1。