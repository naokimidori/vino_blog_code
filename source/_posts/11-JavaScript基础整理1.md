---
title: "JavaScript基础整理1"
date: 2019/11/20 19:21:09
categories:
    - JavaScript
tags:
    - JavaScript
description: js基础面试题整理
cover: https://s1.ax1x.com/2020/03/29/GETWQ0.png
---
### 类型转换

- 强制类型转换

```javascript
var a = '24';
var b = Number(a); ---强制转换
```

同理：

> Boolean(value)：把参数值转换为布尔型值
> Number(value)：把参数值转换为数字
> parseFloat/parseInt：把参数值转换为浮点数/整数
> String(value)：把参数值转换为字符串
> toString(value)：把参数值转换为字符串

- 隐式(自动)转换

```javascript
var a = '24';
var b = a * 1;
a -- '24';
b -- 24;
```

自动转换表

| 值（value）              | 字符串操作环境            | 数字运算环境                   | 逻辑运算环境 | 对象操作环境 |
| :----------------------- | ------------------------- | ------------------------------ | ------------ | ------------ |
| undefined                | "undefined"               | NaN                            | false        | Error        |
| null                     | "null"                    | 0                              | false        | Error        |
| 非空字符串               | 不转换                    | 字符串对应的数字值NaN          | true         | String       |
| 空字符串                 | 不转换                    | 0                              | false        | String       |
| 0                        | "0"                       | 不转换                         | false        | Number       |
| NaN                      | "NaN"                     | 不转换                         | false        | Number       |
| Infinity                 | "Infinity"                | 不转换                         | true         | Number       |
| Number.POSITIVE_INFINITY | "Infinity"                | 不转换                         | true         | Number       |
| Number.NEGATIVE_INFINITY | "-Infinity"               | 不转换                         | true         | Number       |
| -Infinity                | "-Infinity"               | 不转换                         | true         | Number       |
| Number.MAX_VALUE         | "1.7976931348623157e+308" | 不转换                         | true         | Number       |
| Number.MIN_VALUE         | "5e-324"                  | 不转换                         | true         | Number       |
| 其他所有数字             | "数字的字符串值"          | 不转换                         | true         | Number       |
| true                     | "true"                    | 1                              | 不转换       | Boolean      |
| false                    | "false"                   | 0                              | 不转换       | Boolean      |
| 对象                     | toString()                | valueOf() 或 toString() 或 NaN | true         | 不转换       |



### JavaScript的作用域(scope)及作用域链指什么？

简单来说，作用域就是变量与函数的可访问范围，即作用域控制着变量与函数的可见性和生命周期。

js的作用域是靠函数来形成的，也就是说一个函数的变量在函数外不可以访问。

- 全局作用域

  - 函数外定义的变量拥有全局作用域

  ```javascript
  var n = 8;
  function fn() {
    var a = 24;
    return a;
  }
  
  console.log(fn());  // 24
  console.log(n);  // 8
  console.log(a);  // ncaught ReferenceError: a is not defined
  ```

  - 未定义直接赋值的变量自动提升为全局作用域

  ```javascript
  var n = 8;
  function fn() {
    a = 24;
    return a;
  }
  
  console.log(fn());  // 24
  console.log(n);  // 8
  console.log(a);  // 24 提升
  ```

  - window对象的属性拥有全局作用域

- 局部作用域

  局部作用域一般只在固定的代码片段内可访问到，最常见的例如函数内部，所以在一些地方会把这种作用域成为函数作用域。

  局部作用域的特性，外部无法访问。如全局作用域第一个代码片段中的`console.log(a)`会提示报错。

- ES6的块级作用域

  - ES5只有全局作用域和函数作用域，没有块级作用域，会带来下面问题：

  ```javascript
  // 变量提升导致内层变量可能会覆盖外层变量
  var a = 8;
  function fn() {
    console.log(a);
    if (true) {
      var a = 24;
    }
  }
  
  fn();  // undefined
  ```

  ```javascript
  // 用来计数的循环变量泄漏位全局变量
  for (var i = 0; i < 10; i++) {
    setTimeout(()=>{console.log(i)});  // 10 个 10
  }
  console.log(i); // 10
  ```

  -  ES6的块级作用域let/const

- 作用域链

  通俗地讲，当声明一个函数时，局部作用域一级一级向上包起来，就是作用域链。

  1. 当执行函数时，总是先从函数内部找寻局部变量

  2. 如果内部找不到（函数的局部作用域没有），则会向创建函数的作用域（声明函数的作用域）寻找，依次向上

  ```javascript
  var a = 1;
  function fn () {
    var a = 2;
    function fn1 () {
      var a = 3;
      console.log(a); // 3
    }
    function fn2 () {
      console.log(a); // 2
    }
    fn1();
    fn2();
  }
  
  fn();
  console.log(a); // 1
  ```



### 闭包

- 概念
  - **闭包函数：**声明在一个函数中的函数，叫做闭包函数。
  - **闭包：**内部函数总是可以访问其所在的外部函数中声明的参数和变量，即使在其外部函数被返回（寿命终结）了之后。
  - 当函数可以记住并访问所在的词法作用域时，就产生了闭包 **（你不知道的JavaScript）**
  - 闭包是指有权访问另一个函数作用域中的变量的函数  **(JavaScript高级程序设计)**

```javascript
// 示例1
function outerFn(){
  var i = 0; 
  function innerFn(){
      i++;
      console.log(i);
  }
  return innerFn;
}
var inner = outerFn();  //每次外部函数执行的时候，外部函数的地址不同，都会重新创建一个新的地址
inner();  // 1
inner();  // 2
inner();  // 3
var inner2 = outerFn();
inner2(); // 1
inner2(); // 2
inner2(); // 3
```

```javascript
// 示例2
var i = 0;
function outerFn(){
  function innnerFn(){
       i++;
       console.log(i);
  }
  return innnerFn;
}
var inner1 = outerFn();
var inner2 = outerFn();
inner1();  // 1s
inner2();  // 2
inner1();  // 3
inner2();  // 4
```

```javascript
// 示例3
function m1(){
     var x = 1;
     return function(){
          console.log(++x);
     }
}
 
m1()();   //2
m1()();   //2
m1()();   //2
 
var m2 = m1();
m2();   //2
m2();   //3
m2();   //4
```

- 闭包的实际使用

```javascript
// 计时器
function wait(message) {
	setTimeout(function timer() {
		console.log(message)
	}, 1000)
}
wait('hello 闭包')
```

```javascript
// jQuery
function doSomeing(selector,doWhat) {
	$(selector).onClick(function(){
		console.log(doWhat)
	})
}
doSomeing('#dom1','dowhat')
```

```javascript
// 防抖
function debounce(func, delay) {
    var timer;   //计时器id
    return function () {
        clearTimeout(timer)  //清除计时器
        timer = setTimeout(func, delay);
    }
}
debounce(function(){console.log("test"),1000);
...
...
...
```

- 闭包实操题

> 编写一个方法，实现：
>
> var addSix = createBase(6);
>
>  addSix(10); // 返回 16 
>
> addSix(21); // 返回 27

```javascript
function createBase (num) {
  return function (n) {
    return num + n;
  }
}
var addSix = createBase(6);
addSix(10); // 返回 16 
addSix(21); // 返回 27
```

