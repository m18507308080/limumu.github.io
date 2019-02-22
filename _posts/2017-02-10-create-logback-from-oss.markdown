---
layout:     post
title:      "如何借助阿里云OSS备份全环境日志？"
subtitle:   ""
date:       2017-02-10 10:00:00
author:     "李牧牧"
header-img: "http://pnbk67adq.bkt.clouddn.com/assets:img:home-bg.jpg"
header-mask: 0.1
catalog:    true
tags:
    - 阿里云
    - 混合云
---

> 本文发布于 [李牧牧的博客](http://limumu.me) 转载请保留链接 ;)



摘要 

> 当应用服务越来越多时，日志随之也水涨船高，如何统一的备份与查看日志文件就成了必须解决的问题，本文介绍如何巧用阿里云OSS工具做到全局备份日志与查询。



# 工欲利其事，必先利其器

`OSSFS` 能让您在`Linux`系统中把`OSS Bucket` 挂载到本地文件系统中，您能够便捷地通过本地文件系统操作`OSS`上的对象，实现数据的共享，`OSSFS` 基于 `S3FS` 构建，具有 S3FS 的全部功能，主要功能包括：

- 支持POSIX 文件系统的大部分功能，包括文件读写，目录，链接操作，权限，uid/gid，以及扩展属性（extended attributes）
- 通过OSS 的multipart 功能上传大文件。
- MD5 校验保证数据完整性。

> 下载操作系统对应的发行软件版本

 [如何安装OSSFS？](https://help.aliyun.com/document_detail/32196.html "如何安装OSSFS？")  - 来源 阿里云

> 通过 OSS 管理工具查看日志

 [ OSS 管理工具客户端 ](https://market.aliyun.com/store/55050-2.html?spm=5176.mktshop55050.4.1.ip9G0X "OSS 管理工具客户端 ")  - 来源 驻云科技

![](http://pnbk67adq.bkt.clouddn.com/assets:post:img:201705161323014.jpg)



# Q&A

> 问 要是自己搭建这样的系统，估计工作量多大？

答 企业根据自己需要，从头开始一个人一天可以基本部署完毕。

> 问 如何将公司内网测试环境与阿里云生产打通，并持续集成呢？

答 结合本文参考另一篇博文 [《如何零成本构建研发运维一体化？》](http://www.limumu.me/2017/02/18/create-devops-from-aliyun/ "如何零成本构建研发运维一体化？")

> 问 如何设计开发高并发用户数庞大的代码软件架构？

答 结合上面的文字再参考博文 [《如何设计开发高并发高可用的代码架构？》