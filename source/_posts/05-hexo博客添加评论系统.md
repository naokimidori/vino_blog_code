---
title: "Hexo博客添加评论系统"
date: 2019/9/7 12:46:25
updated: 2019/9/8 16:22:13
categories:
    - 工具
tags:
    - tool
    - blog
    - hexo
    - valine
description: 当别人浏览你的文章时，想和你互动一波。所以，没评论系统怎么行~
cover: https://s2.ax1x.com/2019/09/07/n1dPLF.jpg
---

<br/>

## 添加评论系统

&emsp;当别人浏览你的文章时(万一有人来看呢 🙃)，想和你互动一波。所以，没评论系统怎么行！
&emsp;现在网上有很多评论系统服务，比较常见的：

> 1. 多说 ：http://duoshuo.com/
> 2. 畅言 ：https://changyan.kuaizhan.com/
> 3. Valine：https://valine.js.org/
> 4. Disqus：https://disqus.com/
> 5. 友言: http://www.uyan.cc/
> 6. gitment: https://github.com/imsun/gitment

&emsp;我选择的是 `Valine`，不需要访客登录，可以添加邮件提醒功能。
&emsp;先注册[leancloud](https://leancloud.cn/)账户，进入控制台
&emsp;创建应用，然后在设置-应用 key 获取当前应用的`APP ID`和`APP Key`
&emsp;在`themes`-`ButterFly`-`_config.yml`配置如下代码:

```yml
valine:
    enable: true
    appId: xxxxx #你的app id
    appKey: xxxxx #你的app key
    notify: false
    verify: false
    pageSize: 10
    avatar: wavatar
    lang: zh-cn
    placeholder: 留下你的足迹吧!
    guest_info: 昵称,邮箱,website
```

<br/>

## 管理评论数据

&emsp;由于 Valine 是无后端评论系统，所以也就没有评论数据管理功能。

> 当然，鲁迅曾说过：只要思想不滑坡，办法总比困难多

&emsp;所以，这里配合[@DesertsP](https://github.com/DesertsP)开发的[Valine-Admin](https://github.com/DesertsP/Valine-Admin)能够比较轻松的管理评论！具体配置见文档~

&emsp;大概配置如下:
![leancloud配置](https://s2.ax1x.com/2019/09/11/ndXNUH.png)

<br/>
 
## 参考资料

1. [hexo-theme-butterfly 安裝文檔](https://jerryc.me/posts/21cfbf15/)

2. [使用 hexo 搭建个人博客网站最完整详细教程](https://blog.csdn.net/wistbean/article/details/82291124)
