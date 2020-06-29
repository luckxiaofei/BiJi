# kafka学习

## 1、简介

kafka是一个分布式、分区的、多副本的、多订阅者，基于zookeeper协调的分布式日志系统（也可以当做MQ系统）

##2、应用场景

a、日志收集系统

b、消息系统

c、用户活动跟踪

d、运营指标

## 3、模式

a、点对点传递模式

> 生产者生产一条数据，消息只能被消费一次，消息被消费之后会从队列中删除。
>
> 好处：即使有多个消费者同时消费数据，也能保证数据的处理顺序。



b、发布-订阅模式

> 生产者发布消息到 topic中 ，然后有订阅的该topic的消费者，自动消费。
>
> 类似于：微信公众号



| **名词**      | **解释**                                                     |
| ------------- | ------------------------------------------------------------ |
| Producer      | 消息的生成者                                                 |
| Consumer      | 消息的消费者                                                 |
| ConsumerGroup | 消费者组，可以并行消费Topic中的partition的消息               |
| Broker        | 缓存代理，Kafka集群中的一台或多台服务器统称broker.           |
| Topic         | Kafka处理资源的消息源(feeds of messages)的不同分类           |
| Partition     | Topic物理上的分组，一个topic可以分为多个partion,每个partion是一个有序的队列。partion中每条消息都会被分                配一个 有序的Id(offset) |
| Message       | 消息，是通信的基本单位，每个producer可以向一个topic（主题）发布一些消息 |
| Producers     | 消息和数据生成者，向Kafka的一个topic发布消息的 过程叫做producers |
| Consumers     | 消息和数据的消费者，订阅topic并处理其发布的消费过程叫做consumers |

![img](http://kafka.apachecn.org/10/images/log_anatomy.png)