---
layout:     post
title:      "如何搭建阿里云主从RDS数据库并配置安全规则？"
subtitle:   "《推蜜》官方互动养成APP，借力《阿里云》从零到壹的演变"
date:       2017-01-26 10:00:00
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


### 如何选择RDS数据库配置

RDS是阿里云提供的关系型数据库服务，是将直接运行于物理服务器上的数据库实例租给用户，通过对硬件资源的独占分配避开了云服务器硬盘IO共享带来的性能问题。RDS提供给用户单机版与高可用版两种选择，高可用版采用主备架构（备用实例正常情况下对用户不可见），两个实例位于不同服务器，自动同步数据。主实例不可用时，系统会自动将数据库连接切换至备用实例。切换是分钟级别，而且不需要人工介入，全部由系统自动完成，应用系统也无需任何变更。这种架构足以满足90% 用户的高可用需求。



> RDS 1核1G基础配置：单机版83元每月，高可用版132元每月

![](http://pnbk67adq.bkt.clouddn.com/assets:post:img:20170405_rds_single.png)



![](http://pnbk67adq.bkt.clouddn.com/assets:post:img:20170405_rds_backup.png)













