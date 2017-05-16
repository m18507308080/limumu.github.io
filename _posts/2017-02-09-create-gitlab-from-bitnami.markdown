---
layout:     post
title:      "如何一键部署GitLab代码版本管理平台？"
subtitle:   ""
date:       2017-02-09 10:00:00
author:     "李牧牧"
header-img: "http://onb688cva.bkt.clouddn.com/assets:img:home-bg.jpg"
header-mask: 0.1
catalog:    true
tags:
    - 阿里云
    - 混合云
---

> 本文发布于 [李牧牧的博客](http://limumu.me) 转载请保留链接 ;)



摘要：

> `GitLab` 是一个用于仓库管理系统的开源项目。使用`Git`作为代码管理工具，并在此基础上搭建起来的 `Web`服务，`GitLab`是基于`Ruby on Rails`的，安装和配置非常麻烦，不过 `BitNami` 帮我们解决了问题。



# 工欲利其事，必先利其器


![](http://onb688cva.bkt.clouddn.com/assets:post:img:201705161323015.jpg)


> 什么是 `BitNami` ？

`BitNami`是一个开源项目，该项目产生的开源软件包括安装 Web应用程序和解决方案堆栈，以及虚拟设备，意思就是许多开源软件互相依赖的库非常多，安装起来各种不方便，`BitNami` 帮用户简化安装的过程，集成为一个安装程序，只需找到对应操作系统的安装版本直接运行就可以顺利安装，它不但支持软件包安装方式，也支持Docker安装。

[ BitNami GitLab 官方下载地址 ](https://bitnami.com/stack/gitlab" BitNami GitLab 官方下载地址)  - 来源 BitNami

[ 如何使用 BitNami 安装 Gitlab ？ ](http://www.cnblogs.com/wintersun/p/3930900.html"  如何使用 BitNami 安装 Gitlab ？)  - 来源 CNBlog

注意，安装`GitLab`内存至少需要`4G`才能安装成功。



# Q&A

> 问 要是自己搭建这样的系统，估计工作量多大？

答 企业根据自己需要，从头开始一个人一天可以基本部署完毕。

> 问 如何将公司内网测试环境与阿里云生产打通，并持续集成呢？

答 结合本文参考另一篇博文 [《如何零成本构建研发运维一体化？》](http://www.limumu.me/2017/02/18/create-devops-from-aliyun/ "如何零成本构建研发运维一体化？")

> 问 如何设计开发高并发用户数庞大的代码软件架构？

答 结合上面的文字再参考博文 [《如何设计开发高并发高可用的代码架构？》