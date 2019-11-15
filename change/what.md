# what
## console

### assert 断言

### count countReset

### clear


### error

### group

### trace

### 

### 

### 

### 

## Object

### Object.is()
它用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致。不同之处只有两个：一是+0不等于-0，二是NaN等于自身。
```js
+0 === -0 //true
NaN === NaN // false

Object.is(+0, -0) // false
Object.is(NaN, NaN) // true
```

