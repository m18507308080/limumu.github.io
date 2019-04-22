---
layout:     post
title:      "如何使用Docker安装Jenkins？"
subtitle:   ""
date:       2017-02-06 10:00:00
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

> Jenkins的主要目标是监控软件开发流程，快速显示问题。所以能保证开发人员以及相关人员省时省力提高开发效率。

![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705171115001.png)

# 工欲利其事，必先利其器


> Docker 一句话生成

```
docker run -e TZ=Asia/Shanghai -d --name jenkins -p 192.168.200.200:80:8080 -v /app/jenkins/192.168.200.200:/home/ -v /data/jenkins/192.168.200.200:/usr/local/etc/ venizeng/jenkins
```



# 扬长避短，知物善用

> 配置 Git

`Docker` 中`venizeng/jenkins` 的版本自带`Git`，如果想自行安装只需要在 `Jenkins` 所在系统手动安装 `Git` 配置好环境变量，然后在 `Git installations` 选项中将 `Path to Git executable` 填写为 git 即可。

![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705171650git.png)

> 配置 xCode 支持 IOS 打包编译

![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705171650xcode.png)

> 配置 Android-SDK 支持 Android 打包编译

![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705171650anzhuo.png)

> 配置 JDK 

`Docker` 中`venizeng/jenkins` 的版本自带 `JDK`，如果想自行安装只需要在 `Jenkins` 所在系统手动安装 `JDK` 配置好环境变量即可。

> 配置 Maven

将修改好的`Maven Setting.xml` 文件放入 `Jenkins` 所在系统目录中 `/usr/local/etc/setting.xml`，在 `Maven Configuration` 中 `File Path` 填写`Setting.xml` 文件绝对路径

![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705171650maven.png)

> 权限分配

如果想控制不同类型用户只能操作特定的项目，需要配置 `Configure Global Security` 与 `Manage and Assign Roles `即可。

![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705171650se1.png)

![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705171650se2.png)

![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:201705171650se3.png)

> 项目发包脚本参考

```
ssh root@192.168.200.6 "/usr/bin/rm -rf /backup/TWEEMEE-SIT-SCC-SERVICE/CURRENT/ & /usr/bin/mkdir -p /backup/TWEEMEE-SIT-SCC-SERVICE/CURRENT/"
scp /var/jenkins_home/workspace/TWEEMEE-SIT-SCC-SERVICE/target/*.war root@192.168.200.6:/backup/TWEEMEE-SIT-SCC-SERVICE/CURRENT/
ssh root@192.168.200.6 "/usr/bin/cp /backup/TWEEMEE-SIT-SCC-SERVICE/CURRENT/*.war /data/192.168.200.61/ROOT.war"
ssh root@192.168.200.6 "/usr/bin/sh /app/192.168.200.61/shutdown.sh"
ssh root@192.168.200.6 "/usr/bin/rm -rf /data/192.168.200.61/ROOT"
ssh root@192.168.200.6 "/usr/bin/sh /app/192.168.200.61/startup.sh"
ssh root@192.168.200.6 "/usr/bin/cp /backup/TWEEMEE-SIT-SCC-SERVICE/CURRENT/*.war /backup/TWEEMEE-SIT-SCC-SERVICE/"
ssh root@192.168.200.6 "/usr/bin/rm -rf /backup/TWEEMEE-SIT-SCC-SERVICE/CURRENT/"
```





# Q&A

> 问 要是自己搭建这样的系统，估计工作量多大？

答 企业根据自己需要，从头开始一个人两周可以基本部署完毕。

> 问 如何将公司内网测试环境与阿里云生产打通，并持续集成呢？

答 结合本文参考另一篇博文 [《如何零成本构建研发运维一体化？》](http://www.limumu.me/2017/02/18/create-devops-from-aliyun/ "如何零成本构建研发运维一体化？")

> 问 如何设计开发高并发用户数庞大的代码软件架构？

答 结合上面的文字再参考博文 [《如何设计开发高并发高可用的代码架构？》

