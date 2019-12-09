# es-babel
<style>
pre {
display: inline-block;
vertical-align: top;
width: 49%;
}
</style>

## let
- 只在块级作用域内有效
- 没有变量提升
- 不允许重复声明
- 暂时性死区
### 块级作用域、没有变量提升
```js
let g1 = 'g1';
if(true) {
  var g2 = 'g2'
  let g3 = 'g3'
}
console.log(g1)
console.log(g2)
console.log(g3)
```
```js
var g1 = 'g1';
if (true) {
  var g2 = 'g2';
  var _g = 'g3';
}
console.log(g1);
console.log(g2);
console.log(g3);
```
有块级作用域的变量，babel编译之后会改变变量的符号，前面加下划线，没有变量提升。

## const
```js
const gc = 'gc'
gc = 2;




```

```js
function _readOnlyError(name) { 
    throw new Error("\"" + name + "\" is read-only"); 
}
var gc = 'gc';
gc = (_readOnlyError("gc"), 2);
console.log(gc === 'gc') //true
```

## 解构赋值
### 数组结构赋值
```js
let [x, y = 'b'] = ['a'];



```
```js
var _ref = ['a'],
    x = _ref[0],
    _ref$ = _ref[1],
    y = _ref$ === void 0 ? 'b' : _ref$;
```
### 对象结构赋值
```js
let x;
// 报错
{x} = {x: 1};
// 正确
({x} = {x: 1})

var {x: y = 3} = {x: 5};
```
```js


var _x = {
  x: 5
},
    _x$x = _x.x,
    y = _x$x === void 0 ? 3 : _x$x;
```
### 字符串结构赋值
```js
const [a, b, c, d, e] = 'hello';
```
```js
function _slicedToArray(arr, i) {
    return _arrayWithHoles(arr) || _iterableToArrayLimit(arr, i) || _nonIterableRest();
}

function _nonIterableRest() {
    throw new TypeError("Invalid attempt to destructure non-iterable instance");
}

function _iterableToArrayLimit(arr, i) {
    if (!(Symbol.iterator in Object(arr) || Object.prototype.toString.call(arr) === "[object Arguments]")) {
        return;
    }
    var _arr = [];
    var _n = true;
    var _d = false;
    var _e = undefined;
    try {
        for (var _i = arr[Symbol.iterator](), _s; !(_n = (_s = _i.next()).done); _n = true) {
            _arr.push(_s.value);
            if (i && _arr.length === i) break;
        }
    } catch (err) {
        _d = true;
        _e = err;
    } finally {
        try {
            if (!_n && _i["return"] != null) _i["return"]();
        } finally {
            if (_d) throw _e;
        }
    }
    return _arr;
}

function _arrayWithHoles(arr) {
    if (Array.isArray(arr)) return arr;
}
var _hello = 'hello',
    _hello2 = _slicedToArray(_hello, 5),
    a = _hello2[0],
    b = _hello2[1],
    c = _hello2[2],
    d = _hello2[3],
    e = _hello2[4];
```
### 数值布尔结构赋值
```js
let {toString: s} = 123;
```
```js
var _ = 123,
    s = _.toString;
```

## 字符串的扩展
```js
let x = 1;
let y = 2;
`${x} + ${y} = ${x + y}`
```
```js
var x = 1;
var y = 2;
"".concat(x, " + ").concat(y, " = ").concat(x + y);
```

## 函数
### 参数的默认值
```js
function log(x, y = 'World') {
  console.log(x, y);
}
```
```js
function log(x) {
  var y = arguments.length > 1 && arguments[1] !== undefined ? arguments[1] : 'World';
  console.log(x, y);
}
```

### rest 参数
```js
function push(array, ...items) {
  items.forEach(function(item) {
    array.push(item);
    console.log(item);
  });
}

var a = [];
push(a, 1, 2, 3)




```
```js
function push(array) {
  for (var _len = arguments.length, items = new Array(_len > 1 ? _len - 1 : 0), _key = 1; _key < _len; _key++) {
    items[_key - 1] = arguments[_key];
  }

  items.forEach(function (item) {
    array.push(item);
    console.log(item);
  });
}

var a = [];
push(a, 1, 2, 3);
```

### 箭头函数
```js
var f = v => v;



function foo() {
  setTimeout(() => {
    console.log('id:', this.id);
  }, 100);
}

```
```js
var f = function f(v) {
  return v;
};

function foo() {
  var _this = this;
  setTimeout(function () {
    console.log('id:', _this.id);
  }, 100);
}
```
- 函数体内的this对象，就是定义时所在的对象，而不是使用时所在的对象。以下三个变量在箭头函数之中也是不存在的，指向外层函数的对应变量：arguments、super、new.target。
- 不可以当作构造函数，也就是说，不可以使用new命令，否则会抛出一个错误。
- 不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替
- 不可以使用yield命令，因此箭头函数不能用作 Generator 函数

## 数组的扩展
### 扩展运算符（spread） 三个点
```js
function add(x, y) {
  return x + y;
}

const numbers = [4, 38];
add(...numbers) // 42

Math.max(...[14, 3, 77])

[...[2, 3], 1]
```
```js
function add(x, y) {
  return x + y;
}

var numbers = [4, 38];
add.apply(void 0, numbers); // 42

Math.max.apply(Math, [14, 3, 77]);

[2, 3].concat([1]);
```
## 对象
### 扩展
```js
const foo = 'bar';
const baz = {foo};

const o = {
  method() {
    return "Hello!";
  }
};
```
```js
var foo = 'bar';
var baz = {
  foo: foo
};
var o = {
  method: function method() {
    return "Hello!";
  }
};
```
### 字符串函数
```js
let obj = {
  ['h' + 'ello']() {
    return 'hi';
  }
};





```
```js
function _defineProperty(obj, key, value) {
    if (key in obj) {
        Object.defineProperty(obj, key, {
            value: value,
            enumerable: true,
            configurable: true,
            writable: true
        });
    } else {
        obj[key] = value;
    }
    return obj;
}

var obj = _defineProperty({}, 'h' + 'ello', function () {
  return 'hi';
});
```
## 
```js

```
```js

```

## 
```js

```
```js

```

## 
```js

```
```js

```

## 
```js

```
```js

```

## 
```js

```
```js

```