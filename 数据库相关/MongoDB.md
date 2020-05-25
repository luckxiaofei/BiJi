## 优缺点

#### 与关系型数据库相比，MongoDB的优点：

> ①弱一致性（最终一致），更能保证用户的访问速度：
>
> ②文档结构的存储方式，能够更便捷的获取数据。
>
> ③内置GridFS，支持大容量的存储。
>
> ④内置Sharding。
>
> >Sharding的基本思想就要把一个数据库切分成多个部分放到不同的数据库(server)上，从而缓解单一数据库的性能问题
>
> ⑤第三方支持丰富。(这是与其他的NoSQL相比，MongoDB也具有的优势)
>
> ⑥性能优越：

#### 与关系型数据库相比，MongoDB的缺点：

>  ①mongodb不支持事务操作。
>
>  ②mongodb占用空间过大。(消耗内存)
>
>  ③MongoDB没有如MySQL那样成熟的维护工具，这对于开发和IT运营都是个值得注意的地方。 

******

## 应用场景

- 游戏场景，使用 MongoDB 存储游戏用户信息，用户的装备、积分等直接以内嵌文档的形式存储，方便查询、更新
- 物流场景，使用 MongoDB 存储订单信息，订单状态在运送过程中会不断更新，以 MongoDB 内嵌数组的形式来存储，一次查询就能将订单所有的变更读取出来。
- 社交场景，使用 MongoDB 存储存储用户信息，以及用户发表的朋友圈信息，通过地理位置索引实现附近的人、地点等功能
- 物联网场景，使用 MongoDB 存储所有接入的智能设备信息，以及设备汇报的日志信息，并对这些信息进行多维度的分析
- 视频直播，使用 MongoDB 存储用户信息、礼物信息等

![image-20180911105433716](/var/folders/sy/_bmnr14x5298s4lkwqjvvtw80000gn/T/abnerworks.Typora/image-20180911105433716.png)

如果上述有1个 Yes，可以开始考虑 MongoDB。



## MongoDB语法

```sql
查询
例如： 查询条件onumber="002"
mongoTemplate.find (new Query(Criteria.where("onumber").is("002")),entityClass)

多个条件组合查询时：
例如：onumber="002" and cname="zcy"
mongoTemplate
.find (new Query(Criteria.where("onumber").is("002").and("cname").is("zcy")),entityClass)

例如：onumber="002" or cname="zcy"
mongoTemplate
.findOne(new Query(new Criteria().orOperator(Criteria.where("onumber").is("002"),Criteria.where("cname").is("zcy"))),entityClass); 

```

