# redis

## 为什么要用nosql

> 1.整个网站的瓶颈

1.数据超过300万条就必须建立索引

2.访问量（读写混合），一个服务器承受不了

> 2.memcached（缓存）+MySQL+垂直拆分
>
> >发展过程：
> >
> >1.优化数据结构和索引
> >
> >2.文件缓存（IO）
> >
> >3.Memcached（高速缓存）

1.网站80%的数据量都是在查询，所以说我们希望减轻数据库的压力，我们可以使用缓存来保证效率。（缓存只能解决读的问题）

> 3.分库分表+水平拆分+MySQL集群

我所认为的集群的概念是由数台服务器组成，都在完成一个功能，可看作成一个节点。

在第二阶段主要解决的是读的压力，第三个阶段主要是去解决写的压力。

>1.切换数据库引擎，由MyISAM->Innodb
>
>MyISAM：表锁，效率低下
>
>Innodb：行锁
>
>2.使用分库分表技术
>
>根据不同的业务
>
>3.MySQL集群

> 4.如今最近的年代

数据量大，且发生变化快。MySQL为代表的关系型数据库已经不能满足业务了（如定位信息，排行榜信息）数据库的IO压力下，表几乎没法变更大。

![image-20210522204209224](/Users/jameszhang/Library/Application Support/typora-user-images/image-20210522204209224.png)

<center>当今互联网架构图</center>

> 为什么要用NoSQL！

用户的个人信息，社交网络，地理位置，用户自己产生的数据，用户日志等等爆发式增长。nosql可以很好的处理这种情况。

## 什么是NoSQL

> Nosql

Nosql=Not Only SQL（不仅仅是SQL）

关系型数据库：表格+行+列

泛指非关系型数据库，传统的关系型数据库很难对付web2.0时代！尤其是超大规模的高并发的社区。

很多的数据类型用户的个人信息，社交网路，地理位置。这些数据的存储不需要一个固定的格式。redis就是通过类似于Java中的Map键值对来存储。

> Nosql特点

解耦：

1.方便扩展（数据之间没有关系，很好扩展）

2.大数据量提高性能（Redis一秒写8万次，读取11万，Nosql的缓存记录是一种细粒度的缓存）

3.数据类型是多样型的（不需要事先设计数据库）

4.传统RDBMS和NoSQL

> 传统的RDBMS
>
> - 结构化组织
> - SQL
> - 数据和关系都存在单独的表中
> - 数据操作语言，数据定义语言
> - 严格的一致性
> - 基础的事务

> Nosql
>
> - 不仅仅是数据库
> - 没有固定的查询语言
> - 键值对存储、列存储、文档存储、图型数据库
> - 最终一致性
> - CAP定理和BASE（异地多活）
> - 高并发、高可用、高可扩展（随时水平拆分）

大数据时代的3V+3高

大数据时代的3V：主要是描述问题的（海量、多样、实时）

大数据时代的3高：主要是对程序的要求

敏捷开发、极限编程



==去除差异化可以通过加一层来实现。==（比如连接多个版本数据库，业务模型的各个字段分布在不同数据源）添加了jdbc或者mybatis来连接数据库。

```bash
#1.商品的基本信息
  名称、价格、商家信息；
  在关系型数据库就可以解决 MySQL/Oracle（淘宝早年去IOE） 王坚
#2.商品的描述，评论（文字比较多）
文档型数据库，MongDB
#3.图片
分布式文件系统 FastDFS
- 淘宝自己的 TFS
- Google GFS
- Hadoop HDFS
- 阿里云的 oss

#4.商品的关键字（搜索）
- 搜索引擎 Isearch 多隆

#5.商品热门的波段信息
-内存数据库
- Redis Tair

#6.商品的交易，外部的支付接口
- 三方应用
```

大型互联网应用信息：

- 数据类型太多了
- 数据源繁多，经常重构
- 数据要改造，大面积改动

==解决方案：统一数据服务平台（UDSL）==



## NoSQL的四大分类

**kv键值对（内容缓存）：**

- 新浪：**Redis**
- 美团：Redis+Tair 
-  阿里、百度：Redis+memecache

**文档型数据库（bson格式和json一样）**

- **MongoDB**：
  * MongoDB是一个基于分布式文件存储系统的数据库，主要用于处理大量的文档
  * MongoDB是一个介于关系型数据库和非关系型数据库中中间的产品！MongoDB是非关系型数据库中功能最丰富，最像关系型数据库。

**列存储数据库** 

- **HBase**
- 分布式文件系统

**图关系型数据库**

- 他存放的是关系，应用场景比如：朋友圈社交网络，广告推荐！
- **Neo4j**，InfoGrid

