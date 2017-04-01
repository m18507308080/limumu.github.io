---
layout:     post
title:      "如何配置阿里云SLB负载均衡并连通服务器？"
subtitle:   "《推蜜》官方互动养成APP，借力《阿里云》从零到壹的演变"
date:       2017-01-28 10:00:00
author:     "李牧牧"
header-img: "http://onb688cva.bkt.clouddn.com/assets:img:home-bg.jpg"
header-mask: 0.1
catalog:    true
tags:
    - 阿里云
    - 混合云
---

> 本文发布于 [李牧牧的博客](http://limumu.me) 转载请保留链接 ;)

  



提示：

> 阿里云管理操作界面样式总会变化，但思路不会变，如果您登录的操作界面与文章示例图片不太一致，请谅解。





### 如何选择SLB负载均衡配置？

- 阿里云提供不同地域的负载均衡服务，选择ECS服务器同样的服务区。
- 如果业务用户访问量起伏较大，选择按流量计费，否则选择固定带宽。
- 配置负载均衡监听器时，必须勾选健康检查项，配置协议为HTTP。







