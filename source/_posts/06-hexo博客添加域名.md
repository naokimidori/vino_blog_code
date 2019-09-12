---
title: "Hexo博客之绑定自己的域名"
categories:
    - 工具
tags:
    - tool
    - blog
    - hexo
    - 域名
description: 虽然网站已经能够访问了，但是域名却怪怪的`xxx.github.io`，所以必须得搞一个放荡不羁的域名！
cover: https://s2.ax1x.com/2019/09/07/n1dPLF.jpg
---

## 绑定自己的域名

&emsp;虽然网站已经能够访问了，但是域名却怪怪的`xxx.github.io`
&emsp;所以必须得搞一个放荡不羁的域名！
&emsp;域名网上购买渠道有很多，国内较常见的是阿里云、腾讯云之类的。
&emsp;在`xxx.github.io`这个仓库根目录添加一个名为`CNAME`的文件

![创建CNAME](https://s2.ax1x.com/2019/09/11/nwFA7q.png)

<br/>
&emsp;文件里填写的内容：要绑定的域名（不要包含 Http://和 www）

![CNAME内容](https://s2.ax1x.com/2019/09/11/nwFkBn.png)
<br/>

&emsp;进入设置
![设置](https://s2.ax1x.com/2019/09/11/nwAt6e.png)
<br/>

&emsp;保存如下
![设置](https://s2.ax1x.com/2019/09/11/nwArff.png)
<br/>

## 添加域名解析

&emsp;ping 地址 得到一个 ip
![ping域名](https://s2.ax1x.com/2019/09/11/nwVhWV.png)
<br/>

&emsp;在阿里云的[控制台](https://homenew.console.aliyun.com/)的域名选项
![域名解析](https://s2.ax1x.com/2019/09/11/nwZgXD.png)
<br/>

&emsp;选择解析，添加两个 A 记录，用得到的 IP，一个主机记录为："www"，一个为"@"
![添加解析记录](https://s2.ax1x.com/2019/09/11/nweWvT.png)
<br/>

## 访问

&emsp;**大功告成，现在可以使用自己的域名[naoki.top](http://naoki.top/)访问网站了！**

<br/>
 
## 参考资料

[github 怎么绑定自己的域名](https://www.cnblogs.com/liangmingshen/p/9561994.html)
