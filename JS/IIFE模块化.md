IIFE: immediately invoked function expression

function declaration VS function expression

只要对函数的语法进行一些运算或者操作，都会变成function expression（函数表达式）

最大的用处： 设计出`模块化`JS程序。

如

```js
var js = function () {
	console.log('this is a function expression');
}

// use operator
-function declaration() {
	console.log('add a operator and change it to function expresssion')
}

// use ()
(function braceExpression() {
	console.log('braces change it to function expression')
}());
```

```JS
var cart = (function () {
	var products = []; //外部访问不到这个数组
	return { // 对外开放三个接口
			// 可以控制向外界开放哪些接口
		addProduct: function(product) {
			products.push(product);
		},
		getProduct: function() {
			return products;
		},
		getTotal: function() {
			return products.reduce(function(total, product) 	{
				return total += parseInt(product.price);
				
			}, 0)
		}
	}
}());
```

PS: ES6中出现了module，是一种很好的替换方案。