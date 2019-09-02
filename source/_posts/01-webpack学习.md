---
title: webpack学习笔记
date: 2019/6/30 12:46:25
updated: 2019/7/5 16:22:13
categories:
    - 前端
tags:
    - webpack
    - 工程化
description: webpack 是一个现代 JavaScript 应用程序的静态模块打包器(module bundler)。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle。
cover: https://s2.ax1x.com/2019/09/02/nPR1qP.jpg
---

## webpack 介绍

Webpack 是前端 **模块化管理** 和 **打包工具**。它可以将许多松散的模块按照依赖和规则打包成前端资源。还可以将模块**按需加载**。
通过 `loader` 的转换，任何形式的资源都可以视作模块，比如 CommonJs 模块、ES6 模块、CSS、图片、 JSON、Coffeescript、 LESS 等。

> 本质上，webpack 是一个现代 JavaScript 应用程序的静态模块打包器(module bundler)。当 webpack 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle。

![webpack原理](https://s2.ax1x.com/2019/09/02/nPRU2j.png)

### webpack 四个核心概念

-   入口(entry)
-   输出(output)
-   loader
-   插件(plugins)

### 关于模块化

1. 模块：拥有独立功能的部分
2. 模块化：一种将系统分离成独立功能部分的方法
3. 模块化解决的问题： **避免变量污染**

### CommonJS 规范

**nodejs 采用了 CommonJS 模块化规范**

1.  每个文件就是一个独立的模块，其内部所有变量私有，对外不可见
2.  每个模块内部使用 module.exports 进行私有暴露
3.  加载模块使用 require

### ES5 模块

```javascript
//引入
var a = require("./a.js");
var $ = require("jquery");

//暴露
var fuc = () => {};
module.exports.fuc = fuc;
```

### ES6 模块（2015）

```javascript
//引入
import a from './a.js

//暴露
export var fuc=( )=>{ }
```

## webpack 安装

### 全局安装,安装命令行工具

`yarn global add webpack` 或 `npm install --global webpack`

### 项目安装

初始化
`yarn init -y` 或 `npm init -y`

项目安装依赖
`yarn add webpack@3.8.1 --save-dev`

## 配置文件 webpack.config.js

> 以 3.8.1 版本为例

```javascript
var webpack = require("webpack");
var path = require("path");

//webpack配置对象
module.exports = {
    //入口
    entry: "./src/a.js", // 单入单出
    // entry:['./src/a.js','./src/c.js'],   //多入口 单出口
    // entry: {                  //多入口，多出口
    //     // key(打包以后的文件名): value(入口路径)
    //     amodule: './src/a.js',
    //     cmodule: './src/c.js'
    // },
    // 配置输出
    output: {
        //输出的路径(硬盘输出)
        path: path.resolve(__dirname, "dist/"),
        //输出的文件名
        filename: "bundle.js",
        // filename: "[name].js",  /*多出口需设置filename*/
        // webpack-dev-server 服务器输出路径
        publicPath: "/dist/"
    },
    //loader加载器配置
    module: {
        rules: [
            // css-loader
            {
                test: /\.css$/,
                use: ["style-loader", "css-loader"]
            },
            //less-loader
            {
                test: /\.less$/,
                use: [
                    {
                        loader: "style-loader" // creates style nodes from JS strings
                    },
                    {
                        loader: "css-loader" // translates CSS into CommonJS
                    },
                    {
                        loader: "less-loader" // compiles Less to CSS
                    }
                ]
            },
            //file-loader
            {
                test: /\.(png|jpg|gif)$/,
                use: [
                    {
                        loader: "file-loader",
                        options: {}
                    }
                ]
            }
        ]
    },
    //所有插件都写在此处！！！！
    plugins: [
        new webpack.BannerPlugin("作者: naoki"),
        new webpack.optimize.CommonsChunkPlugin("common") //提取公共模块
    ],
    //自动打包
    watch: true
};
```

---
