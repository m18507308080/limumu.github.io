---
layout:     post
title:      "如何零成本构建研发运维一体化？"
subtitle:   "《推蜜》《蜜蜂少女队》官方互动养成APP，借力《阿里云》从零到壹的演变"
date:       2017-02-18 10:00:00
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

> 随着公司业务的不断迅速增长，使得管理 IT 基础设施需求变得更为艰难。初创企业或小微互联网公司的程序员往往开发运维两兼职，那么如何简单有效的搭建整套自动化运维监控系统变的十分重要。



# 知己知彼，百战不殆

![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:2017041801_devops.png?imageView2/0/q/75|watermark/2/text/5p2O54mn54mnIGxpbXVtdS5tZQ==/font/5b6u6L2v6ZuF6buR/fontsize/520/fill/IzAwMDAwMA==/dissolve/100/gravity/SouthEast/dx/10/dy/10|imageslim)
***公司运维架构资源分配图***  *图片来源: 李牧牧博客* 

我们窥探一只互联网小团队他们的运维系统功能清单

- [x] 配置网络设备和服务器
- [x] 新虚拟机的配置
- [x] 应用程序部署
- [x] 收集和聚合的日志
- [x] 性能监视服务、网络和应用程序
- [x] 服务器异常报警和服务可用性监控

想要完全部署以上功能，如果不使用正确的工具集来执行这些任务将会是一件即费时又费钱的事。某些工具需要巨大的投资，而有一些却很容易获取，因为它们是开源。你可以进行一个简单的成本效益分析, 然后选择一组工具，帮助你解决当前应用场景下遇到的问题。



# 小步快跑＋快速迭代

> 传统软件企业的软件产品从无到有流程相对繁琐，对于需要快速开发迭代的初创互联网企业来说，时间线拉得有点太长。

![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:2017041705_aliyun.png)



> 往往一家互联网小团队会采用如下方式

