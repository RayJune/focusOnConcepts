JS的原型链通过\_\_proto\_\_属性来实现的

>RayJune注：\_\_proto\_\_是对象才有的属性

```js
var date = new Date(); // 随便创建一个对象
console.dir(date); // 发现只有__proto__属性

date.getDay(); // 调用方法成功
// 成功的原因在于date本身没有这个方法（即Date本身没这个方法，date从__proto__上找到object，找到了这个方法，所以调用成功）

date.doSomething(); //调用失败
// 失败的原因在于先在date内找doSomethino，失败；接着去date.__proto__proto找，失败；接着去date.__proto__proto__proto找，发现不存在了，null，所以报出错误
```

