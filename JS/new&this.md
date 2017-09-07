当使用new + 函数时，this发生了什么

```js
function foo() {
	console.log(this);
}

new foo();  // foo {}
```

当对函数调用 new 时，发生的内部情况是这样的：

```js
temp = {};
binded = foo.bind(temp);
binded();
```

正常使用：

```js
function Foo(name) {
	this.name = 'rayjune';
}	

console.dir(new Foo());
```
