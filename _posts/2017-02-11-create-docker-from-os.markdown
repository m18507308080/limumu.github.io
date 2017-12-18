---
layout:     post
title:      "如何部署分布式Docker容器服务？"
subtitle:   ""
date:       2017-02-11 10:00:00
author:     "李牧牧"
header-img: "http://onb688cva.bkt.clouddn.com/assets:img:home-bg.jpg"
header-mask: 0.1
catalog:    true
tags:
    - 阿里云
    - 混合云
---

> 本文发布于 [李牧牧的博客](http://limumu.me) 转载请保留链接 ;)



# 工欲利其事，必先利其器

我们使用`Docker`的第一步，应该是获取一个官方的镜像，例如`mysql`、`wordpress`，基于这些基础镜像我们可以开发自己个性化的应用。我们可以使用`Docker`命令行工具来下载官方镜像。
但是因为网络原因，我们下载一个300M的镜像需要很长的时间，甚至下载失败。因为这个原因，阿里云容器`Hub`服务提供了官方的镜像站点加速官方镜像的下载速度。

![](http://onb688cva.bkt.clouddn.com/assets:post:img:201705161323013.jpg)

> 下载阿里云`Docker`加速器 

```
curl -sSL http://acs-public-mirror.oss-cn-hangzhou.aliyuncs.com/docker-engine/internet | sh -
```

> 针对`Docker`客户端版本大于1.10的用户

- 您可以通过修改daemon配置文件`/etc/docker/daemon.json`来使用加速器：

  ```
  sudo mkdir -p /etc/docker
  sudo tee /etc/docker/daemon.json <<-'EOF'
  {
    "registry-mirrors": ["https://hx11cpdt.mirror.aliyuncs.com"]
  }
  EOF
  sudo systemctl daemon-reload
  sudo systemctl restart docker
  ```

> 针对`Docker`客户的版本小于等于1.10的用户

或者想配置启动参数，可以使用下面的命令将配置添加到`Docker Daemon`的启动参数中。

- 系统要求 `CentOS 7` 以上，`Docker 1.9` 以上。

  ```
  sudo cp -n /lib/systemd/system/docker.service /etc/systemd/system/docker.service
  ```

- Docker 1.12 以下版本使用 `Docker Daemon` 命令

  ```
  sudo sed -i "s|ExecStart=/usr/bin/docker daemon|ExecStart=/usr/bin/docker daemon --registry-mirror=https://qxx96o44.mirror.aliyuncs.com|g" /etc/systemd/system/docker.service
  ```

- Docker 1.12 及以上版本使用 `Docker` 命令，这里`https://xxxxxxx.mirror.aliyuncs.com` 地址需要注册阿里云的免费账户才能提供。

  ```
  sudo sed -i "s|ExecStart=/usr/bin/dockerd|ExecStart=/usr/bin/dockerd --registry-mirror=https://xxxxxxx.mirror.aliyuncs.com|g" /etc/systemd/system/docker.service
  sudo systemctl daemon-reload
  sudo service docker restart
  ```

 [使用阿里云 Docker 镜像加速器](https://yq.aliyun.com/articles/29941 "使用阿里云 Docker 镜像加速器")  - 来源 阿里云



# 扬长避短，知物善用

随着`Docker`被大规模的部署应用，如何通过可视化的方式了解`Docker`环境的状态以及健康变得越来越重要。下面基于以下标准来评估选择工具：

1. 易于部署

2. 是否支持分布式
3. 信息呈现的详细度
4. 整个部署过程中日志的聚集程度
5. 数据报警能力
6. 是否可以监控非`Docker`的资源
7. 成本

对比工具如下

- [x] Docker Stats  难部署、信息不完整、无报警、无集成、无监控、免费
- [x] CAdvisor         难部署、无报警、无监控       
- [x] Scout              难部署、收费
- [x] DataDog         难部署、收费
- [x] Shipyard         难部署
- [x] DockerUI        不支持多主机

根据以上结果，选择相对功能完整的`Shipyard`作为集中化管理平台。



> 安装 `Docker` 集中化 `Web` 可视化管理平台 `Shipyard`

![](http://onb688cva.bkt.clouddn.com/assets:post:img:201705161323011.jpg)



> 主机部署脚步，［192.168.200.5］为主机地址

```
docker run -ti -d --restart=always --name shipyard-rethinkdb rethinkdb

docker run -ti -d -p 4001:4001 -p 7001:7001 --restart=always --name shipyard-discovery microbox/etcd -name discovery

docker run -ti -d -p 2375:2375 --hostname=$HOSTNAME --restart=always --name shipyard-proxy -v /var/run/docker.sock:/var/run/docker.sock -e PORT=2375 shipyard/docker-proxy:latest

docker run -ti -d --restart=always --name shipyard-swarm-manager swarm:latest manage --replication --addr 192.168.200.5:3375 --host tcp://0.0.0.0:3375 etcd://192.168.200.5:4001

docker run -ti -d --restart=always --name shipyard-swarm-agent swarm:latest join --addr 192.168.200.5:2375 etcd://192.168.200.5:4001

docker run -ti -d --restart=always --name shipyard-controller --link shipyard-rethinkdb:rethinkdb --link shipyard-swarm-manager:swarm -p 192.168.200.200:80:8080 shipyard/shipyard:latest server -d tcp://swarm:3375
```



> 如何有其他物理机要加入 `Docker` 集中管理，只需执行从机部署脚步，［192.168.200.6］为主机地址

```
docker run -ti -d -p 2375:2375 --hostname=$HOSTNAME --restart=always --name shipyard-proxy -v /var/run/docker.sock:/var/run/docker.sock -e PORT=2375 shipyard/docker-proxy:latest

docker run -ti -d --restart=always --name shipyard-swarm-manager swarm:latest \manage --replication --addr 192.168.200.6:3375 --host tcp://0.0.0.0:3375 etcd://192.168.200.5:4001

docker run -ti -d --restart=always --name shipyard-swarm-agent swarm:latest join --addr 192.168.200.6:2375 etcd://192.168.200.5:4001
```

![](http://onb688cva.bkt.clouddn.com/assets:post:img:201705161323012.jpg)

[ 如何部署 Docker Shipyard？](http://www.jianshu.com/p/f9f855f8f3f4 "如何部署 Docker Shipyard？")  - 来源 简书

[ 如何使用 Docker ？](http://www.jianshu.com/p/f3f1e6cefda0 "如何使用 Docker ？")  - 来源 简书



# Q&A

> 问 要是自己搭建这样的系统，估计工作量多大？

答 企业根据自己需要，从头开始一个人两周可以基本部署完毕。

> 问 如何将公司内网测试环境与阿里云生产打通，并持续集成呢？

答 结合本文参考另一篇博文 [《如何零成本构建研发运维一体化？》](http://www.limumu.me/2017/02/18/create-devops-from-aliyun/ "如何零成本构建研发运维一体化？")

> 问 如何设计开发高并发用户数庞大的代码软件架构？

答 结合上面的文字再参考博文 [《如何设计开发高并发高可用的代码架构？》



