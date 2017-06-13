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

> 笔者的博客就是采用本文中的方法搭建而成 [李牧牧的博客](http://limumu.me) 

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