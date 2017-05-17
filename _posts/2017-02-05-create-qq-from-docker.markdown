---
layout:     post
title:      "如何使用Docker部署QQ小秘书？"
subtitle:   ""
date:       2017-02-05 10:00:00
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

> 敲一行命令就能启动一个智能聊天机器人，Perl 和你都如此优雅. Enjoy!



# 工欲利其事，必先利其器

项目来源于 GitHub 上 Mojo-Webqq 的贡献，事先需要注册用来充当机器人的QQ号码

> Docker 安装方式

```
docker run -it  --env MOJO_WEBQQ_LOG_ENCODING=utf8 -p 80:5000 -v /tmp:/tmp sjdy521/mojo-webqq 
```

> 获取QQ群ID

```
http://部署机器人服务器IP/openqq/get_group_info
```

> 调用方式，如需发送中文消息，先将中文内容 URL ENCODE 后再填入消息体

```
curl -d "did=QQ群ID&content=消息英文内容" "http://部署机器人服务器IP/openqq/send_discuss_message" &
```

[ QQ机器人 GitHub 项目](https://github.com/sjdy521/Mojo-Webqq "QQ机器人 GitHub 项目")  - 来源 GitHub

[ URI Encoding 工具站 ](http://tool.chinaz.com/Tools/urlencode.aspx "URI Encoding 工具站 ")  - 来源 站长之家



# Q&A

> 问 要是自己搭建这样的系统，估计工作量多大？

答 企业根据自己需要，从头开始一个人两周可以基本部署完毕。

> 问 如何将公司内网测试环境与阿里云生产打通，并持续集成呢？

答 结合本文参考另一篇博文 [《如何零成本构建研发运维一体化？》](http://www.limumu.me/2017/02/18/create-devops-from-aliyun/ "如何零成本构建研发运维一体化？")

> 问 如何设计开发高并发用户数庞大的代码软件架构？

答 结合上面的文字再参考博文 [《如何设计开发高并发高可用的代码架构？》



