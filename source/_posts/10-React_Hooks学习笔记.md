---
title: "React Hooks学习笔记"
date: 2019/10/19 13:11:22
categories:
    - 前端
    - React
tags:
    - React
    - React Hooks
description: Hook 是 React 16.8 的新增特性。它可以让你在不编写 class 的情况下使用 state 以及其他的 React 特性,Hook 是一些可以让你在函数组件里“钩入” React state 及生命周期等特性的函数。Hook 不能在 class 组件中使用 —— 这使得你不使用 class 也能使用 React。
cover: http://ww1.sinaimg.cn/large/8347ed67ly1g83rt3e6ahj20m80ciaal.jpg
---

## ✨React Hooks
### 官网介绍
>Hook 是 React 16.8 的新增特性。它可以让你在不编写 class 的情况下使用 state 以及其他的 React 特性
### 什么是Hook?
>Hook 是一些可以让你在函数组件里“钩入” React state 及生命周期等特性的函数。Hook 不能在 class 组件中使用 —— 这使得你不使用 class 也能使用 React。

>Hook 在 class 内部是不起作用的。但可以使用它们来取代 class 

>hooks可以反复多次使用，相互独立。

### Hook带来的好处
1. Hook 使开发者在无需修改组件结构的情况下复用状态逻辑
2. 解决了嵌套地狱的问题
3. 整合生命周期
4. 不使用class从而解决了this指向问题

### 官网demo
```javascript
import React, { useState } from 'react';

function Example() {
  // 声明一个新的叫做 “count” 的 state 变量
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```
---

## 📌 State Hook
`useState`就是一个react自带的hook函数。

`useState` 会返回一对值：当前状态和一个更新它的函数，可以在事件处理函数中或其他一些地方调用这个函数。`useState` 唯一的参数就是初始 `state`

### useState及其等价的class示例

```javascript
import React, { useState } from 'react';

function Example() {
  // 声明一个叫 "count" 的 state 变量
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```
等价于(class)
```javascript
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```
#### 调用 useState 方法的时候做了什么?

- 它定义一个 “state 变量”,示例中的变量为`count`。
- 与 class 里面的 `this.state` 提供的功能完全相同。
- 般来说，在函数退出后变量就就会”消失”，而 state 中的变量会被 React 保留。

#### useState 需要哪些参数？
- seState() 方法里面唯一的参数就是初始 state

#### useState 方法的返回值是什么？
- 返回值为：当前 state 以及更新 state 的函数。

### 声明调用多个 state 变量
1. `useState`是可以多次调用的
2. `useState`接收的初始值没有规定一定要是`string`/`number`/`boolean`这种简单数据类型，它完全可以接收对象或者数组作为参数

```javascript
function ExampleWithManyStates() {
  // 声明多个 state 变量！
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
  // ...
}
```
### react是怎么保证多个useState的相互独立的？
>react是根据useState出现的顺序来定的。

```javascript
//第一次渲染
useState(42);  //将age初始化为42
useState('banana');  //将fruit初始化为banana
useState([{ text: 'Learn Hooks' }]); //...

//第二次渲染
useState(42);  //读取状态变量age的值（这时候传的参数42直接被忽略）
useState('banana');  //读取状态变量fruit的值（这时候传的参数banana直接被忽略）
useState([{ text: 'Learn Hooks' }]); //...
```
改下代码:
```javascript
let showFruit = true;
function ExampleWithManyStates() {
  const [age, setAge] = useState(42);
  
  if(showFruit) {
    const [fruit, setFruit] = useState('banana');
    showFruit = false;
  }
 
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
```
这样一来:
```javascript
//第一次渲染
useState(42);  //将age初始化为42
useState('banana');  //将fruit初始化为banana
useState([{ text: 'Learn Hooks' }]); //...

//第二次渲染
useState(42);  //读取状态变量age的值（这时候传的参数42直接被忽略）
// useState('banana');  
useState([{ text: 'Learn Hooks' }]); //读取到的却是状态变量fruit的值，导致报错
```
鉴于此，react规定必须把hooks写在函数的最外层，不能写在ifelse等条件语句当中，来确保hooks的执行顺序一致。

---

## ⚡️ Effect Hook

之前写的有状态组件(class)，通常会产生很多的副作用（side effect），比如发起ajax请求获取数据，添加一些监听的注册和取消注册，手动修改dom等等。之前都把这些副作用的函数写在生命周期函数钩子里，比如`componentDidMount`，`componentDidUpdate`和`componentWillUnmount`。而现在的`useEffect`就相当与这些声明周期函数钩子的集合体。

React 将按照 effect 声明的顺序依次调用组件中的每一个 effect。


### useEffect及其等价的class示例
```javascript
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // 更新标题
    document.title = `You clicked ${count} times`;
  });

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```
等价于(class)
```javascript
class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  componentDidMount() {
    document.title = `You clicked ${this.state.count} times`;
  }

  componentDidUpdate() {
    document.title = `You clicked ${this.state.count} times`;
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```
梳理逻辑:
首先，声明了一个状态变量`count`，将它的初始值设为0。然后告诉react，这个组件有一个副作用。给`useEffect hook`传了一个匿名函数，这个匿名函数就是副作用。在这个例子里，副作用是调用browser API来修改文档标题。当react要渲染组件时，它会先记住用到的副作用。等react更新了DOM之后，它再依次执行定义的副作用函数。

这里要注意几点：
第一，react首次渲染和之后的每次渲染都会调用一遍传给`useEffect`的函数。而之前要用两个声明周期函数来分别表示首次渲染`componentDidMount`，和之后的更新导致的重新渲染`componentDidUpdate`。

第二，useEffect中定义的副作用函数的执行不会阻碍浏览器更新视图，也就是说这些函数是**异步执行**的，而之前的componentDidMount或componentDidUpdate中的代码则是同步执行的。这种安排对大多数副作用说都是合理的，但有的情况除外，比如有时候需要先根据DOM计算出某个元素的尺寸再重新渲染，这时候希望这次重新渲染是同步发生的，也就是说它会在浏览器真的去绘制这个页面前发生。

### 清除副作用
在 React 组件中有两种常见副作用操作：需要清除的和不需要清除的。先来更仔细地看一下它们之间的区别。

#### 无需清除的 effect
>有时候，想在 React 更新 DOM之后运行一些额外的代码。比如发送网络请求，手动变更 DOM，记录日志，这些都是常见的无需清除的操作。因为在执行完这些操作之后，就可以忽略他们了。

例如之前的示例就是无需清除的 effect
```javascript
useEffect(() => {
    document.title = `You clicked ${count} times`;
});
```

#### 需要清除的 effect
为了防止引起内存泄露，需要清除 effect。例如：订阅外部数据源 

在React class 中一般在`componentWillUnmount`这个生命钩子中清除

`useEffect` 可以在组件渲染后实现各种不同的副作用。有些副作用可能需要清除，所以需要返回一个函数，如下：
```javascript
useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }
    
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
});
```
#### 怎么跳过一些不必要的副作用函数
只需要给useEffect传第二个参数即可.

用第二个参数来告诉react只有当这个参数的值发生改变时，才执行我副作用函数（第一个参数）
```javascript
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]); // 只有当count的值发生变化时，才会重新执行`document.title`这一句
```

## 自定义Hook
待续...

## 参考链接
1. [30分钟精通React Hooks](https://juejin.im/post/5be3ea136fb9a049f9121014)
2. [官网文档](https://react-1251415695.cos-website.ap-chengdu.myqcloud.com/docs/hooks-intro.html)