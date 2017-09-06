### Types

Primitives: When you access a primitive type you `work directly on its value`. (string, number, boolean, null, undefined)

Complex: When you access a complex type you work `on a reference` to its value. (object, function, array)


### Properties

Use dot( . ) notation when accessing properties.

```js
var luke = {
  jedi: true,
  age: 28
};

// bad
var isJedi = luke['jedi'];

// good
var isJedi = luke.jedi;
```

Use subscript notation [] when accessing properties with a variable.

```js
var luke = {
  jedi: true,
  age: 28
};

function getProp(prop) {
  return luke[prop];
}

var isJedi = getProp('jedi');
```

### Blocks

If you're using multi-line blocks with if and else, put else on the same line as your if block's closing brace.

```js
// bad
if (test) {
  thing1();
  thing2();
}
else {
  thing3();
}

// good
if (test) {
  thing1();
  thing2();
} else {
  thing3();
}
```

### Comments

Prefixing your comments with FIXME or TODO helps other developers quickly understand if you're pointing out a problem that needs to be revisited, or if you're suggesting a solution to the problem that needs to be implemented. These are different than regular comments because they are actionable. The actions are FIXME -- need to figure this out or TODO -- need to implement.

Use `// FIXME`: to annotate problems.

```js
function Calculator() {

  // FIXME: shouldn't use a global here
  total = 0;

  return this;
}
```

Use `// TODO`: to annotate solutions to problems.

```js
function Calculator() {

  // TODO: total should be configurable by an options param
  this.total = 0;

  return this;
}
```

### Naming Conventions

#### Don't save references to this. Use Function#bind.

```js
// bad
function () {
  var self = this;
  return function () {
    console.log(self);
  };
}

// bad
function () {
  var that = this;
  return function () {
    console.log(that);
  };
}

// bad
function () {
  var _this = this;
  return function () {
    console.log(_this);
  };
}

// good
function () {
  return function () {
    console.log(this);
  }.bind(this);
}
```

#### Name your functions. This is helpful for stack traces.

```js
// bad
var log = function (msg) {
  console.log(msg);
};

// good
var log = function log(msg) {
  console.log(msg);
};
```

### Modules

### jQuery

Prefix jQuery object variables with a $.

```js
// bad
var sidebar = $('.sidebar');

// good   
var $sidebar = $('.sidebar');
```


For DOM queries use Cascading $('.sidebar ul') or parent > child $('.sidebar > ul')

Use find with scoped jQuery object queries.

```js
// bad
$('ul', '.sidebar').hide();

// bad
$('.sidebar').find('ul').hide();

// good
$('.sidebar ul').hide();

// good
$('.sidebar > ul').hide();

// good
$sidebar.find('ul').hide();
```