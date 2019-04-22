---
layout:     post
title:      "如何给服务器安装操作系统？"
subtitle:   "Linux & Docker & CentOS 如何和谐共存"
date:       2017-02-12 10:00:00
author:     "李牧牧"
header-img: "http://pqcjj2s3l.bkt.clouddn.com/assets:img:home-bg.jpg"
header-mask: 0.1
catalog:    true
tags:
    - 阿里云
    - 混合云
---

> 本文发布于 [李牧牧的博客](http://limumu.me) 转载请保留链接 ;)



摘要：

> 把大象装进冰箱里只需要三步：打开冰箱、把大象塞进去、把冰箱门关上，安装操作系统也是如此，差别只是：选择什么样的冰箱、怎么优雅的塞进去、如何制定使用规则。

 ![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705161323000.jpg)

我们选择 CentOS Linux 作为硬件服务器操作系统，并且部署 Docker 实现容器虚拟化，在这之前，先关注如下几篇文章：

- [x] [Linux 作为服务器操作系统的优势是什么？](https://www.zhihu.com/question/19738282 "Linux 作为服务器操作系统的优势是什么？")  - 来源 知乎

- [x] [为什么国内互联网公司喜欢用 Centos？](https://www.zhihu.com/question/22814858 "为什么国内互联网公司喜欢用 Centos ？")  - 来源 知乎

- [x] [为什么选择 Docker 实现容器虚拟化？](https://www.zhihu.com/question/22871084 "为什么选择 Docker 实现容器虚拟化？")  - 来源 知乎





# 工欲利其事，必先利其器

想必童鞋们首次接触到的操作系统都是 `Microsoft Windows` 系列，注重用户体验的微软公司拥有大量的忠实粉丝，大量的用户群体与社区让` Windows` 操作系统安装方式多种多样：光盘安装、`ISO`镜像安装、`GHOST`一键还原、U盘安装，其中最方便快速的方式莫过于 U盘安装 ，`Linux` 也可以通过 U 盘安装的方式部署操作系统，接下来我们来看看如何操作。



- [x] 物理计算机

给物理计算机挑选配置主要看这台服务器未来的业务范围与大小，假如用于安装关系型数据库、Key-Value数据库、分布式文件存储的数据库，类似这样的作为数据中心使用的话，建议配置着重点在硬盘大小与读写读写可靠性，内存大小与`CPU`，如果用于 `Java` 后端应用、运营平台，那么配置着重点在内存大小与`CPU`，另外如果公司业务线不长，只是一个小型的移动应用开发企业，普通的小型工作站就完全可以满足需求，费用甚至低于普通PC个人电脑。

- [x] 4G 空间以上 U盘

正式发行版 `Linux` 镜像一般在 3-4G ，如果空间不足的话就无法使用 U盘 安装操作系统。

- [x] `CentOS 7` 系统镜像文件

 [阿里云开源镜像站](http://mirrors.aliyun.com/centos/ "阿里云开源镜像站")  - 来源 阿里云

- [x] U盘启动盘制作工具

 [老毛桃U盘启动盘制作工具](http://www.laomaotao.org/ "老毛桃U盘启动盘制作工具")  - 来源 老毛桃



# 扬长避短，知物善用

通常物理服务器购买来就自带了操作系统，这就需要我们将自带的操作系统以及之前的分区方案一并删除，我们需要借助《老毛桃U盘启动盘制作工具》进行删除操作，当然首先需要在自己的个人电脑中安装此工具，然后插入U盘，启老毛桃U盘制作工具软件，在操作界面选择需要操作的 U盘，其他选择默认即可，然后点击一键制作功能。


![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705161323001.jpg)

![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705161323002.jpg)

到这里我们成功的安装了U盘工具，一般称它为U盘PE工具系统，有了它就可以删除服务器自带操作系统和分区的工具了，接下来需要将服务器的 `BIOS` 设置为开机时读取 U盘数据，每台品牌计算机都有默认的快捷设置按钮，只需在开机时不停的敲入对应按钮就可以直接进入U盘PE工具系统。

 [各品牌电脑开机启动菜单快捷键](http://blog.sina.com.cn/s/blog_52330bed01010yw9.html "各品牌电脑开机启动菜单快捷键")  - 来源 lxing20

 ![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705161323003.jpg)

 

>  因为每个版本的老毛桃工具界面会有变化，只要选择类似 进入PE系统的选项敲回车即可，上图选择 02 选项。


 ![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705161323006.jpg)

 ![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705161323007.jpg)

上图中将 `HD0` 硬盘中的所有主分区与扩张分区全部删除，图中删除本地磁盘C与扩张分区，到这里已经成功将服务器自带的操作系统与分区抹除，接下来就可以安装 `CentOS` 了，首先回到个人PC电脑端，将 插在服务器的U盘插入到 PC个人电脑中，打开老毛桃工具，选择 `ISO`模式，选择插入的U盘，选择下载好的`CentOS`镜像文件，点击制作并确认格式化模式对话框。

  ![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705161323008.jpg)

  ![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705161323009.jpg)

写入的过程有点缓慢，`USB 3.0` 的U盘写入速度会快一些，这里需要注意几个问题：

1. U盘读写质量会影响到成功率，劣质的U盘会导致写入虽然提示成功，但是系统依然读取不了。
2. 写入成功后，需要修改U盘名称，因为当`BIOS`从U盘启动时会通过 `GRUB` 命令识别U盘名称，一旦出现了空格、特殊字符就会出现一直停留在启动界面的情况，所以需要修改U盘名称， 越简单越好大小写区分，比如取名：`USB`。
3. 通常当 U盘 插入到服务器时，启动服务器并通过启动项快捷键让服务器从U盘启动到安装界面，这个过程是很快的，假如一直停留在加载界面，说明 `Grub` 找不到 U盘 ，需要修改 U盘的名称为 （方法2）中取名的`USB`，回车再次加载启动，就可以了。

 [为什么 USB 3.0 U盘读写会快？](https://www.zhihu.com/question/28081066 "为什么 USB 3.0 U盘读写会快？")  - 来源 知乎

如果一切正常，开始安装操作系统，同样的将U盘插入服务器，并根据品牌选择启动项快捷键，进入到 `CentOS` 安装界面。

  ![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705161323010.jpg)

 [CentOS 图形化安装教程](http://www.centoscn.com/image-text/setup/2014/0724/3342.html "CentOS 图形化安装教程")  - 来源 CentOSCN

安装过程注意几点

- [x] 选择正确的时区与编码方式
- [x] 选择最小安装方式，服务器不要安装图形化界面
- [x] 最大化配置根分区空间



# 约定优于配置

有次笔者在听盛大的运维来公司讲课时讲到：“很多企业的服务器硬盘里，零零散散各种文件散落在各种角落，以至于由于错乱的文件与文件夹层级关系，导致出一些生产事故，所以一定要提前约定好。”，其实不管是服务器硬盘，还是程序代码，约定优于配置真的是简单而又不失灵活性的好方法。

```
  ***Wrrning***
  Authorised access only
  This system is the property of www.domain.com
  Disconnect IMMEDIATELY if you are not an authorized user!
  Your IP has been IDS records Don't damage any files!

  ***TIPS***
  Application in app folder /app
  Backup in backup folder /backup
  Soft in soft folder /soft
  Log in data folder /data
```

这是笔者在 /etc/motd 文件中写入的提醒内容

- 所有应用程序放在 /app 
- 所有备份文件放在 /backup
- 所有软件文件放在 /soft
- 所有日志文件放在 /data

日志文件所在的文件夹，每月将日志数据用 `Shell` 脚本上传到 `OSS` 分片存储文件夹。

[如何使用 Linux Shell 上传文件到 OSS云存储？ ](https://bbs.aliyun.com/simple/t233456.html "如何使用 Linux Shell 上传文件到 OSS云存储？ ")  - 来源 阿里云

优化服务器参数，将更改默认`SSH`端口号。

[如何优化服务器参数提高并发能力？](http://www.ha97.com/4396.html "如何优化服务器参数提高并发能力？")  - 来源 博客教主





# Q&A
> 问 要是自己搭建这样的系统，估计工作量多大？

答 企业根据自己需要，从头开始一个人一天可以基本部署完毕。

> 问 如何将公司内网测试环境与阿里云生产打通，并持续集成呢？

答 结合本文参考另一篇博文 [《如何零成本构建研发运维一体化？》](http://www.limumu.me/2017/02/18/create-devops-from-aliyun/ "如何零成本构建研发运维一体化？")

> 问 如何设计开发高并发用户数庞大的代码软件架构？

答 结合上面的文字再参考博文 [《如何设计开发高并发高可用的代码架构？》](http://www.limumu.me/2017/02/16/create-java-from-aliyun/ "如何设计开发高并发高可用的代码架构？")