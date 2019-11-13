# es-babel
<style>
pre {
display: inline-block;
vertical-align: top;
width: 45%;
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