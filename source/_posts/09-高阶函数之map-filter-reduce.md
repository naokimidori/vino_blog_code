---
title: "高阶函数之map filter reduce"
date: 2019/10/10 12:46:25
categories:
    - 前端
    - javascript
tags:
    - javascript
description: 高阶函数指的是一个函数以函数为参数，或以函数为返回值，或者既以函数为参数又以函数为返回值
cover: http://ww1.sinaimg.cn/large/8347ed67ly1g83rfo47pjj20e80e8jre.jpg
---

# 高阶函数
>高阶函数指的是一个函数以函数为参数，或以函数为返回值，或者既以函数为参数又以函数为返回值

高阶函数经常用于：

- 抽象或隔离行为、作用，异步控制流程作为回调函数，promises，monads等
- 创建可以泛用于各种数据类型的功能
- 部分应用于函数参数（偏函数应用）或创建一个柯里化的函数，用于复用或函数复合。
- 接受一个函数列表并返回一些由这个列表中的函数组成的复合函数


### js一些内置的高阶函数
`Array.prototype.map`
`Array.prototype.filter` 
`Array.prototype.reduce `

#### 一张图讲清三者区别
![区别](https://upload-images.jianshu.io/upload_images/18509339-c81a84969495d496.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

---
## map
>map() 方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。map 不会改变原数组。
```javascript
var animals = [
  { name: "Fluffykins", species: "rabbit" },
  { name: "Caro", species: "dog" },
  { name: "Hamilton", species: "dog" },
  { name: "Harold", species: "fish" },
  { name: "Ursula", species: "cat" },
  { name: "Jimmy", species: "fish" }
];

// 不使用高阶函数
var names = [];
for (let i = 0; i < animals.length; i++) {
  names.push(animals[i].name);
}
console.log(names); //["Fluffykins", "Caro", "Hamilton", "Harold", "Ursula", "Jimmy"]


// 使用高阶函数
var names = animals.map(x=>x.name);
console.log(names); //["Fluffykins", "Caro", "Hamilton", "Harold", "Ursula", "Jimmy"]
```
---
## filter
>filter() 方法会创建一个新数组，其中包含所有通过回调函数测试的元素。
filter 为数组中的每个元素调用一次 callback 函数， callback 函数返回 true 表示该元素通过测试，保留该元素，false 则不保留。filter 不会改变原数组，它返回过滤后的新数组。
```javascript
var animals = [
  { name: "Fluffykins", species: "rabbit" },
  { name: "Caro", species: "dog" },
  { name: "Hamilton", species: "dog" },
  { name: "Harold", species: "fish" },
  { name: "Ursula", species: "cat" },
  { name: "Jimmy", species: "fish" }
];

// 不使用高阶函数
var dogs = [];
for (var i = 0; i < animals.length; i++) {
  if (animals[i].species === "dog") dogs.push(animals[i]);
}
console.log(dogs); 


// 使用高阶函数
var dogs = animals.filter(x => x.species === "dog");
console.log(dogs); // {name: "Caro", species: "dog"} // { name: "Hamilton", species: "dog" }

```
---
## reduce
>reduce 方法对调用数组的每个元素执行回调函数，最后生成一个单一的值并返回。 reduce 方法接受两个参数：1）reduce 函数（回调），2）一个可选的 initialValue。
reduce() 方法接收一个函数作为累加器，数组中的每个值（从左到右）开始缩减，最终计算为一个值。

#### 语法
`arr.reduce(callback,initialValue)`

#### reduce的一些应用场景
1.求和求积
```javascript
var arr = [1, 2, 3, 4];
var sum = arr.reduce((x,y)=>x+y)
var mul = arr.reduce((x,y)=>x*y)
console.log( sum ); //求和，10
console.log( mul ); //求乘积，24
```
2.计算数组中每个元素出现的次数
```javascript
let names = ['Alice', 'Bob', 'Tiff', 'Bruce', 'Alice'];

let nameNum = names.reduce((pre,cur)=>{
  if(cur in pre){
    pre[cur]++
  }else{
    pre[cur] = 1 
  }
  return pre
},{})
console.log(nameNum); //{Alice: 2, Bob: 1, Tiff: 1, Bruce: 1}
```
3.数组去重
```javascript
let arr = [1,2,3,4,4,1]
let newArr = arr.reduce((pre,cur)=>{
    if(!pre.includes(cur)){
      return pre.concat(cur)
    }else{
      return pre
    }
},[])
console.log(newArr);// [1, 2, 3, 4]
```
4.将二维数组转化为一维
```javascript
let arr = [[0, 1], [2, 3], [4, 5]]
let newArr = arr.reduce((pre,cur)=>{
    return pre.concat(cur)
},[])
console.log(newArr); // [0, 1, 2, 3, 4, 5]
```
5.将多维数组转化为一维
```javascript
let arr = [[0, 1], [2, 3], [4,[5,6,7]]]
const newArr = function(arr){
   return arr.reduce((pre,cur)=>pre.concat(Array.isArray(cur)?newArr(cur):cur),[])
}
console.log(newArr(arr)); //[0, 1, 2, 3, 4, 5, 6, 7]
```
6.对象里的属性求和
```javascript
var result = [
    {
        subject: 'math',
        score: 10
    },
    {
        subject: 'chinese',
        score: 20
    },
    {
        subject: 'english',
        score: 30
    }
];

var sum = result.reduce(function(prev, cur) {
    return cur.score + prev;
}, 0);
console.log(sum) //60
```
7.将[1,3,1,4]转为数字1314
```javascript
function addDigitValue(prev,curr,curIndex,array){
    var exponent = (array.length -1) -curIndex;
    var digitValue = curr*Math.pow(10,exponent);
    return prev + digitValue;
}
var arr6 = [1,3,1,4];
var result7 = arr6.reduce(addDigitValue,0)
console.info('result7',result7)
```
### 参考链接
https://juejin.im/post/5cb30e2ce51d456e63760450#heading-9
https://www.cnblogs.com/chengxs/p/11088238.html