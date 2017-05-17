---
layout:     post
title:      "如何使用Docker安装Jenkins？"
subtitle:   ""
date:       2017-02-06 10:00:00
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

> Jenkins的主要目标是监控软件开发流程，快速显示问题。所以能保证开发人员以及相关人员省时省力提高开发效率。

![](http://onb688cva.bkt.clouddn.com/assets:post:img:201705171115001.png)

# 工欲利其事，必先利其器


> Docker 一句话生成

```
docker run -e TZ=Asia/Shanghai -d --name jenkins -p 192.168.200.200:80:8080 -v /app/jenkins/192.168.200.200:/home/ -v /data/jenkins/192.168.200.200:/usr/local/etc/ venizeng/jenkins
```







