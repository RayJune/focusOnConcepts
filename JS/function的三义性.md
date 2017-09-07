```js
function foo() {
	console.log('this is a function');
}

foo(); // this is a function
```

函数首先是一个函数。

其次，函数是一个`object`。

```js
foo.     // 后面会出来一系列方法
foo.name //函数名： foo

foo.author = 'rayjune'; //增加属性
foo.getAuthor = function () {
	return this.author;
}
```

最后，函数还可以当成constructor来用（即其他面向对象语言中的类）

```
new foo();
```