---
title: "['1', '2', '3'].map(parseInt) what & why ?"
date: 2019/7/13 12:46:25
updated: 2019/7/15 16:22:13
categories:
    - 前端
    - javascript
tags:
    - javascript
    - ES6
description: parseInt() 函数解析一个字符串参数，并返回一个指定基数的整数 (数学系统的基础)。
cover: https://s2.ax1x.com/2019/09/02/nPR2RJ.jpg
---

> 转自 [https://github.com/sisterAn/blog/issues/19](https://github.com/sisterAn/blog/issues/19) 侵删

### 一道题目引发的问题

```javascript
["10", "10", "10", "10", "10"].map(parseInt);
// [10, NaN, 2, 3, 4]
```

### parseInt

`parseInt()`  函数解析一个字符串参数，并返回一个指定基数的整数 (数学系统的基础)。

```javascript
const intValue = parseInt(string[, radix]);
```

`string`  要被解析的值。如果参数不是一个字符串，则将其转换为字符串(使用 ToString 抽象操作)。字符串开头的空白符将会被忽略。

`radix`  一个介于 2 和 36 之间的整数(数学系统的基础)，表示上述字符串的基数。默认为 10。
`返回值`  返回一个整数或 NaN

```javascript
parseInt(100); // 100
parseInt(100, 10); // 100
parseInt(100, 2); // 4 -> converts 100 in base 2 to base 10
```

**注意：**
在`radix`为 undefined，或者`radix`为 0 或者没有指定的情况下，JavaScript 作如下处理：

-   如果字符串 string 以"0x"或者"0X"开头, 则基数是 16 (16 进制).
-   如果字符串 string 以"0"开头, 基数是 8（八进制）或者 10（十进制），那么具体是哪个基数由实现环境决定。ECMAScript 5 规定使用 10，但是并不是所有的浏览器都遵循这个规定。因此，永远都要明确给出 radix 参数的值。
-   如果字符串 string 以其它任何值开头，则基数是 10 (十进制)。

更多详见[parseInt | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt)

### map

`map()`  方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。

```javascript
var new_array = arr.map(function callback(currentValue[,index[, array]]) {
 // Return element for new_array
 }[, thisArg])
```

可以看到`callback`回调函数需要三个参数, 我们通常只使用第一个参数 (其他两个参数是可选的)。
`currentValue`  是 callback 数组中正在处理的当前元素。
`index`可选, 是 callback 数组中正在处理的当前元素的索引。
`array`可选, 是 callback map 方法被调用的数组。
另外还有`thisArg`可选, 执行 callback 函数时使用的 this 值。

```javascript
const arr = [1, 2, 3];
arr.map(num => num + 1); // [2, 3, 4]
```

更多详见[Array.prototype.map() | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

### 回到真实的事例上

回到我们真实的事例上

```javascript
["1", "2", "3"].map(parseInt);
```

对于每个迭代`map`, `parseInt()`传递两个参数: **字符串和基数**。
所以实际执行的的代码是：

```javascript
["1", "2", "3"].map((item, index) => {
    return parseInt(item, index);
});
```

即返回的值分别为：

```javascript
parseInt("1", 0); // 1
parseInt("2", 1); // NaN
parseInt("3", 2); // NaN, 3 不是二进制
```

所以：

```javascript
["1", "2", "3"].map(parseInt);
// 1, NaN, NaN
```

由此，加里·伯恩哈德例子也就很好解释了，这里不再赘述

```javascript
["10", "10", "10", "10", "10"].map(parseInt);
// [10, NaN, 2, 3, 4]
```

### 如何在现实世界中做到这一点

如果您实际上想要循环访问字符串数组, 该怎么办？ `map()`然后把它换成数字？使用编号!

```javascript
["10", "10", "10", "10", "10"].map(Number);
// [10, 10, 10, 10, 10]
```

---
