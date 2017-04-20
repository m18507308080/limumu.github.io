---
layout:     post
title:      "如何安装阿里云Redis缓存系统并配置持久化？"
subtitle:   "《推蜜》官方互动养成APP，借力《阿里云》从零到壹的演变"
date:       2017-01-18 10:00:00
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



### 如何在ECS上搭建Redis？

> 官网下载Redis

Redis官网提供最新版下载，如果需要指定的版本，可以自行编辑URL规则直接下载安装包。

```
# wget http://download.redis.io/releases/redis-3.2.8.tar.gz

正在解析主机 download.redis.io (download.redis.io)... 109.74.203.151
正在连接 download.redis.io (download.redis.io)|109.74.203.151|:80... 已连接。
已发出 HTTP 请求，正在等待回应... 200 OK
长度：1547237 (1.5M) [application/x-gzip]
正在保存至: “redis-3.2.8.tar.gz”

100%[=======================>] 1,547,237    406KB/s 用时 3.7s   

(406 KB/s) - 已保存 “redis-3.2.8.tar.gz” [1547237/1547237])
```

[Redis官网下载页面](https://redis.io/download "Redis官网下载页面")  - 来源 Redis官网

> 安装Redis服务

```
# tar xzvf redis-3.2.8.tar.gz
# cd redis-3.2.8
# make PREFIX=/app/redis intall #安装到指定目录中
```

如果make失败，一般是你们系统中还未安装gcc,那么可以通过yum安装之：

```
# yum update 
# yum install gcc
```



> 解析配置文件

```
# redis 配置文件示例
 
# 当你需要为某个配置项指定内存大小的时候，必须要带上单位，
# 通常的格式就是 1k 5gb 4m 等酱紫：
#
# 1k  => 1000 bytes
# 1kb => 1024 bytes
# 1m  => 1000000 bytes
# 1mb => 1024*1024 bytes
# 1g  => 1000000000 bytes
# 1gb => 1024*1024*1024 bytes
#
# 单位是不区分大小写的，你写 1K 5GB 4M 也行
 
################################## INCLUDES ###################################
 
# 假如说你有一个可用于所有的 redis server 的标准配置模板，
# 但针对某些 server 又需要一些个性化的设置，
# 你可以使用 include 来包含一些其他的配置文件，这对你来说是非常有用的。
#
# 但是要注意哦，include 是不能被 config rewrite 命令改写的
# 由于 redis 总是以最后的加工线作为一个配置指令值，所以你最好是把 include 放在这个文件的最前面，
# 以避免在运行时覆盖配置的改变，相反，你就把它放在后面。
#
# include /path/to/local.conf
# include /path/to/other.conf
 
################################ 常用 #####################################
 
# 默认情况下 redis 不是作为守护进程运行的，如果你想让它在后台运行，你就把它改成 yes。
# 当redis作为守护进程运行的时候，它会写一个 pid 到 /var/run/redis.pid 文件里面。
daemonize no
 
# 当redis作为守护进程运行的时候，它会把 pid 默认写到 /var/run/redis.pid 文件里面，
# 但是你可以在这里自己制定它的文件位置。
pidfile /var/run/redis.pid
 
# 监听端口号，默认为 6379，如果你设为 0 ，redis 将不在 socket 上监听任何客户端连接。
port 6379
 
# TCP 监听的最大容纳数量
#
# 在高并发的环境下，你需要把这个值调高以避免客户端连接缓慢的问题。
# Linux 内核会一声不响的把这个值缩小成 /proc/sys/net/core/somaxconn 对应的值，
# 所以你要修改这两个值才能达到你的预期。
tcp-backlog 511
 
# 默认情况下，redis 在 server 上所有有效的网络接口上监听客户端连接。
# 你如果只想让它在一个网络接口上监听，那你就绑定一个IP或者多个IP。
#
# 示例，多个IP用空格隔开:
#
# bind 192.168.1.100 10.0.0.1
# bind 127.0.0.1
 
# 指定 unix socket 的路径。
#
# unixsocket /tmp/redis.sock
# unixsocketperm 755
 
# 指定在一个 client 空闲多少秒之后关闭连接（0 就是不管它）
timeout 0
 
# tcp 心跳包。
#
# 如果设置为非零，则在与客户端缺乏通讯的时候使用 SO_KEEPALIVE 发送 tcp acks 给客户端。
# 这个之所有有用，主要由两个原因：
#
# 1) 防止死的 peers
# 2) Take the connection alive from the point of view of network
#    equipment in the middle.
#
# On Linux, the specified value (in seconds) is the period used to send ACKs.
# Note that to close the connection the double of the time is needed.
# On other kernels the period depends on the kernel configuration.
#
# A reasonable value for this option is 60 seconds.
# 推荐一个合理的值就是60秒
tcp-keepalive 0
 
# 定义日志级别。
# 可以是下面的这些值：
# debug (适用于开发或测试阶段)
# verbose (many rarely useful info, but not a mess like the debug level)
# notice (适用于生产环境)
# warning (仅仅一些重要的消息被记录)
loglevel notice
 
# 指定日志文件的位置
logfile ""
 
# 要想把日志记录到系统日志，就把它改成 yes，
# 也可以可选择性的更新其他的syslog 参数以达到你的要求
# syslog-enabled no
 
# 设置 syslog 的 identity。
# syslog-ident redis
 
# 设置 syslog 的 facility，必须是 USER 或者是 LOCAL0-LOCAL7 之间的值。
# syslog-facility local0
 
# 设置数据库的数目。
# 默认数据库是 DB 0，你可以在每个连接上使用 select <dbid> 命令选择一个不同的数据库，
# 但是 dbid 必须是一个介于 0 到 databasees - 1 之间的值
databases 16
 
################################ 快照 ################################
#
# 存 DB 到磁盘：
#
#   格式：save <间隔时间（秒）> <写入次数>
#
#   根据给定的时间间隔和写入次数将数据保存到磁盘
#
#   下面的例子的意思是：
#   900 秒内如果至少有 1 个 key 的值变化，则保存
#   300 秒内如果至少有 10 个 key 的值变化，则保存
#   60 秒内如果至少有 10000 个 key 的值变化，则保存
#　　
#   注意：你可以注释掉所有的 save 行来停用保存功能。
#   也可以直接一个空字符串来实现停用：
#   save ""
 
save 900 1
save 300 10
save 60 10000
 
# 默认情况下，如果 redis 最后一次的后台保存失败，redis 将停止接受写操作，
# 这样以一种强硬的方式让用户知道数据不能正确的持久化到磁盘，
# 否则就会没人注意到灾难的发生。
#
# 如果后台保存进程重新启动工作了，redis 也将自动的允许写操作。
#
# 然而你要是安装了靠谱的监控，你可能不希望 redis 这样做，那你就改成 no 好了。
stop-writes-on-bgsave-error yes
 
# 是否在 dump .rdb 数据库的时候使用 LZF 压缩字符串
# 默认都设为 yes
# 如果你希望保存子进程节省点 cpu ，你就设置它为 no ，
# 不过这个数据集可能就会比较大
rdbcompression yes
 
# 是否校验rdb文件
rdbchecksum yes
 
# 设置 dump 的文件位置
dbfilename dump.rdb
 
# 工作目录
# 例如上面的 dbfilename 只指定了文件名，
# 但是它会写入到这个目录下。这个配置项一定是个目录，而不能是文件名。
dir ./
 
################################# 主从复制 #################################
 
# 主从复制。使用 slaveof 来让一个 redis 实例成为另一个reids 实例的副本。
# 注意这个只需要在 slave 上配置。
#
# slaveof <masterip> <masterport>

# 如果 master 需要密码认证，就在这里设置
# masterauth <master-password>
 
# 当一个 slave 与 master 失去联系，或者复制正在进行的时候，
# slave 可能会有两种表现：
#
# 1) 如果为 yes ，slave 仍然会应答客户端请求，但返回的数据可能是过时，
#    或者数据可能是空的在第一次同步的时候
#
# 2) 如果为 no ，在你执行除了 info he salveof 之外的其他命令时，
#    slave 都将返回一个 "SYNC with master in progress" 的错误，
#
slave-serve-stale-data yes
 
# 你可以配置一个 slave 实体是否接受写入操作。
# 通过写入操作来存储一些短暂的数据对于一个 slave 实例来说可能是有用的，
# 因为相对从 master 重新同步数而言，据数据写入到 slave 会更容易被删除。
# 但是如果客户端因为一个错误的配置写入，也可能会导致一些问题。
#
# 从 redis 2.6 版起，默认 slaves 都是只读的。
#
# Note: read only slaves are not designed to be exposed to untrusted clients
# on the internet. It's just a protection layer against misuse of the instance.
# Still a read only slave exports by default all the administrative commands
# such as CONFIG, DEBUG, and so forth. To a limited extent you can improve
# security of read only slaves using 'rename-command' to shadow all the
# administrative / dangerous commands.
# 注意：只读的 slaves 没有被设计成在 internet 上暴露给不受信任的客户端。
# 它仅仅是一个针对误用实例的一个保护层。
slave-read-only yes
 
# Slaves 在一个预定义的时间间隔内发送 ping 命令到 server 。
# 你可以改变这个时间间隔。默认为 10 秒。
#
# repl-ping-slave-period 10
 
# The following option sets the replication timeout for:
# 设置主从复制过期时间
#
# 1) Bulk transfer I/O during SYNC, from the point of view of slave.
# 2) Master timeout from the point of view of slaves (data, pings).
# 3) Slave timeout from the point of view of masters (REPLCONF ACK pings).
#
# It is important to make sure that this value is greater than the value
# specified for repl-ping-slave-period otherwise a timeout will be detected
# every time there is low traffic between the master and the slave.
# 这个值一定要比 repl-ping-slave-period 大
#
# repl-timeout 60
 
# Disable TCP_NODELAY on the slave socket after SYNC?
#
# If you select "yes" Redis will use a smaller number of TCP packets and
# less bandwidth to send data to slaves. But this can add a delay for
# the data to appear on the slave side, up to 40 milliseconds with
# Linux kernels using a default configuration.
#
# If you select "no" the delay for data to appear on the slave side will
# be reduced but more bandwidth will be used for replication.
#
# By default we optimize for low latency, but in very high traffic conditions
# or when the master and slaves are many hops away, turning this to "yes" may
# be a good idea.
repl-disable-tcp-nodelay no
 
# 设置主从复制容量大小。这个 backlog 是一个用来在 slaves 被断开连接时
# 存放 slave 数据的 buffer，所以当一个 slave 想要重新连接，通常不希望全部重新同步，
# 只是部分同步就够了，仅仅传递 slave 在断开连接时丢失的这部分数据。
#
# The biggest the replication backlog, the longer the time the slave can be
# disconnected and later be able to perform a partial resynchronization.
# 这个值越大，salve 可以断开连接的时间就越长。
#
# The backlog is only allocated once there is at least a slave connected.
#
# repl-backlog-size 1mb
 
# After a master has no longer connected slaves for some time, the backlog
# will be freed. The following option configures the amount of seconds that
# need to elapse, starting from the time the last slave disconnected, for
# the backlog buffer to be freed.
# 在某些时候，master 不再连接 slaves，backlog 将被释放。
#
# A value of 0 means to never release the backlog.
# 如果设置为 0 ，意味着绝不释放 backlog 。
#
# repl-backlog-ttl 3600
 
# 当 master 不能正常工作的时候，Redis Sentinel 会从 slaves 中选出一个新的 master，
# 这个值越小，就越会被优先选中，但是如果是 0 ， 那是意味着这个 slave 不可能被选中。
#
# 默认优先级为 100。
slave-priority 100
 
################################## 安全 ###################################
 
# Require clients to issue AUTH <PASSWORD> before processing any other
# commands.  This might be useful in environments in which you do not trust
# others with access to the host running redis-server.
#
# This should stay commented out for backward compatibility and because most
# people do not need auth (e.g. they run their own servers).
# 
# Warning: since Redis is pretty fast an outside user can try up to
# 150k passwords per second against a good box. This means that you should
# use a very strong password otherwise it will be very easy to break.
# 
# 设置认证密码
# requirepass foobared
 
################################### 限制 ####################################
 
# Set the max number of connected clients at the same time. By default
# this limit is set to 10000 clients, however if the Redis server is not
# able to configure the process file limit to allow for the specified limit
# the max number of allowed clients is set to the current file limit
# minus 32 (as Redis reserves a few file descriptors for internal uses).
#
# 一旦达到最大限制，redis 将关闭所有的新连接
# 并发送一个‘max number of clients reached’的错误。
#
# maxclients 10000
 
# 如果你设置了这个值，当缓存的数据容量达到这个值， redis 将根据你选择的
# eviction 策略来移除一些 keys。
#
# 如果 redis 不能根据策略移除 keys ，或者是策略被设置为 ‘noeviction’，
# redis 将开始响应错误给命令，如 set，lpush 等等，
# 并继续响应只读的命令，如 get
#
# This option is usually useful when using Redis as an LRU cache, or to set
# a hard memory limit for an instance (using the 'noeviction' policy).
#
# WARNING: If you have slaves attached to an instance with maxmemory on,
# the size of the output buffers needed to feed the slaves are subtracted
# from the used memory count, so that network problems / resyncs will
# not trigger a loop where keys are evicted, and in turn the output
# buffer of slaves is full with DELs of keys evicted triggering the deletion
# of more keys, and so forth until the database is completely emptied.
#
# In short... if you have slaves attached it is suggested that you set a lower
# limit for maxmemory so that there is some free RAM on the system for slave
# output buffers (but this is not needed if the policy is 'noeviction').
#
# 最大使用内存
# maxmemory <bytes>
 
# 最大内存策略，你有 5 个选择。
# 
# volatile-lru -> remove the key with an expire set using an LRU algorithm
# volatile-lru -> 使用 LRU 算法移除包含过期设置的 key 。
# allkeys-lru -> remove any key accordingly to the LRU algorithm
# allkeys-lru -> 根据 LRU 算法移除所有的 key 。
# volatile-random -> remove a random key with an expire set
# allkeys-random -> remove a random key, any key
# volatile-ttl -> remove the key with the nearest expire time (minor TTL)
# noeviction -> don't expire at all, just return an error on write operations
# noeviction -> 不让任何 key 过期，只是给写入操作返回一个错误
# 
# Note: with any of the above policies, Redis will return an error on write
#       operations, when there are not suitable keys for eviction.
#
#       At the date of writing this commands are: set setnx setex append
#       incr decr rpush lpush rpushx lpushx linsert lset rpoplpush sadd
#       sinter sinterstore sunion sunionstore sdiff sdiffstore zadd zincrby
#       zunionstore zinterstore hset hsetnx hmset hincrby incrby decrby
#       getset mset msetnx exec sort
#
# The default is:
#
# maxmemory-policy noeviction
 
############################## APPEND ONLY MODE ###############################
 
# By default Redis asynchronously dumps the dataset on disk. This mode is
# good enough in many applications, but an issue with the Redis process or
# a power outage may result into a few minutes of writes lost (depending on
# the configured save points).
#
# The Append Only File is an alternative persistence mode that provides
# much better durability. For instance using the default data fsync policy
# (see later in the config file) Redis can lose just one second of writes in a
# dramatic event like a server power outage, or a single write if something
# wrong with the Redis process itself happens, but the operating system is
# still running correctly.
#
# AOF and RDB persistence can be enabled at the same time without problems.
# If the AOF is enabled on startup Redis will load the AOF, that is the file
# with the better durability guarantees.
#
# Please check http://redis.io/topics/persistence for more information.
 
appendonly no
 
# The name of the append only file (default: "appendonly.aof")
 
appendfilename "appendonly.aof"
 
# The fsync() call tells the Operating System to actually write data on disk
# instead to wait for more data in the output buffer. Some OS will really flush 
# data on disk, some other OS will just try to do it ASAP.
#
# Redis supports three different modes:
#
# no: don't fsync, just let the OS flush the data when it wants. Faster.
# always: fsync after every write to the append only log . Slow, Safest.
# everysec: fsync only one time every second. Compromise.
#
# The default is "everysec", as that's usually the right compromise between
# speed and data safety. It's up to you to understand if you can relax this to
# "no" that will let the operating system flush the output buffer when
# it wants, for better performances (but if you can live with the idea of
# some data loss consider the default persistence mode that's snapshotting),
# or on the contrary, use "always" that's very slow but a bit safer than
# everysec.
#
# More details please check the following article:
# http://antirez.com/post/redis-persistence-demystified.html
#
# If unsure, use "everysec".
 
# appendfsync always
appendfsync everysec
# appendfsync no

```



> 修改默认配置

```
# 修改daemonize为yes，即默认以后台程序方式运行（还记得前面手动使用&号强制后台运行吗）。
daemonize no
# 可修改默认监听端口
port 6379
# 修改生成默认日志文件位置
logfile "/data/redis/logs/redis.log"
# 配置持久化文件存放位置
dir /app/redis/redisData
# 开启数据持久化，让Redis将数据写入到文件中
appendfilename "/app/redis/appendonly.aof"
# 设置认证密码，建议使用MD5码
requirepass 823da4223e46ec671a10ea13d7823534
```



> 启动Redis服务

```
＃ redis-server /app/redis/redis.conf # 指定读取配置文件启动服务
* Increased maximum number of open files to 10032 (it was originally set to 256).
                _._                                                  
           _.-``__ ''-._                                             
      _.-``    `.  `_.  ''-._           Redis 3.8.2 (00000000/0) 64 bit
  .-`` .-```.  ```\/    _.,_ ''-._                                   
 (    '      ,       .-`  | `,    )     Running in stand alone mode
 |`-._`-...-` __...-.``-._|'` _.-'|     Port: 6379
 |    `-._   `._    /     _.-'    |     
  `-._    `-._  `-./  _.-'    _.-'                                   
 |`-._`-._    `-.__.-'    _.-'_.-'|                                  
 |    `-._`-._        _.-'_.-'    |           http://redis.io        
  `-._    `-._`-.__.-'_.-'    _.-'                                   
 |`-._`-._    `-.__.-'    _.-'_.-'|                                  
 |    `-._`-._        _.-'_.-'    |                                  
  `-._    `-._`-.__.-'_.-'    _.-'                                   
      `-._    `-.__.-'    _.-'                                       
          `-._        _.-'                                           
              `-.__.-'                                               

[1760] # Server started, Redis version 3.8.2
[1760] * The server is now ready to accept connections on port 6379
```



> 检查是否启动成功

```
#检测后台进程是否存在
ps -ef |grep redis

#检测6379端口是否在监听
netstat -lntp | grep 6379

#使用`redis-cli`客户端检测连接是否正常
./redis-cli
127.0.0.1:6379> keys *
(empty list or set)
127.0.0.1:6379> set key "hello world"
OK
127.0.0.1:6379> get key
"hello world"
```



> 停止 Redis 服务

```
#使用客户端
redis-cli shutdown
#因为Redis可以妥善处理SIGTERM信号，所以直接kill -9也是可以的
kill -9 PID
```



> 配置主从服务

```
# 复制一份新的 redis-slave.conf 文件，告诉新配置文件它从主服务读取数据
# slaveof <masterip> <masterport>
# 启动从服务时，指定读取redis-slave.conf文件启动
```



> 借力 OSS 将 Redis 交给云储存以及云备份

阿里云提供 OSSFS 工具，可以在Linux系统中把OSS bucket 挂载到本地文件系统中，您能够便捷地通过本地文件系统操作OSS 上的对象，实现数据的共享。 

[OSSFS 安装说明](https://help.aliyun.com/document_detail/32196.html "OSSFS 安装说明")  - 来源 阿里云