## Redis入门

> Redis是什么

Redis（Remote Dictionary Server），即远程服务字典

支持网络、可基于内存和持久化的日志型，kv数据库

> Redis能干什么

1.内存存储，持久化，因为内存中断电即失，所以持久化很重要（rdb，aof）

2.效率高，可以用于高速缓存

3.发布订阅系统

4.地图信息分析

5.计时器、计数器（浏览量）

> 特性

1. 多样的数据类型

2. 持久化
3. 集群
4. 事务

> 学习中需要用到的东西

1. 官网
2. 中文网
3. 下载地址

（windows在Github上下载）

redis推荐是在Linux服务器上搭建的

## Redis下载安装

> 1. 下载相关文件压缩包，并解压
> 2. 下载运行环境（gcc）
>
> - ```bash
>   yum install gcc-c++
>   ```
>
> - make编译原文件 
>
> - make test 编译测试
>
> - make install编译安装
>
> 1. 修改redis.conf 配置文件 
>    * daemonize yes
> 2. 启动redis-redis-server /.../ 配置文件的目录
> 3. 访问redis-redis-cli

Redis-benchmark是一个压力测试工具

## 基础知识

redis默认有16个数据库，默认使用的是第0个

```bash
#切换第几个数据库
select x
#查看数据库大小
DBSIZE
#查看所有的key
keys *
#清空当前库
flushdb
#清空所有数据库
flushall
#是否存在键
exists key
```

> redis是单线程

redis是基于内存操作的，CPU利用率不是Redis的性能瓶颈，Redis的瓶颈是根据机器的内存和网络带宽，既然可以使用单线程来实现，就可以使用单线程了。

多线程还要涉及频繁的上下文切换

## redis基本类型

**String类型**

```bash
#像一条记录后面添加字符串
append xxx "xxx"
#获取字符串长度
strlen xxx
#实现++操作
incr xxx
incrby xxx 10
#实现--操作
decr xxx
decrby xxx 10
#获得字符串某一区间的值(包括头尾)
getrange xxx 0 3
#修改某一字符串区间的值（offset为开始的下标）
setrange xxx offset xxx
#setex(set with expire) 设置过期时间
setex xxx 30 "ghjk"
#setnx(set if not exist) 不存在再设置，在分布式锁中会常常使用
#批量设置
mset k1 xxx k2 yyy k3 zzz
mget k1 k2 k3
msetnx
#设置对象
set customer:1 {name:james, age:9}
mset customer:2:name james customer:2:age 9
#getset 先get后set
getset db redis
```

String的使用场景：可以是字符串还可以是数字

- 计数器
- 统计多单位的数量 
- 粉丝数
- 对象缓存存储

**List**

```bash
#向列表中添加值
LPUSH xxx one
RPUSH xxx two
lset list 下标 xxx
#从列表中获取在下标范围中的值
LRANGE list 0 -1
#从列表中移除元素
Lpop list #移除list的第一个元素
Rpop list #移除list的最后一个
Lindex xxx 1 #通过下标获取list的值
Llen xxx #获取列表的长度
Lrem list （个数） xxx #从列表中移除制定的value及个数
ltrim list 1 2 #通过下标的长度来截取列表长度
rpoplpush list1 list2 
linsert list before "world" "other"
```

**Set**

set中的值是不重复的

```bash
#set集合中添加值
sadd myset xxx
# 查看指定set的所有值
smembers set
#查看指定set的值是不是在集合中
sismember set xxx
#获取set集合中的内容元素的个数
scard set
#移除set集合中的指定元素
srem set xxx
#随机获取number个元素
srandmember set number
#随机删除set集合中的元素
spop set
#将一个集合中指定的值xxx移动到另一个集合
smove set1 set2 xxx
#数字集合类（set1-set2）
sdiff set1 set2 差集
sinter set1 set2 交集
sunion set1 set2 并集
```

粉丝共同关注

**Hash**

是一个集合，存储的value是键值对的方式,本质和string类型没有太大的区别

```bash
#存取查
hset myhash xxx xxx
hget myhash xxx
hgetall myhash
hmset
hmget
hdel myhash xxx
hlen myhash #获取集合中的字段数量
hkeys myhash
hvalues myhash
hincr
hdecr
hexists
```

hash用来存放变更的信息，尤其是用户信息的保存。hash更适合对象的存储，String更适合字符串的方式。

**Zset（有序集合）**

在set的基础上，添加一个值，add set xxx || zadd set score xxx

```bash
根据score进行排序
zrangebyscore zset -inf +inf withscores
移除任务中的元素
zrem zset xxx
```





