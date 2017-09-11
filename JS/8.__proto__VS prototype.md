**所有JS对象**都是`实例化`而来的。

\_\_proto\_\_在实例化时产生。

而所有的constructor（即强类型语言）中的`类`，都有prototype属性。

date.\_\_proto\_\_指向的是Date.prototype

date.\_\_proto\_\_ === Date.prototype //true


因为类也是对象，所以date对象也有__proto__方法，指向Date.prototype;但prototype只有类才有，所以对象们并不一定有prototype

区别：

* prototype只有类才有，\_\_proto\_\_所有对象都有。类既有prototype又有\_\_proto\_\_
* prototype可读可写，\_\_proto\_\_只读

