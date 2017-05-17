---
layout:     post
title:      "如何快速搭建Maven私服？"
subtitle:   ""
date:       2017-02-08 10:00:00
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

> 公司开发项目的过程中，会使用一些开源框架、第三方的工具等等，这些都是以`jar`包的方式被项目所引用，并且有些`jar`包还会依赖其他的`jar`包，我们同样需要添加到项目中，所有这些相关的`jar`包都会作为项目的依赖。

 ![](http://onb688cva.bkt.clouddn.com/assets:post:img:201705171115000.png)



# 工欲利其事，必先利其器

从`Maven`官网下载的安装包，默认配置仓库地址为是`http://repo1.maven.org/maven2` ，但是默认的中央仓库在国外，速度有点慢，所以产生了一些第三份的仓库提供方，我们罗列市面上一些网络私服。

- [x] http://mvnrepository.com/                      

- [x] http://maven.oschina.net/content/groups/public/

- [x] http://maven.aliyun.com/nexus/

- [x] http://repository.jboss.org/nexus/content/groups/public     

- [x] http://mirrors.ibiblio.org/pub/mirrors/maven2/    

- [x] http://maven.net.cn/content/groups/public/          


以上市面的仓库，有的速度慢，有的已经停止服务，有的不太好上传自己的 `jar` ，另外有些企业需要对自己的 `jar` 设置私有化，也满足不了需求，这就需要自己搭建私服仓库。



# 扬长避短，知物善用

部署`Maven Nexus`私服 ，可以直接从官网下载对应操作系统的安装包，也可以通过`Docker`一句话安装。

> 官网安装包部署 `Nexus`

`Sonatype`官网下载安装包，`Linux`版的无需安装，直接解压即可，然后进入bin目录下,运行./nexus start，启动服务，在地址栏里输入服务IP地址和8081端口就可以打开用户界面，点Sign In登录管理页面，默认用户名密码是admin和admin123，在`Repositories`页面里显示着，默认已经创建了5个仓库（2个为group），直接可以拿来用，无需再自行创建仓库。

 [ Sonatype Nuxus 官网下载 ](https://www.sonatype.com/download-oss-sonatype "Sonatype Nuxus 官网下载 ")  - 来源 Sonatype



> `Docker` 一句话安装

```
docker run -e TZ=Asia/Shanghai -it -d -p 192.168.200.200:80:8081 --name nexus sonatype/nexus
```



# 约定优于配置

本地私服配置好后，需要修改开发机 Maven 配置文件，告诉 Maven 从本地私服 `pull jar` 包

> 安装 `Maven` 环境

`Maven` 下载完毕后需要配置环境变量，然后修改 安装目录下 `conf/settings.xml` 

```
<repositories>
	<repository>
		<id>nexus</id>
		<url>http://maven.tweemee.com/content/groups/public/</url>
		<releases> <enabled>true</enabled> </releases>
		<snapshots> <enabled>true</enabled> </snapshots>
	</repository>		
</repositories>
```

 [ `Maven` 官网下载 ](http://maven.apache.org/download.cgi " Maven 官网下载  ")  - 来源 `Maven`



# Q & A

> 问 要是自己搭建这样的系统，估计工作量多大？

答 企业根据自己需要，从头开始一个人一天可以基本部署完毕。

> 问 如何设计开发高并发用户数庞大的代码软件架构？

答 结合上面的文字再参考博文 [《如何设计开发高并发高可用的代码架构？》