// first-class function 

即function可以和number等数据类型一样，可以被当做参数传递给其他变量。

```js
document.addEventListener('click', function() {});
```

// higher-order function

即可以返回函数的函数。

```js
function foo() {
	var var1 = 1; 
	var var2 = 2; 
	return function () {
		console.log(var1 + var2);
	};
}
```