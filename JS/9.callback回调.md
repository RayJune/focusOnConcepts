JS是一门异步执行的语言。异步和回调就像一块硬币的两面，谁也离不开谁。有了异步执行通常都会使用回调。

回调函数代码比较短时，可以这样写（给回调函数添加函数名可以方便以后维护）：

```js
document.addEventListener('click', 	  function documentClickHandler() { 
	// 
});
```

回调函数代码比较长时可以这样写：

```js
document.addEventListener('click', documentClickHandler);

documentCLickHandler() {
	//
}
```

// 使用module

```js
var handlerModule =  (function (){ 
	return {
		handler1: function () {}, 		  
		handler2: function() {}} 
	;}())
	
document.addEventListener('click', handlerModule.handler1)
```

