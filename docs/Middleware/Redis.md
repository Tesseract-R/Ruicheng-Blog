### <font size=3pt face="MV Boli" color="gray">By Ruicheng Zhang</font>



# Redis



### *Redis快的原因：*

-   *基于内存，没有磁盘IO的开销*
-   *单线程，避免线程切换的性能损耗 (IO密集型系统，CPU不是Redis的制约瓶颈)*
-   *非阻塞IO多路复用机制*
-   *底层的数据存储结构优化，使用原生的数据结构提升性能*



## 底层数据结构

-   字符串
-   链表
-   字典
-   跳跃表
-   整数集合
-   压缩链表



## 支持的数据类型

-   String
-   Hash
-   Set
-   List
-   SortedSet



-   Bitmap
-   HyperLogLog
-   Geospatial



## 过期Key的删除策略：

-   惰性删除
-   定期删除
-   定时删除



## 缓存

### 缓存击穿

### 缓存雪崩

### 缓存穿透

### 缓存集中失效

### 缓存热点

### 缓存大Key

### 缓存数据一致性

### 数据并发竞争预热



## 集群方案

-   主从复制
-   Sentinel（哨兵）模式
-   Redis Cluster模式





## 负载均衡

