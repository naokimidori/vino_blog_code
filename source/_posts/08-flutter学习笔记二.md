---
title: "Flutter学习笔记(2)之常用组件~1"
categories:
    - 前端
    - flutter
tags:
    - 学习
    - flutter
description: 常用组件1：Text Widget文本组件、Container容器组件
cover: http://ww1.sinaimg.cn/large/8347ed67gy1g74z0mtz31j20go09emx8.jpg
---

> Flutter 一切皆组件！

## 01-Text Widget

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext content) {
    return MaterialApp(
      title: "Tittle",
      home: Scaffold(
        body: Center(
            child: Text(
          '我叫 vino ,热爱前端, 梅西忠实粉丝, 今天2019/09/24，梅西获得了职业生涯第六座世界足球先生奖杯🏆，高兴！😃',
          textAlign: TextAlign.left,
        )),
      ),
    );
  }
}
```

### 1.1 textAlign 属性

文本对齐格式

```dart
child: Text(
  '我叫 vino ,热爱前端, 梅西忠实粉丝, 今天2019/09/24，梅西获得了职业生涯第六座世界足球先生奖杯🏆，高兴！😃',
  textAlign: TextAlign.left
))
```

默认`left`,可以设置为`left` `center` `right` `start` `end`
![left和start](http://ww1.sinaimg.cn/large/8347ed67gy1g7aof9cigqj20cv0nzabn.jpg)
![center](http://ww1.sinaimg.cn/large/8347ed67gy1g7aof9dg1tj20cv0nz403.jpg)
![right和end](http://ww1.sinaimg.cn/large/8347ed67gy1g7aof9hmftj20cv0nz75v.jpg)

### 1.2 maxLines 属性

最大行数，超出隐藏

```dart
 child: Text(
  '我叫 vino ,热爱前端, 梅西忠实粉丝, 今天2019/09/24，梅西获得了职业生涯第六座世界足球先生奖杯🏆，高兴！😃',
  textAlign: TextAlign.center,
  maxLines: 1,
))
```

![最大行数](http://ww1.sinaimg.cn/large/8347ed67gy1g7aoisusnsj20c80nh0u4.jpg)

### 1.3 overflow 属性

用来处理文本溢出

-   clip：直接切断，剩下的文字就没有了，感觉不太友好，体验性不好。
-   ellipsis:在后边显示省略号，体验性较好，经常使用。
-   fade: 溢出的部分会进行一个渐变消失的效果，当然是上线的渐变，不是左右的哦。

```dart
child: Text(
  '我叫 vino ,热爱前端,梅西忠实粉丝,今天2019/09/24，梅西获得了职业生涯第六座世界足球先生奖杯🏆，高兴！😃',
  textAlign: TextAlign.center,
  maxLines: 1,
  overflow: TextOverflow.ellipsis,
))
```

![clip](http://ww1.sinaimg.cn/large/8347ed67gy1g7aora02aaj20b301o746.jpg)
![ellipsis](http://ww1.sinaimg.cn/large/8347ed67gy1g7aor9zumgj20ba01st8m.jpg)
![fade](http://ww1.sinaimg.cn/large/8347ed67gy1g7aor9zqfxj20b501q746.jpg)

### 1.4 style 属性

style 属性有很多，使用时查询 [api 手册](https://api.flutter.dev/flutter/painting/TextStyle-class.html) 即可
例如: 字体大小 25，红色，下划线

```dart
style: TextStyle(
  fontSize: 25.0,
  color: Color.fromRGBO(220, 20, 60, 1),
  decoration: TextDecoration.underline,
  decorationColor: Colors.blue,
  decorationStyle: TextDecorationStyle.wavy
)
```

![style](http://ww1.sinaimg.cn/large/8347ed67gy1g7aq5jk6z3j20ba03j3z7.jpg)

## 02-Container 容器组件

这个组件相当于`HTML`中的`div`

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Container Widget',
      home: Scaffold(
        body: Center(
          child: Container(
            child: new Text('Hello Vino', style: TextStyle(fontSize: 40.0)),
            alignment: Alignment.topCenter,
            width: 500.0,
            height: 400.0,
            color: Colors.lightBlue,
          ),
        ),
      ),
    );
  }
}

```

![Container](http://ww1.sinaimg.cn/large/8347ed67gy1g7arfl6sgwj20bp0nyabd.jpg)

### 2.1 Alignment 属性

-   `bottomCenter`:下部居中对齐。
-   `botomLeft`: 下部左对齐。
-   `bottomRight`：下部右对齐。
-   `center`：纵横双向居中对齐。
-   `centerLeft`：纵向居中横向居左对齐。
-   `centerRight`：纵向居中横向居右对齐。
-   `topLeft`：顶部左侧对齐。
-   `topCenter`：顶部居中对齐。
-   `topRight`： 顶部居左对齐。

### 2.2 width height color 属性

```dart
child: Container(
    child: new Text('Hello Vino', style: TextStyle(fontSize: 40.0)),
    alignment: Alignment.topCenter,
    width: 500.0,
    height: 400.0,
    color: Colors.lightBlue,
)
```

### 2.3 padding 属性

```dart
child: Container(
    child: new Text('Hello Vino', style: TextStyle(fontSize: 40.0)),
    alignment: Alignment.topLeft,
    width: 500.0,
    height: 400.0,
    color: Colors.lightBlue,
    padding: const EdgeInsets.fromLTRB(30.0, 50.0, 0.0, 0.0),
)
```

![padding](http://ww1.sinaimg.cn/large/8347ed67gy1g7arpu8qfbj20bw0nngmy.jpg)

-   如果四周 padding 值相同，直接可以:`padding:const EdgeInsets.all(10.0)`
-   `EdgeInsets.fromLTRB(value1,value2,value3,value4)`的 value 值分别为**左、上、右、下**

### 2.4 margin 属性

同 padding 属性一样

`margin: const EdgeInsets.fromLTRB(30.0, 0.0, 10.0, 20.0)`

或者

`margin: const EdgeInsets.all(20.0)`

### 2.5 decoration 属性

`decoration`是 `container` 的修饰器，主要的功能是设置背景和边框。

```dart
child: Container(
      child: new Text('Hello Vino', style: TextStyle(fontSize: 40.0)),
      alignment: Alignment.topLeft,
      width: 500.0,
      height: 400.0,
      // color: Colors.lightBlue,
      padding: const EdgeInsets.fromLTRB(30.0, 50.0, 0.0, 0.0),
      margin: const EdgeInsets.all(10.0),
      decoration: new BoxDecoration(
          gradient: const LinearGradient(
            colors: [Colors.cyan, Colors.purple, Colors.red]
          ),
          border: Border.all(width: 5.0, color: Colors.yellow)
        )
      )
```

![decoration](http://ww1.sinaimg.cn/large/8347ed67gy1g7ashhzcfvj20bq0nsmyn.jpg)

-   若需要给背景加入一个渐变，这时候需要使用`BoxDecoration`这个类
-   须把之前的`color`去掉，否则会冲突
-   `border`如上述代码所示

## 参考链接

1. [Flutter 免费视频第二季-常用组件讲解](https://juejin.im/post/5bfb3bdc6fb9a049f9123e90#heading-12)
