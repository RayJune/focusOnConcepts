The same-origin policy restricts how a document or script loaded from one origin can interact with a resource from another origin. It is a critical security mechanism for `isolating potentially malicious documents`.
同源策略限制从一个源加载的文档或脚本如何与来自另一个源的资源进行交互。这是一个用于`隔离潜在恶意文件的关键的安全机制`。


### Definition of an origin

Two pages have the same origin if the protocol, port (if one is specified), and host are the same for both pages.如果协议，端口（如果指定了一个）和域名对于两个页面是相同的，则两个页面具有相同的源。

提交表单不受同源政策的限制。

如果非同源，共有三种行为受到限制。
*  Cookie、LocalStorage 和 IndexDB 无法读取。
* DOM 无法获得。
* AJAX 请求不能发送。