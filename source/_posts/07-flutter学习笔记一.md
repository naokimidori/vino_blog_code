---
title: "Flutter学习笔记(1) 开发环境搭建"
categories:
    - 前端
    - flutter
tags:
    - 学习
    - flutter
description: 从零学flutter之开发环境搭建
cover: http://ww1.sinaimg.cn/large/8347ed67gy1g74z0mtz31j20go09emx8.jpg
---

## Flutter

官方介绍:

> Flutter 是 Google 开源的 UI 工具包，帮助开发者通过一套代码库高效构建多平台精美应用，支持移动、Web、桌面和嵌入式平台。

不同于其他我们熟知的移动端跨平台方案，Flutter 更像游戏引擎，因为 Flutter 有自己的渲染引擎：我们在 Flutter 上写了界面后，Flutter 会在自己的 canvas 上渲染，移动端不负责绘制。

Flutter 开辟了一种全新的思路，利用 Dart 语言，同时支持 JIT 和 AOT 两种编译方式的特性，在不同场景下使用不同的编译方式，达到最高效的开发和运行体验。

在 Debug 模式下，为了保证开发体验，采用 JIT 这种动态编译的方式，将代码运行在 Dart 虚拟机上，使得我们编写的代码可以实时更新，实现 HotReload 的特性，提升开发体验。

而在 Release 模式下，又需要保证运行速度和渲染流程度，则会采用 AOT 的编译方式，将代码直接编译成各自平台的 Native 代码，以此提高使用体验。

在 UI 渲染方面， Flutter 的渲染不依赖于平台，基于自带的 Skia 渲染引擎 ，构建了一套完整的跨平台 UI 渲染框架；在和平台交互方面，Flutter 提供了 Platform Channel 的通道，可以方便的和 Native 交互。可以说是 Google 融合多种技术才有的产物，也是跨平台方案发展的必然产物。

除此之外，一个好的技术，还需要有完善的文档去让人学习，有专业的人去维护，让技术不断发展，而在这方面，Flutter 即有完善的文档，也有 Google 团队的维护。因此 Flutter 肯定会更好的发展。

<!--## Flutter VS React Native-->
<!--待续~-->

## 搭建 Flutter 开发环境

### 系统要求

要想安装和运行 Flutter，你的开发环境至少应该满足如下的需求：

-   操作系统：Windows 7 SP1 或更高的版本（64 位操作系统）。
-   磁盘空间：除安装 IDE 和一些工具之外还应有至少 400 MB 的空间。
-   工具：要让 Flutter 在你的开发环境中正常使用，依赖于以下的工具：

    -   Windows PowerShell 5.0
    -   Git for Windows 2.x

### 配置 Flutter 中国镜像

#### 镜像源

国内有两个镜像可以用

-   Flutter 社区

&emsp;&emsp;FLUTTER_STORAGE_BASE_URL: `https://storage.flutter-io.cn`

&emsp;&emsp;PUB_HOSTED_URL: `https://pub.flutter-io.cn`

-   上海交通大学 Linux 用户组

&emsp;&emsp;FLUTTER_STORAGE_BASE_URL:`https://mirrors.sjtug.sjtu.edu.cn`

&emsp;&emsp;PUB_HOSTED_URL: `https://dart-pub.mirrors.sjtug.sjtu.edu.cn`

#### windows 下的配置方法

1. `计算机` -> `属性` -> `高级系统设置` -> `环境变量`，打开环境变量设置框。
2. 在用户变量下，选择`新建环境变量`，添加如下的两个环境变量和值

| 变量名                   | 值                              |
| ------------------------ | ------------------------------- |
| FLUTTER_STORAGE_BASE_URL | `https://storage.flutter-io.cn` |
| PUB_HOSTED_URL           | `https://pub.flutter-io.cn`     |

### 搭建 Android 开发环境

#### 下载 Android Studio

`Android Studio` 的下载地址有三个，选一个可以下载的地址：

-   官方地址：developer.android.com/studio
-   官方中文地址：developer.android.google.cn/studio/
-   国内第三方地址：www.androiddevtools.cn/

#### 配置 Android SDK 环境变量

![](http://ww1.sinaimg.cn/large/8347ed67gy1g6wmpjylozj20pq0fwaci.jpg)

![](http://ww1.sinaimg.cn/large/8347ed67gy1g6wmpjz53tj20sk0jz0uj.jpg)

#### 创建模拟器

![](http://ww1.sinaimg.cn/large/8347ed67gy1g6wmpk3jvdj20ox0f9769.jpg)

在打开的页面里点击 `Create Virtual Device...`

在 Phone 里选择一个设备，这里选择 `Pixel 2 XL`

![](http://ww1.sinaimg.cn/large/8347ed67gy1g6wmpky9n7j20s80j5wfj.jpg)

一直点击`next`完成~
在用户环境变量`path`中添加上
![](http://ww1.sinaimg.cn/large/8347ed67gy1g6wn4xjm9dj20f10fujrq.jpg)

### 下载 Flutter SDK

#### 命令行方式

1. 打开命令行窗口，cd 到安装 Flutter SDK 的目录
2. 安装稳定版 `git clone -b stable https://github.com/flutter/flutter.git`
3. 打开 flutter 的文件夹，双击运行 `flutter_console.bat` 开始安装

_这种方式有时候网速慢，容易失败_

#### 直接下载压缩包方式

1. 官网下载最新稳定版本
2. 将 Flutter SDK 的 zip 包解压到一个目录下，例如`C:\src\flutter`（目录随意，但是不要放在需要权限的目录下，例如 `C:\Program Files\` ）

#### 配置环境变量

打开用户环境变量 `path`,新增一条`C:\src\flutter\bin`

### 运行 flutter doctor

上述命令会检查你的现有环境，然后把检测结果以报告形式呈现出来

```
Doctor summary (to see all details, run flutter doctor -v):
[√] Flutter (Channel stable, v1.9.1+hotfix.2, on Microsoft Windows [Version 10.0.18362.356], locale zh-CN)

[!] Android toolchain - develop for Android devices (Android SDK version 29.0.2)
    ! Some Android licenses not accepted.  To resolve this, run: flutter doctor --android-licenses
[!] Android Studio (version 3.5)
    X Flutter plugin not installed; this adds Flutter specific functionality.
    X Dart plugin not installed; this adds Dart specific functionality.
[!] Connected device
    ! No devices available

! Doctor found issues in 3 categories.
```

问题 1：`Some Android licenses not accepted.`

解决：命令`flutter doctor --android-licenses`,手动输入`y`即可

问题 2：`Flutter plugin not installed` 和 `Dart plugin not installed`

解决：进入 Android Studio 的设置`settings`中的`plugins`搜索下载即可

问题 3：`No devices available`

解决：使用 Android Studio 连接手机调试。

## 开发使用的 IDE

1. android studio
2. vscode

推荐`vscode`,安装`flutter`插件
![](http://ww1.sinaimg.cn/large/8347ed67gy1g6wqkes52jj210v0fcq5o.jpg)

**至此，flutter 开发环境搭建完毕~**

## 参考资料

1. [搭建 Flutter 开发环境](https://juejin.im/book/5c5423ef6fb9a049cd54a213/section/5c615b6751882562e66c8f9e)
2. [Flutter 学习笔记（1）：开发环境搭建](https://cloud.tencent.com/developer/news/240657)
