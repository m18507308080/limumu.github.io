---
layout:     post
title:      "如何使用Docker安装数据库？"
subtitle:   ""
date:       2017-02-07 10:00:00
author:     "李牧牧"
header-img: "http://cdn.static.limumu.me/assets:img:home-bg.jpg"
header-mask: 0.1
catalog:    true
tags:
    - 阿里云
    - 混合云
---

> 本文发布于 [李牧牧的博客](http://limumu.me) 转载请保留链接 ;)



摘要：

> 下载数据库，配置数据库，主从配置，参数配置，地址设置，编码设置，每次有新数据库需要部署也是非常麻烦的，本文介绍如何用 Docker 完成这些任务



# 工欲利其事，必先利其器

> Docker MySQL 部署一句话

```
docker run --name mysql -e TZ=Asia/Shanghai -e MYSQL_ROOT_PASSWORD=Pass1234 -p 192.168.200.200:3306:3306 -d -v /app/mysql/192.168.200.200:/etc/mysql/conf.d -v /data/mysql/192.168.200.200:/var/lib/mysql mysql:5.6
```

> 将配置文件放入 `/app/mysql/192.168.200.200`

```
# The MySQL server

[mysqld]
skip-name-resolve
skip-external-locking
slave-skip-errors=all
#skip-grant-tables
#skip-name-resolve
#bind-address=127.0.0.1
max_connections=16384
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci
init_connect='SET NAMES utf8mb4'

[client]
default-character-set = utf8mb4
 
[mysql]
default-character-set = utf8mb4
```

# Q & A

> 问 要是自己搭建这样的系统，估计工作量多大？

答 企业根据自己需要，从头开始一个人一天可以基本部署完毕。

> 问 如何设计开发高并发用户数庞大的代码软件架构？

答 结合上面的文字再参考博文 [《如何设计开发高并发高可用的代码架构？》