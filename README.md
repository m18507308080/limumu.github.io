# limumu blog 模板

[李牧牧的博客](http://www.limumu.me) limumu.me blog

![](http://www.limumu.me/assets/img/blog-me.png)


## 关于模版

我的博客模版是从作者 [Hux Blog](https://github.com/Huxpro) 的 https://github.com/Huxpro/huxpro.github.io Fork的，感谢Hux。


## 修改了哪些东西

> 在作者框架基础上作了如下变化

- [x] 所有 开源工具库 改由 cdn.bootcss.com 获取
- [x] 所有 自定义资源文件 改由 七牛云存储 获取
- [x] 替换 多说评论插件 为 搜狐评论畅言
- [x] 替换 百度打点 为 百度自适应打点
- [x] 修改 package.json 同步提交到 GitHub.com 与 Coding.net ，解决 GitHub 被百度爬虫屏蔽问题
- [x] 添加 搜狐畅言打赏功能
- [x] 添加 百度多渠道分享
- [x] 去除了 Disqus、多说、Tag、Catalog、Google Analytics功能提升速度与体验


## 核心文件结构说明

- [x] _config.yml 个人资料、基础配置
- [x] index.html  首页固定模版，百度统计
- [x] about.html  说明页固定模版，畅言评论插件、打赏功能、百度多渠道分享
- [x] _layouts/post.html 文章详情模版，畅言评论插件、打赏功能、百度多渠道分享
- [x] _posts/*.markdown 此目录文章自动编译为静态模版并按日期显示在首页


> 支付宝、微信打赏

![](http://www.limumu.me/assets/img/blog-cheking.png)

> 页面资源加载

![](http://www.limumu.me/assets/img/blog-network.png)

> 全国网络测试

![](http://www.limumu.me/assets/img/blog-ping.png)

> 百度爬虫收录情况

![](http://www.limumu.me/assets/img/blog-baidu.png)


## 感谢

Jekyll、Github Pages、[Hux Blog](https://github.com/Huxpro)!