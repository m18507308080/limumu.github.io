---
layout:     post
title:      "如何部署阿里云OSS分片存储系统并配置专属域名？"
subtitle:   "《推蜜》官方互动养成APP，借力《阿里云》从零到壹的演变"
date:       2017-01-16 10:00:00
author:     "李牧牧"
header-img: "http://pnbk67adq.bkt.clouddn.com/assets:img:home-bg.jpg"
header-mask: 0.1
catalog:    true
tags:
    - 阿里云
    - 混合云
---

> 本文发布于 [李牧牧的博客](http://limumu.me) 转载请保留链接 ;)

  



提示：

> 阿里云管理操作界面样式总会变化，但思路不会变，如果您登录的操作界面与文章示例图片不太一致，请谅解。



# 如何配置 OSS 云存储？

OSS Bucket是全网唯一的，不能与其它用户的Bucket同名。

OSS针对Bucket ACL提供三种权限

私有：对object的所有访问操作需要进行身份验证，需要SDK签名访问。
公共读：对object写操作需要进行身份验证；可以对object进行匿名读。
公共读写：所有人都可以对object进行读写操作。

OSS支持日志存储，日志文件可以存储在自建的Bucket中。

OSS跨域设置，将GET*，*POST*，*PUT*，*DELETE*，*HEAD全部放开。

![](http://pnbk67adq.bkt.clouddn.com/assets:post:img:20170405_create_oss.png)

![](http://pnbk67adq.bkt.clouddn.com/assets:post:img:20170405_create_oss_plugin.png)



# Q & A

> 问 要是自己搭建这样的系统，估计工作量多大？

答 企业根据自己需要，从头开始一个人两周可以基本部署完毕。

> 问 如何设计开发高并发用户数庞大的代码软件架构？

答 结合上面的文字再参考博文 [《如何设计开发高并发高可用的代码架构？》










