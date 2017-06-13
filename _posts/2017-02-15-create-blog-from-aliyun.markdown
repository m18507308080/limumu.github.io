---
layout:     post
title:      "十分钟免费搭建博客网站"
subtitle:   "零成本自建个人博客的正确打开方式"
date:       2017-02-15 10:00:00
author:     "李牧牧"
header-img: "http://cdn.static.limumu.me/assets:img:home-bg.jpg"
header-mask: 0.1
catalog:    true
tags:
    - GitHub
    - Coding
    - 七牛云
    - Jelly
---

> 本文发布于 [李牧牧的博客](http://limumu.me) 转载请保留链接 ;)



# 毛遂自荐

> 笔者博客代码的存放与解析服务归功于`GitHub`与`GitPage`的鼎力配合，资源文件的快速加载与内容分发归功于`七牛云存储`，感谢`Coding`充当了`GitHub`与`百度爬出`之间的润滑剂，很幸运能免费体验到`百度自适应打点`、`百度多渠道分享`、`搜狐评论畅言`、`搜狐畅言打赏`，感谢博客灵魂`Jekyll`让笔者能轻松的使用`Markdown`撰写文章，感谢博客域名的引路人`阿里云`。 [李牧牧的博客](http://limumu.me) 

![](http://cdn.static.limumu.me/assets:post:img:2017061301.png)

##### 关于模版

我的博客模版是从作者 [Hux Blog](https://github.com/Huxpro/huxpro.github.io) Fork的，感谢Hux。

##### 修改了哪些东西

> 在作者框架基础上作了如下变化

- [x] 所有 开源工具库 改由 cdn.bootcss.com 获取
- [x] 所有 自定义资源文件 改由 七牛云存储 获取
- [x] 替换 多说评论插件 为 搜狐评论畅言
- [x] 替换 百度打点 为 百度自适应打点
- [x] 修改 package.json 同步提交到 GitHub.com 与 Coding.net ，解决 GitHub 被百度爬虫屏蔽问题
- [x] 添加 搜狐畅言打赏功能
- [x] 添加 百度多渠道分享
- [x] 去除了 Disqus、多说、Tag、Catalog、Google Analytics功能提升速度与体验

#####  核心文件结构说明

- [x] _config.yml 个人资料、基础配置
- [x] index.html 首页固定模版，百度统计
- [x] about.html 说明页固定模版，畅言评论插件、打赏功能、百度多渠道分享
- [x] _layouts/post.html 文章详情模版，畅言评论插件、打赏功能、百度多渠道分享
- [x] _posts/*.markdown 此目录文章自动编译为静态模版并按日期显示在首页

#####  支付宝、微信打赏

![](http://cdn.static.limumu.me/assets:post:img:2017061302.png)


#####  高速页面资源加载

![](http://cdn.static.limumu.me/assets:post:img:2017061303.png)


#####  全国网络访问测速

![](http://cdn.static.limumu.me/assets:post:img:2017061304.png)

#####  国际网络访问测速

![](http://cdn.static.limumu.me/assets:post:img:2017061305.png)


#####  百度爬虫收录情况

![](http://cdn.static.limumu.me/assets:post:img:2017061306.png)


# 十分钟倒计时开始

> `GitHub` 用于实际存放博客文件，由于`GitHub`在美国，访问速度相对缓慢，笔者后续会采用其他办法解决问题，现在先把账号建立起来，并打开GitPage功能。

[如何使用`GitHub`创建项目](http://blog.csdn.net/tao_627/article/details/51407391 "如何使用`GitHub`创建项目")  - 来源 CSDN

> `Jekyll` 是一个静态站点生成器，它会根据网页源码生成静态文件。它提供了模板、变量、插件等功能，所以实际上可以用来编写整个网站，对于非设计出生的笔者，选择 `Jekyll` 官方提供 或 `GitHub`开源作者提供的优雅模版就是不二选择，笔者 Fork Hux 的博客模版。

[Hux 的`Jekyll`模版](https://github.com/Huxpro/huxpro.github.io "Hux 的`Jekyll`模版")  - 来源 GitHub

[笔者博客在 `GitHub`的`Jekyll`模版](https://github.com/m18507308080/limumu.github.io "笔者博客在 `GitHub`的`Jekyll`模版")  - 来源 GitHub

> 大刀阔斧的删除文件

- [x] less 文件夹
- [x] portfolio 文件夹 
- [x] pwa 文件夹
- [x] tags.html 文件

> 毫不犹豫的迁移文件到七牛云存储

- [x] css文件夹
- [x] fonts文件夹
- [x] img 文件夹
- [x] js文件夹

> 修改几个代码文件资源引用路径为七牛云地址

- [x] _config.yml
- [x] 404.html
- [x] about.html
- [x] footer.html
- [x] head.html
- [x] offilne.html

![](http://cdn.static.limumu.me/assets:post:img:2017061307.png)

> 将修改后的文件提交至`GitHub`并将`CNAME`内容修改为`GitPage`提供的域名地址，如需要修改为自己的域名就还需要在域名提供商管理页将 `A纪录`修改为 `GitPage IP`地址，注意此时得到的`GitHub IP` 地址有能会变化，当出现访问不了博客的情况时，可以考虑是否是地址变了。

```
ping username.github.io // 得到IP地址
```

![](http://cdn.static.limumu.me/assets:post:img:2017061309.png)

> 由于 `GitHub`  屏蔽百度爬虫，所以百度收录不了博客文章，我们采用同时提交代码到`GitHub.com`与  `Coding.com`的办法让国内百度爬虫可以到`Coding.com`收录文章。

![](http://cdn.static.limumu.me/assets:post:img:2017061308.png)


# Q&A

> 问 照这样搭建需要多少费用？

答 不需要一分钱，每次写好文章后，提交代码博客自动更新。

> 问 有哪些需要注意的么？

答 目前只需要注意`GitHub`的地址会变化，假如变化了可以重新通过`Ping`获取地址并更新`A记录`

> 问 为什么使用`七牛云`和`畅言`？

答 七牛有免费的存储空间以及免费的CDN内容分发网络，畅言有相对成熟快速免费的评论与打赏功能。