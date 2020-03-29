---
title: "JavaScript基础整理2"
date: 2019/12/03 17:00:09
categories:
    - JavaScript
tags:
    - JavaScript
description: js基础面试题整理
cover: https://s1.ax1x.com/2020/03/29/GETWQ0.png
---
### JavaScript 中的相等性

JavaScript 中有严格比较和类型转换比较：

- 严格比较（例如 ===）在不允许强制转型的情况下检查两个值是否相等；
- 抽象比较（例如 ==）在允许强制转型的情况下检查两个值是否相等。

```javascript
var a = "24";
var b = 24;
a == b;         // true
a === b;        // false
```

### 回调函数

回调函数是可以作为**参数传递给另一个函数的函数**，并在某些操作完成后执行。

```javascript
function modifyArray(arr, callback) {
  // 对 arr 做一些操作
  arr.push(100);
  // 执行传进来的 callback 函数
  callback();
}

var arr = [1, 2, 3, 4, 5];

modifyArray(arr, function() {
  console.log("array has been modified", arr);
});
```

### "use strict"的作用是什么？

严格模式`use strict`是ES5引入的，更好的将错误检测引入代码的方法。顾名思义，使得JS在更严格的条件下运行。

```javascript
function doSomething(val) {
  "use strict"; 
  x = val + 10;  // 错误地创建了全局变量
}
doSomething(1);  // Uncaught ReferenceError: x is not defined
```

### null 和 undefined

```javascript
// 数据类型不同
typeof(null)  		// object
typeof(undefined) // undefined

// 相等性
null == undefined  // true
null === undefined // false

// Number转换
Number(null) 			 // 0
Number(undefined)  // NaN

// Boolean转换
Boolean(null) 		 // false
Boolean(undefined) // false
```

- null表示"没有对象"，即该处不应该有值。典型用法是：
  - 作为函数的参数，表示该函数的参数不是对象。
  - 作为对象原型链的终点**null**。

- undefined表示"缺少值"，就是此处应该有一个值，但是还没有定义。典型用法是：

  - 变量被声明了，但没有赋值时，就等于undefined。
  - 调用函数时，应该提供的参数没有提供，该参数等于undefined。

  - 对象没有赋值的属性，该属性的值为undefined。
  - 函数没有返回值时，默认返回undefined。

- null == undefined 为true？	

> 从Javascript规范中找到答案：
>
> 规范中提到， **要比较相等性之前，不能将 null 和 undefined 转换成其他任何值**，并且规定null 和 undefined 是相等的。

### JavaScript 中的数据类型

**值类型(基本类型)**：字符串（String）、数字(Number)、布尔(Boolean)、空（Null）、未定义（Undefined）、Symbol。

**引用数据类型**：对象(Object)、数组(Array)、函数(Function)。

> Symbol 是 ES6 引入了一种新的原始数据类型，表示独一无二的值。



### 事件冒泡和事件捕获

事件冒泡

- 概念：从触发事件的那个节点一直到`document`，是自下而上的去触发事件。
- 阻止冒泡： e.stopPropagation() 或 e.cancelBubble() --- IE

事件捕获

- 概念： 从`document`到触发事件的那个节点，即自上而下的去触发事件。
- dom.addEventListener('click', function(){}, true)  第三个参数为true的话代表事件捕获

DOM事件流(event flow)

	1. 事件捕获
 	2. 处于目标事件
 	3. 事件冒泡

