IndexedDB is a low-level API for client-side `storage of significant amounts of structured data`, including files/blobs. This API `uses indexes to enable high-performance searches` of this data. While Web Storage is useful for storing smaller amounts of data, it is less useful for storing `larger amounts of structured data`. IndexedDB provides a solution. 
IndexedDB 是一种低级API，用于客户端`存储大量结构化数据`(包括, 文件/ blobs)。该API使用索引来实现对该数据的`高性能搜索`。虽然 Web Storage 对于存储较少量的数据很有用，但对于存储更大量的`结构化数据`来说，这种方法不太有用。（IndexedDB提供了一个存储大量数据解决方案，并可以`离线使用`）。

而它是一个事务型数据库系统。（又称：noSQL）
And it's a transactional database system.

生命周期：

>永久保存，除非被清除

存储空间大小：

>一个单独的数据库没有大小限制，不过可能限制每个Indexeddb数据库的大小，例如firefox在用户界面上只会针对存储超过 50 MB 大小的 BLOB（二进制大对象）请求权限，总体基本没有大小限制

作用空间： 

>子域名之间相互独立

使用场景:

>离线应用或webapp可以考虑使用indexeddb中存取数据
>
>IndexedDB 在浏览器的隐私模式（Firefox 的 Private Browsing 模式和 Chrome 的 Incognito 模式）下是被完全禁止的。


* IndexedDB是面向对象的。indexedDB不是用二维表来表示集合的关系型数据库。这一点非常重要，将影响你设计和建立你的应用程序。
* indexedDB不使用结构化查询语言（SQL）。它通过索引(index)所产生的指针(cursor)来完成查询操作，从而使你可以迭代遍历到结果集合。


IndexedDB 鼓励使用的基本模式如下所示：

1. 打开数据库并且开始一个事务。
2. 创建一个 object store。
3. 构建一个请求来执行一些数据库操作，像增加或提取数据等。
4. 通过监听正确类型的 DOM 事件以等待操作完成。
5. 在操作结果上进行一些操作（可以在 request 对象中找到）

```js
if (!window.indexedDB) {
    window.alert("Your browser doesn't support a stable version of IndexedDB. Such and such feature will not be available.")
}

// 打开我们的数据库
var db,
    request = window.indexedDB.open("MyTestDatabase");

// 第二个参数是数据库的版本号，如果我们打开的数据库不是我们期望的最新版本的话，我们可以对 object store 进行创建或是删除


request.onerror = function(event) {
  // Do something with request.errorCode!
  alert("Database error: " + event.target.errorCode);
};
request.onsuccess = function(event) {
  // Do something with request.result!
  db = request.result;
};

// 创建和更新数据库版本号
// 在数据库第一次被打开时或者当指定的版本号高于当前被持久化的数据库的版本号时，这个 versionchange 事务将被创建。
// 版本号是一个 unsigned long long 数字，这意味着它可以是一个非常大的整数。这也意味着你不能使用浮点数，否则它会被转换成最接近的较小的整数并且事务可能不会启动


request.onupgradeneeded = function(event) { 
   // 更新对象存储空间和索引 .... 
};
```

再来一段更完整的代码

```js
// 我们的客户数据看起来像这样。
var customerData = [
  { ssn: "444-44-4444", name: "Bill", age: 35, email: "bill@company.com" },
  { ssn: "555-55-5555", name: "Donna", age: 32, email: "donna@home.org" }
];
var dbName = "the_name";

var request = indexedDB.open(dbName, 2);

request.onerror = function(event) {
  // 错误处理程序在这里。
};

// onupgradeneeded 是我们唯一可以修改数据库结构的地方。在这里面，我们可以创建和删除对象存储空间以及构建和删除索引。
request.onupgradeneeded = function(event) {
  var db = event.target.result;

  // 创建一个对象存储空间来持有有关我们客户的信息。
  // 我们将使用 "ssn" 作为我们的 key path 因为它保证是唯一的。
  var objectStore = db.createObjectStore("customers", { keyPath: "ssn" });

  // 创建一个索引来通过 name 搜索客户。
  // 可能会有重复的，因此我们不能使用 unique 索引。
  objectStore.createIndex("name", "name", { unique: false });

  // 创建一个索引来通过 email 搜索客户。
  // 我们希望确保不会有两个客户使用相同的 email 地址，因此我们使用一个 unique 索引。
  objectStore.createIndex("email", "email", { unique: true });

  // 在新创建的对象存储空间中保存值
  for (var i in customerData) {
    objectStore.add(customerData[i]);
  }
};

// 在你可以对新数据库做任何事情之前，你需要开始一个事务。事务来自于数据库对象

// 如果你刚刚创建了一个数据库，你可能想往里面写点东西。看起来会像下面这样:
var transaction = db.transaction(["customers"], "readwrite");
```