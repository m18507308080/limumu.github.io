---
layout:     post
title:      "如何部署阿里云MQ消息队列平台？"
subtitle:   "《推蜜》官方互动养成APP，借力《阿里云》从零到壹的演变"
date:       2017-01-06 10:00:00
author:     "李牧牧"
header-img: "http://onb688cva.bkt.clouddn.com/assets:img:home-bg.png"
header-mask: 0.1
catalog:    true
tags:
    - 阿里云
    - 混合云
---

> 本文发布于 [李牧牧的博客](http://limumu.me) 转载请保留链接 ;)

  



提示：

> 阿里云管理操作界面样式总会变化，但思路不会变，如果您登录的操作界面与文章示例图片不太一致，请谅解。



### 如何在ECS上搭建ActiveMQ？

> 官网下载ActiveMQ

```
# wget http://archive.apache.org/dist/activemq/apache-activemq/5.9.0/apache-activemq-5.9.0-bin.tar.gz
正在解析主机 archive.apache.org (archive.apache.org)... 163.172.17.199
正在连接 archive.apache.org (archive.apache.org)|163.172.17.199|:80... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度：55438331 (53M) [application/x-gzip]
正在保存至: “apache-activemq-5.9.0-bin.tar.gz”

100%[======================>] 55,438,331  1.61MB/s 用时 14m 11s

已保存 “apache-activemq-5.9.0-bin.tar.gz” [55438331/55438331])
```

[ActiveMQ官网下载页面](http://activemq.apache.org/download-archives.html "ActiveMQ官网下载页面")  - 来源 ActiveMQ官网

> 安装 ActiveMQ

```
# tar xzvf apache-activemq-5.9.0-bin.tar.gz
# cd apache-activemq-5.9.0
# cp -r apache-activemq-5.9.0 /app
```

> 配置 ActiveMQ

更改管理后台访问端口

```
<bean id="jettyPort" class="org.apache.activemq.web.WebConsolePort" init-method="start">
        <!-- the default port number for the web console -->
        <property name="port" value="8161"/>
</bean>
```

更改接口调用端口

```
<transportConnector name="openwire" uri="tcp://0.0.0.0:61616?maximumConnections=1000&amp;wireFormat.maxFrameSize=104857600"/>
```



> 启动 ActiveMQ 服务

```
#cd /app/apache-activemq-5.9.0/bin
# ./activemq-admin start &
```












