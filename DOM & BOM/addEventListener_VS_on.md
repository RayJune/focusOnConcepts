
The main distinction between using .onclick and .addEventListener('click',...) is primarily one of utility. 

* .addEventListener('click',...) will allow a single click to perform multiple functions (such as an interaction on the page and an AJAX request)  addEventListener（'click'，...）将允许单次单击执行多个功能（例如页面上的交互和AJAX请求）
* adding multiple .onclick methods to a single element will `only allow the last .onclick assigned to it to run`. 而将多个.onclick方法添加到单个元素将仅允许最后一个。分配给它的onclick来运行。

.addEventListener is preferable in every case I can think of, even if only one function is going to run when the element is clicked (in case, for example, you wanted to expand your program later on; you'd need only add another addEventListener to the element rather than delete the .onclick and then add the two or more addEventListener methods).
.addEventListener在每种情况下都是可以想到的，即使单击元素时只有一个函数运行（例如，以后想要扩展程序），您只需要添加另一个addEventListener到元素，而不是删除.onclick，然后添加两个或更多的addEventListener方法）。

Above all, addEventListener is the better one. ：）


