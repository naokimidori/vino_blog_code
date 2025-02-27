---
title: "Hexo博客网站搭建的过程"
date: 2019/9/1 12:46:25
updated: 2019/9/3 16:22:13
categories:
    - 工具
    - hexo博客
tags:
    - tool
    - blog
    - hexo
description: 自从接触了前端这行，一直就想鼓捣一个自己的博客网站。一方面呢，可以记录一下平时所见所学以及工作中遇到的难点。二来也可以用来交(zhuang)流(B)。后来找工作时发现许多公司都会问你是否有个人主页之类的，想来也是一个求职的加分项。
cover: https://s2.ax1x.com/2019/09/07/n1dPLF.jpg
---

## 写在最前:

&emsp;👉 自从接触了前端这行，一直就想鼓捣一个自己的博客网站。一方面呢，可以记录一下平时所见所学以及工作中遇到的难点。二来也可以用来交(zhuang)流(B)😜。后来找工作时发现许多公司都会问你是否有个人主页之类的，想来也是一个求职的加分项。于是果断搞起!
&emsp;👉 其实之前也有过记录文章的习惯，最开始使用印象笔记，主要是给自己看。后来发现印象笔记的 markdown 编辑器实在是难用，果断弃之。自从有这个想法以来，也浏览过博客园以及 CSDN，博客园的网页外观像是十年前的网页，不忍直视。CSDN 的网站全部充斥着各种广告，对于我这种精神洁癖的人来说，难以接受。目前国内我觉得掘金论坛以及简书做的都还是不错。之前我也在简书上记录过几篇文章，但最近简书内容审查，几个月之内不能写文章，这又让我很难受了 😭。于是乎自己便决定搞一个网站来玩玩，毕竟我也算是业内人士了 🤔！
&emsp;👉 经过我长时间(实际上是上班摸鱼时间)的调查，决定使用 Hexo + github 来搭建最初的版本。之所以部署在 github 上，最大的原因肯还不是穷！国内阿里云腾讯云一年几大百，遭不住！虽然 github 服务器，访问起来有点慢，但也无所谓了。毕竟也没几个人会来访问的 🙃。至于以后要不要迁移到国内服务器上，再说吧~
&emsp;👉 不说废话了，开搞开搞~

<br/>
 
## Hexo 介绍

&emsp;[Hexo](https://hexo.io/zh-cn/)：Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
&emsp;**使用感受**: 确实快，简洁。而且还有现成的主题，直接套就完事了。具体安装文档里面都有。

<br/>
 
## 准备工作

### 一个 github 仓库

&emsp;注意这个仓库最好和你 github 的 username 一致。比如你 github 的名字叫 cxk，你的这个仓库名字就叫做`cxk.github.io`，今后博客的打包生成的代码就放在这个仓库里面就行了。这个`cxk.github.io`也是博客访问的地址。

### nodejs 以及 Hexo 脚手架

&emsp;这个我想程序猿都会装吧。照着 Hexo 文档一步一步整就完事了~
&emsp;Hexo 脚手架安装: `npm install -g hexo-cli`

### 初始化生成项目

&emsp;安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件

```
hexo init <folder>
cd <folder>
npm install
```

&emsp;新建完成后，指定文件夹的目录如下：

```
.
├── _config.yml   //配置文件
├── package.json  //包文件信息
├── scaffolds     //模板文件，简单来说写的文章就是根据这个创建的
├── source        //页面级文件
|   ├── _drafts
|   └── _posts
└── themes        //主题，官网一大堆，看见喜欢的copy就行了
```

<br/>
 
## 主题 theme

&emsp;hexo 丰富的主题选择也是我使用它的主要原因。因为真的简单，会不会编程都没关系。傻瓜式的一步一步来，你的网站就出来啦！
&emsp;这次我选的是一个叫 [ButterFly](https://jerryc.me/) 的主题，由衷的感谢作者的开源精神。
&emsp;更多的详细配置参考主题的更多的详细配置参考主题的[安装文档](https://jerryc.me/posts/21cfbf15/#Page-Front-matter)

<br/>
 
## 发布文章

&emsp;博客网站嘛，最重要的当然是写文章、展示文章功能！(其实我觉得狂拽酷炫才是最重要的...😂)
&emsp;废话少说~~

### 新建文章

&emsp;新建文章的话，可以直接在根目录的 source 文件夹下的\_posts 文件夹下右键新建 md 文件
&emsp;**但是：**

> 作为一名 21 世纪的程序猿，推荐使用命令行方式，这样显得更 Geek 一点 😎，
> 打开命令行,例如：`hexo new "xxxx"`

### Front-matter

> Front-matter 是文件最上方以 --- 分隔的区域，用于指定个别文件的变量

通俗讲，就是文章页面的一些配置信息:

```markdown
---
title: 标题
date:  日期
tags:  标签
categories: 分类(归档)
keywords:   关键词
description: 描述
top_img:  文章顶部图片，没有的话展示封面图
comments  是否显示评论（除非设置false,可以不写）
cover:  封面图，没有的话展示默认图
toc:  是否显示toc 
toc_number: 是否显示toc数字
---

下面是文章的正式部分...
...
```

### 预览与生成

> `hexo s` 本地预览，会打开一个`http://localhost:4000/`的地址，能够实时刷新预览
> `hexo clean` 删除原来的 dist 目录
> `hexo g` 打包生成

### 快速部署

#### 安装 `hexo-deployer-git`

&emsp;`npm install hexo-deployer-git --save`

#### 配置文件

&emsp;然后在根目录下的`_config.yml`文件配置:

```
deploy:
    type: git
    repo: https://github.com/xxx/xxxx.github.io.git   //git仓库地址
```

#### 推送到 github 上

&emsp;命令行：`hexo d`即可

### 访问网站

&emsp;推送到 github 仓库之后，打开浏览器输入`xxx.github.io`就可以访问了

<br/>
 
## 参考资料

1. [hexo-theme-butterfly 安裝文檔](https://jerryc.me/posts/21cfbf15/)

2. [使用 hexo 搭建个人博客网站最完整详细教程](https://blog.csdn.net/wistbean/article/details/82291124)
