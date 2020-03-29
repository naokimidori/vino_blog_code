---
title: "JavaScript基础整理3"
date: 2020/01/14 18:21:09
categories:
    - JavaScript
tags:
    - JavaScript
description: js基础面试题整理
cover: https://s1.ax1x.com/2020/03/29/GETWQ0.png
---
### 如何判断一个数字是否是整数

思路： 对1进行取模，看看是否有余数

```javascript
function isInt(num) {
  return num % 1 === 0;
}

console.log(isInt(4)); // true
console.log(isInt(12.2)); // false
console.log(isInt(0.3)); // false
```



###  比较两个对象

方式一：

​	**通过`JSON.stringify(obj)`来判断两个对象转后的字符串是否相等**

- 优点：用法简单，对于**顺序相同**的两个对象可以快速进行比较得到结果
- 缺点：当两个对比的对象中**key的顺序不是完全相同**时会比较出错

方式二：

​	层级较少，可以自己写一个方法，通过遍历其中一个对象的keys，使用Obeject.hasOwnProperty可以进行判断

```javascript
/*
 * @param x {Object} 对象1
 * @param y {Object} 对象2
 * @return  {Boolean} true 为相等，false 为不等
 */
var deepEqual = function (x, y) {
  // 指向同一内存时
  if (x === y) {
    return true;
  }
  else if ((typeof x == "object" && x != null) && (typeof y == "object" && y != null)) {
    if (Object.keys(x).length != Object.keys(y).length)
      return false;
 
    for (var prop in x) {
      if (y.hasOwnProperty(prop))
      {  
        if (! deepEqual(x[prop], y[prop]))
          return false;
      }
      else
        return false;
    }
 
    return true;
  }
  else 
    return false;
}
```



方式三：

​	最好是依靠完善的测试库，涵盖了各种边界情况。Underscore和Lodash有一个名为_.isEqual()方法，用来比较好的处理深度对象的比较。

### Array.from()

Array.from()方法就是将一个类数组对象或者可遍历对象转换成一个真正的数组。

要将一个类数组对象转换为一个真正的数组，必须具备以下条件：

- 该类数组对象必须具有length属性，用于指定数组的长度。如果没有length属性，那么转换后的数组是一个空数组。

- 该类数组对象的属性名必须为数值型或字符串型的数字

- 该类数组对象的属性名可以加引号，也可以不加引号

```javascript
let arrayLike1 = {
    0: 'tom', 
    1: '65',
    2: '男',
    3: ['jane','john','Mary'],
    'length': 4
}
let arr1 = Array.from(arrayLike1)
console.log(arr1) // ['tom','65','男',['jane','john','Mary']

let arrayLike2 = {
    'name': 'tom', 
    'age': '65',
    'sex': '男',
    'friends': ['jane','john','Mary'],
    length: 4
}
let arr2 = Array.from(arrayLike2)
console.log(arr2)  // [ undefined, undefined, undefined, undefined ]
```

将Set结构的数据转换为真正的数组：　

```javascript
let arr = [1, 2, 3, 1, 2, 3, 4]
let set = new Set(arr)
console.log(Array.from(set))  // [ 1, 2, 3, 4 ]
```

### JavaScript执行机制

```javascript
// 示例一
console.log('a');

new Promise(resolve => {
    console.log('b')
    resolve()
}).then(() => {
    console.log('c')
    setTimeout(() => {
      console.log('d')
    }, 0)
})

setTimeout(() => {
    console.log('e')
    new Promise(resolve => {
        console.log('f')
        resolve()
    }).then(() => {
        console.log('g')
    })
}, 100)

setTimeout(() => {
    console.log('h')
    new Promise(resolve => {
        resolve()
    }).then(() => {
        console.log('i')
    })
    console.log('j')
}, 0)

// a b c h j i d e f g 
```

1. 打印 `a`
2. `promise` 立即执行，打印 `b`
3. `promise.then` 推入微任务队列
4. `setTimeout` 推入宏任务队列
5. 整段代码执行完毕，开始执行微任务，打印 `c` ，遇到 `setTimeout` 推入宏任务队列排队等待执行
6. 没有可执行的微任务开始执行宏任务，定时器按照延迟时间排队执行
7. 打印 `h j` ，`promise.then` 推入微任务队列
8. 有可执行的微任务，打印 `i` ，继续执行宏任务，打印 `d`
9. 执行延迟为100的宏任务，打印 `e f`，执行微任务打印 `g`，所有任务执行完毕

---

```javascript
// 示例二
console.log('start')

a().then(() => {
  console.log('a_then')
})

console.log('end')

function a() {
  console.log('a_function')
  return b().then((res) => {
    console.log('res', res)
    console.log('b_then')
    return Promise.resolve('a方法的返回值')
  })
}

function b() {
  console.log('b_function')
  return Promise.resolve('返回值')
}

// start a_function b_function end （res 返回值） b_then a_then
```

#### 总结

- `JavaScript` 单线程，任务需要排队执行
- 同步任务进入主线程排队，异步任务进入事件队列排队等待被推入主线程执行
- 定时器的延迟时间为 0 并不是立刻执行，只是代表相比于其他定时器更早的被执行
- 以宏任务和微任务进一步理解Js执行机制
- 整段代码作为宏任务开始执行，执行过程中宏任务和微任务进入相应的队列中
- 整段代码执行结束，看微任务队列中是否有任务等待执行，如果有则执行所有的微任务，直到微任务队列中的任务执行完毕，如果没有则继续执行新的宏任务
- 执行新的宏任务，凡是在执行宏任务过程中遇到微任务都将其推入微任务队列中执行
- 反复如此直到所有任务全部执行完毕