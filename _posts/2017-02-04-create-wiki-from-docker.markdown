---
layout:     post
title:      "如何使用Docker部署Wiki文档协助系统？"
subtitle:   ""
date:       2017-02-04 10:00:00
author:     "李牧牧"
header-img: "http://pqcjj2s3l.bkt.clouddn.com/assets:img:home-bg.jpg"
header-mask: 0.1
catalog:    true
tags:
    - 阿里云
---

> 本文发布于 [李牧牧的博客](http://limumu.me) 转载请保留链接 ;)



摘要：

> **DokuWiki**是一个开源wiki引擎程序，运行于PHP环境下。Doku Wiki 程序小巧而功能强大、灵活，适合中小团队和个人网站知识库的管理。

![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705171650wiki.jpeg)

![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705171651wiki.jpeg)

![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705171661wiki.jpeg)

![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705171662wiki.jpeg)


# 工欲利其事，必先利其器

> Docker 一句话生成 Wiki

```
docker run -it -d -p 192.168.200.114:80:80 —name 192.168.200.114 -v /data/wiki/192.168.200.114:/var/www istepanov/dokuwik
```



Wiki的关键是编写文档者如何写，阅读文档者知道去哪读，所以需要事先约定好。



# Q&A

> 问 要是自己搭建这样的系统，估计工作量多大？

答 企业根据自己需要，从头开始一个人一天可以基本部署完毕。

> 问 如何将公司内网测试环境与阿里云生产打通，并持续集成呢？

答 结合本文参考另一篇博文 [《如何零成本构建研发运维一体化？》](http://www.limumu.me/2017/02/18/create-devops-from-aliyun/ "如何零成本构建研发运维一体化？")

> 问 如何设计开发高并发用户数庞大的代码软件架构？

答 结合上面的文字再参考博文 [《如何设计开发高并发高可用的代码架构？》

