### <font size=3pt face="MV Boli" color="gray">By Ruicheng Zhang</font>

# RabbitMQ

## 特性

对于Client Publisher而言，Server是消息的接受者

对于Client Consumer而言，Server是消息的发送者

1.   消息仓储：持久化

     保证消息不丢失

2.   延后传递：堆积

3.   复制（广播）

     不同的消息生产者生产了具有不同routing key的消息，通过exchange路由器将不同的routing key消息投递到不同队列，从而分发给不同消费者。



## 消息不可靠

-   套接字write操作不可靠

-   网络故障

-   消费者宕机
-   kill-9

消息 → 套接字的缓存 → 通过网卡转发到链路 → 消费者套接字缓存 → read操作读消息



## 消息可靠

1.   server deliver后不删除

2.   client收到消息处理后回复ack

3.   server收到ack后删除消息
4.   没收到ack消息重新投递
5.   ack丢失会导致消息重复处理
6.   去重（幂等）由业务系统自己考虑

:bookmark:

![bookmark](RabbitMQ.assets/1f516



## Todo

-   延时队列
-   镜像队列
-   模式：
    -   消息可靠
    -   消息不可靠



