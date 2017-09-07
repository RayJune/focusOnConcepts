this是一个参数，是JS内部函数被调用时的上下文来隐式绑定的。

这里直接指向window，因为foo是定义在window之上的

```js
function foo() {console.log(this);}

foo() === window.foo();
```

可以用bind来绑定。（显示制定）

```js
var a = foo.bind(document);

a(); // #document
```


