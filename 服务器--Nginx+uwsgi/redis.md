## Redis简介
Redis 是完全开源免费的，是一个高性能的key-value数据库。
Redis与其他key-value缓存缓存产品有以下三个特点：
- Redis支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用。
- Redis不仅仅支持简单的key-value类型的数据，同时还提供list，set，zset，hash等数据结构的存储。
- Redis支持数据的备份，即master-slave模式的数据备份。
## Redis优势
- 性能极高 – Redis能读的速度是110000次/s,写的速度是81000次/s 。
- 丰富的数据类型 – Redis支持二进制案例的 Strings, Lists, Hashes, Sets 及 Ordered Sets 数据类型操作。
- 原子 – Redis的所有操作都是原子性的，意思就是要么成功执行要么失败完全不执行。单个操作是原子性的。多个操作也支持事务，即原子性，通过MULTI和EXEC指令包起来。
- 丰富的特性 – Redis还支持 publish/subscribe, 通知, key 过期等等特性。
## Redis与其他key-value存储有什么不同？
- Redis有着更为复杂的数据结构并且提供对他们的原子性操作，这是一个不同于其他数据库的进化路径。Redis的数据类型都是基于基本数据结构的同时对程序员透明，无需进行额外的抽象。
- Redis运行在内存中但是可以持久化到磁盘，所以在对不同数据集进行高速读写时需要权衡内存，因为数据量不能大于硬件内存。在内存数据库方面的另一个优点是，相比在磁盘上相同的复杂的数据结构，在内存中操作起来非常简单，这样Redis可以做很多内部复杂性很强的事情。同时，在磁盘格式方面他们是紧凑的以追加的方式产生的，因为他们并不需要进行随机访问。
## window操作redis
#### 下载
[redis下载](https://github.com/MSOpenTech/redis/releases)
#### redis使用方式
- Redis临时服务
- Redis默认服务安装
- Redis自定义服务安装
- Redis主从服务安装
#### Redis临时服务
进入Redis安装包目录，启动临时服务
```Python
redis-server.exe  redis.window.conf
# 服务端调用
redis-cli.exe -h -p
# 客户端调用
```
#### Redis默认服务安装
```Python
redis-server.exe --service-install redis.windows.conf --loglevel verbose
# 此时window服务中将注册Redis服务
redis-server.exe --service-start
# 启动服务
redis-cli.exe -h 127.0.0.1 -p 6379
# 客户端调用
redis-server.exe --service-stop
# 停止服务
redis-server.exe --service-uninstall
# 卸载服务
```

#### Redis自定义服务安装
```Python
redis-server.exe --service-install redis.windows.conf --service-name RedisServer1 --loglevel verbose
# 在window服务中注册Redis服务
redis-server.exe --service-start --service-name RedisServer1
# 启动服务
redis-cli.exe -h 127.0.0.1 -p 6379
# 客户端调用
redis-server.exe --service-stop --Service-name RedisServer1
# 停止服务
redis-server.exe --service-uninstall --Service-name RedisServer1
# 卸载服务
```
#### 安装主从
为了分担读写压力，Redis支持主从复制，Redis的主从结构可以采用一主多从或者级联结构，Redis主从复制可以根据是否是全量分为全量同步和增量同步  
步骤：
- 复制所有文件
- 主服务器redis.windows.conf修改如下：
```
port 6379
```
- 从服务器redis.windows.conf修改如下：
```
port 6380
slaveof 127.0.0.1 6379
```
- 启动主从服务器
- 160  all 2100  116 
- 启动主从客户端
```
redis-cli.exe -h 127.0.0.1 -p 6379
redis-cli.exe -h 127.0.0.1 -p 6380
```
## 集群简介
Redis集群是一个可以在多个Redis节点之间进行数据共享的设施

Redis集群不支持那些需要同时处理多个键的Redis命令，因为执行这些命令需要在多个Redis节点之间移动数据，并且在高负载的情况下，这些命令将降低Redis集群的性能，并导致不可预测的行为。  

Redis集群通过服务来提供一定程度的可用性：即使集群中有一部分节点失效或者无法进行通讯，集群也可以继续处理命令请求。

Redis集群提供了以下两个好处：
- 将数据自动切分到多个节点的能力。
- 当集群中的一部分节点失效或者无法进行通讯时，仍然可以继续处理请求的能力。
## Redis集群分区原理
Redis集群键分布算法使用数据分片，而非一致性哈希来实现：一个Redis集群包含16384个哈希槽，他们的编号为0~16383，这个槽时一个逻辑意义上的槽，实际上并不存在，redis中的每个key都属于这1638个哈希槽的其中一个， 存取key时都要进行key->slot的映射计算。
Redis集群有16384个哈希槽，每个key通过CRC16校验后对16384取模来决定放置哪个槽，集群的每个节点负责一部分hash槽，举个例子，比如当前集群有3个节点，那么
：
节点A包含0到5500号哈希槽
节点B包含5501到11000号哈希槽
节点C包含11001到16384号哈希槽
这种结构很容易添加或者删除节点
## Ubuntu安装过程
```
sudo apt-get install redis-server
# 下载
service redis status
# 开启redis服务
redis-cli
# 打开redis客户端
./src/redis-cli info | grep 'redis_version'
# 本地查看版本
./src/redis-cli -h 远程主机的IP info | grep 'redis_version'
# 远程查看版本
```
## 集群操作
#### 单机配置　　

创建集群目录
```
cd /home/horns/桌面/redis集群/
mkdir -p 7000 7001 7002 7003 7004 7005 7006
```
将/etc/redis/redis.conf/　分别复制到所有的文件夹中，并且修改以下设置

```
port 7000（每个节点的端口号）
daemonize yes（后台运行）
bind 192.168.1.110（绑定当前机器 IP）
dir /home/redis-cluster/7000/data/（数据文件存放位置）
pidfile /var/run/redis_7000.pid（pid 7000和port要对应）
cluster-enabled yes（启动集群模式）
cluster-config-file nodes-7000.conf（7000和port要对应）
cluster-node-timeout 15000
appendonly yes
```
启动节点
```
redis-server /home/horns/redis集群/7000/redis.conf
...
ps -aux | grep redis
# 查看进程

```
安装集群所需软件
```
sudo apt-get install ruby
gem install redis
ruby redis-trib.rb create --replicas 1 172.17.37.110:7000 172.17.37.110:7001 172.17.37.110:7002 172.17.37.110:7003 172.17.37.110:7004 172.17.37.110:7005 172.17.37.110:7006
```
启动集群
```
ruby redis-trib.rb create --replicas 1 ip:port ip:port ip:port ....
ruby redis-trib.rb create --replicas 1 172.17.37.110:7000 172.17.37.110:7001 172.17.37.110:7002 172.17.37.110:7003 172.17.37.110:7004 172.17.37.110:7005 172.17.37.110:7006
```
redis-trib.rb文件在 /usr/share/doc/redis-tools/examples 中

--replicas 1 表示主从复制比例为 1:1，即一个主节点对应一个从节点；然后，默认给我们分配好了每个主节点和对应从节点服务，以及 solt 的大小，因为在 Redis 集群中有且仅有 16383 个 solt ，默认情况会给我们平均分配，当然你可以指定，后续的增减节点也可以重新分配。
我们现在有六个节点，三个主节点三个从节点，默认最少需要六个节点才能组成集群。

#### 多机器配置
与单击配置相比较，需要修改的
- 绑定ip配置为每个机器的ip
- 端口号可以使用一样的，也可以配置为不一样的
- 安装的软件在每个机器上必须安装
- 启动集群命令只要在其中一个机器上执行即可

### Python操作Redis集群
安装包
```
pip install redis-py-cluster
```
```
from rediscluster import StrictRedisCluster
startup_nodes = [
    {"host":"192.168.1.110", "port":7000},
    {"host":"192.168.1.110", "port":7001},
    {"host":"192.168.1.110", "port":7002},
    {"host":"192.168.1.110", "port":7003},
    {"host":"192.168.1.110", "port":7004},
    {"host":"192.168.1.110", "port":7005}
]
rc = StrictRedisCluster(startup_nodes=startup_nodes, decode_responses=True)
rc.set('name','admin')
rc.set('age',18)
print "name is: ", rc.get('name')
print "age  is: ", rc.get('age')
```
