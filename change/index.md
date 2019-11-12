# es-babel
## let

<style>
pre {
display: inline-block;
width: 45%;
}
</style>

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
"use strict";

var g1 = 'g1';

if (true) {
  var g2 = 'g2';
  var _g = 'g3';
}

console.log(g1);
console.log(g2);
console.log(g3);
```
有块级作用域的变量，babel编译之后会改变变量的符号，前面加下划线。

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