![](http://pqcjj2s3l.bkt.clouddn.com/assets:post:img:2017041706_aliyun.png)



> 预备期

产品经理跟需求方沟通，了解要平台、功能、产品设计的需求、时长、预算等等，只有了解客户的详细需求才能做出开发方案，提交方案后需要找前端与后端开发、测试人员探讨方案可行性，包括功能开发的难度、实际开发的费用以及时间，接着项目各个组开始讨论，UI 设计针对产品开展设计 UI 界面跟 UE ，最后将所有文档上传共享到公司文档系统中。



> 孵化期

相关研发组长根据产品需求文档进行评估提出测评、预发跟正式发布时间，前后端研发根据业务松紧程度安排晨会、每周进度会议，直到项目顺利进入测试阶段，然后由测试专员针对 App 进行多机型内容测试、性能测试、功能测试、视觉测试并将问题提交到 Bug 系统让接口研发人员调试修复，确认没有BUG后开始走验收流程，很多大型互联网企业的验收流程会有（DEV、SIT、UAT、QAS、PRE、PRD），小团队通常会缩短为（DEV、SIT、QAS、PRD）。



> 新生期

上线需要申请成为公司开发者并上传真实有效各项材料，除了 App Store 外，国内多个安卓市场都需要单独申请与上传合法材料，一般苹果的 App Store 审核大概需要一个星期，安卓审核在 3 天左右，所以 App 开发测试一定要提前半个月完成，给长线审核预留一定的时间，如需要微信用户下载 App ，需要单独注册腾讯应用宝，到此 App 才算上线成功提供给用户下载使用。



# 开始搭建全链路服务

> 给计算机安装操作系统

给公司内部使用的服务器其实没有高低贵贱之分，合理利用服务器资源，小团队一般不会配备专业的全职运维，那么选择硬件服务器提供商时需要着重于售后服务，往往品牌服务器供应商的售后都有保障。创业团队刚开始不必考虑硬件服务器是购买刀片机还是塔式机，其实单台工作站电脑就完全可以满足公司内部日常工作，线上生产服务应该交给云服务提供商，如果公司除了移动应用业务线，还有公司内部管理系统业务线，笔者建议购买三台工作站分别处理移动端全线业务、企业内部系统业务、数据中心服务器，之所以独立出把于数据相关的服务独立出来也是为了结构清晰方便管理与监控。如果条件允许的话一定要给服务器配备 UPS 电源，不要太依赖硬盘。

*** 总结 *** 

- [x] 选择硬件服务器关键是售后要靠谱
- [x] 购买普通工组站电脑就够了（ 32G 内存 1T 硬盘无独显）
- [x] 数据中心与业务线各自独立使用物理服务器
- [x] 给服务器配备 UPS 应急电源

[如何给服务器安装操作系统？](http://www.limumu.me/2017/02/12/create-os-from-server/ "如何给服务器安装操作系统？")  - 来源 李牧牧博客




> 让应用容器化

实际工作中，往往需要在同一台物理计算机中安装多个应用服务，为了服务之间网络地址与端口不相互冲突，会在物理机安装多个虚拟操作系统才解决问题。

市面上虚拟化主流工具对比

- [ ] KVM           对于研发人员上手难度相对较高，社区成熟资料齐全
- [ ] Vmware        CPU与内存的占用相对较大，必须先安装操作系统再安装应用软件
- [ ] VirtualBox    CPU与内存的占用相对较大，作用于服务器有点浪费资源
- [x] Docker        应用容器引擎，可移植性好保障线上线下环境一致性，操作简单。


[如何部署分布式Docker容器服务？](http://www.limumu.me/2017/02/11/create-docker-from-os/ "如何部署分布式Docker容器服务？")  - 来源 李牧牧博客




> 日志 与 备份 兼得

当业务服务慢慢增多时，如何合理安排好日志文件与应用版本包备份存放位置变得尤为重要，如果日志业务量大小还不需要（ElasticSearch＋LogStash＋Kibana）采集、清洗、分析日志数据的话，如何简单有效的将多台物理机的各种环境日志统一管理备份起来。

[如何借助阿里云OSS备份全环境日志？](http://www.limumu.me/2017/02/10/create-logback-from-oss/ "如何借助阿里云OSS备份全环境日志？")  - 来源 李牧牧博客




> 代码的版本控制

研发工程师每天写的代码不单单是劳动成果，并且还是公司价值的组成部分。公司采用哪种代码版本管理平台原则上要满足几个条件，网络稳定性、数据安全性、对于创业团队成本控制也很有必要。

市面上代码版本管理主流平台对比

- [ ] Github       国内访问过于缓慢，项目私有化需要收费
- [ ] Coding       国内访问过于缓慢
- [ ] OSChina      业界良心的代码版本在线管理平台
- [x] GitLab       开源免费支持公司内部本地化安装

[如何一键部署GitLab代码版本管理平台？](http://www.limumu.me/2017/02/09/create-gitlab-from-bitnami/ "如何一键部署GitLab代码版本管理平台？")  - 来源 李牧牧博客



> 私有的项目库

世上的开源项目多如牛毛，很多开源项目的代码并不能直接复用在自己公司的项目中，有的研发工程会自己研发工具，有的会将开源项目或者开源工具根据公司业务稍作修改，让公司内部开发更有效率，但像这样的改动是不好上传到公网服务器给大家共用的，那么就需要公司自己拥有一套项目库管理私服平台。

[如何快速搭建Maven私服？](http://www.limumu.me/2017/02/08/create-maven-from-docker/ "如何快速搭建Maven私服？")  - 来源 李牧牧博客



> 一句话生成可用中间件

不管是移动应用后端架构还是传统软件项目，缓存系统、队列系统、主从数据库都是让产品更优秀的必须品，而每次需要新增这样的服务时都需要经历中间价软件的下载、安装、配置、调试的过程，如何才能有效率的快速搭建呢。

[如何使用Docker安装数据库？](http://www.limumu.me/2017/02/07/create-mysql-from-docker/ "如何使用Docker安装数据库？")  - 来源 李牧牧博客

[如何使用Docker安装Redis缓存？](http://www.limumu.me/2017/01/18/create-redis-from-aliyun/ "如何使用Docker安装Redis缓存？")  - 来源 李牧牧博客

[如何使用Docker安装ActiveMQ队列？](http://www.limumu.me/2017/01/06/create-mq-from-aliyun.markdown/ "如何使用Docker安装ActiveMQ队列？")  - 来源 李牧牧博客



> 有请发包总管

后端数据服务项目总是项目的重头戏，前后端业务线长自然项目就多，并且每个项目都有开发环境、测试环境、预生产环境、生产环境，如果将开发兼运维从命令行中解救出来，最低限度的避免出错，这就需要搭建一套自动化持续构建发包系统。

[如何使用Docker安装Jenkins？](http://www.limumu.me/2017/02/06/create-jenkins-from-docker/ "如何使用Docker安装Jenkins？")  - 来源 李牧牧博客




> 通知小秘书

当项目迭代版本验收时，总需要将项目发布到对应的环境上，此时测试有可能正在工作，突然就无响应了，虽然自动化持续构建发包系统有邮件通知，但往往不太及时并且有的测试还不定会看到。另外到项目线上环境出现大的事故时如果及时提醒团队人员及时修复呢。可以利用 GitHub 上的一个项目，它会创造 QQ 聊天机器人，通过接口调用来完成发包消息与异常消息及时提醒服务。 

[如何使用Docker部署QQ小秘书？](http://www.limumu.me/2017/02/05/create-qq-from-docker/ "如何使用Docker部署QQ小秘书？")  - 来源 李牧牧博客



> 协作知识文档

在实际工作中，当产品经理提交产品文档并约定好进测日期时，后端工程师第一件事出了分配工作任务外，就是将业务转换为接口文档，提供挡板数据，让前端可以同步开发从而不耽误开发进度，那么搭建一套Wiki文档系统尤为重要。

[如何使用Docker部署Wiki文档协助系统？](http://www.limumu.me/2017/02/04/create-wiki-from-docker/ "如何使用Docker部署Wiki文档协助系统")  - 来源 李牧牧博客



> 测试员的利器

产品开始验收，每当有 Bug 出现，测试人员如果将问题描述给开发并控制 Bug 进度，测试组长如何统计 测试工作 KPI，那么搭建功能完善的产品Bug跟踪系统必不可少。

[如何使用Docker搭建Jira产品Bug跟踪系统？](http://www.limumu.me/2017/02/03/create-jira-from-docker/ "如何使用Docker搭建Jira产品Bug跟踪系统？")  - 来源 李牧牧博客



> 无止尽的报表

数据报表是企业运营与营销团队的利器，不定期的各种报表需求非常多，如果每次都经历分析需求、设计界面、画页面、写代码、填充数据、测试、发包，往往会浪费很多时间，耽误市场部工作效率，那么对于小团队来说，部署一套开源免费、稳定方便的报表系统尤其重要。

[如何使用Docker搭建ReportServer报表系统？](http://www.limumu.me/2017/02/02/create-bi-from-docker/ "如何使用Docker搭建ReportServer报表系统")  - 来源 李牧牧博客



> 把文档存下来

产品文档、项目文档、需求分析、常用软件、工具系统、历史渠道包都需要存放位置，市面上有许多优秀强大的工具，他们要么有容量限制、要么有人数限制或者项目限制，部署一套自己的FTP存储系统方便公司内部使用。

[如何使用Docker搭建 FTP 系统？](http://www.limumu.me/2017/02/01/create-ftp-from-docker/ "如何使用Docker搭建 FTP 系统？")  - 来源 李牧牧博客



# 总结一下

- [x] 选择有靠谱售后的硬件工作站并配备UPS

- [x] 安装操作系统并将所有服务分布式容器化

- [x] 多环境日志与备份统一云存储

- [x] 选择部署接地气的研发辅助系统

- [x] 配备多环境发包系统并绑定通知小秘书

- [x] 部署Bug跟踪系统

- [x] 独立的报表与存储系统让工作如虎添翼




# Q & A
> 问 要是自己搭建这样的系统，估计工作量多大？

答 企业根据自己需要，从头开始一个人两周可以基本部署完毕。


> 问 如何设计开发高并发用户数庞大的代码软件架构？

答 结合上面的文字再参考博文 [《如何设计开发高并发高可用的代码架构？》](http://www.limumu.me/2017/02/16/create-java-from-aliyun/ "如何设计开发高并发高可用的代码架构？")




















