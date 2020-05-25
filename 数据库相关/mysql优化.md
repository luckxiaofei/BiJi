# mysql优化--思索总结

****

## 背景：

最近在公司遇到一个业务场景的查询优化，也就2000条的数据查询竟然要两分多种（慢出天际），但是这条sql业务上也没有什么错误。于是苦事冥想开始想怎么优化它！同时做个笔记，加强记忆。

******

想要优化一条sql首先得知道 它的基本执行时怎么样？

##sql的解析顺序

```sql
select [distinct]  
from
left join  
on  
where  
group by  
having  
union  
order by  
limit  
```

上面是一条查询sql的基本语法，下面就是mysql的对这个条查询sql的执行顺序

* 执行 FROM 语句，

  mysql是从左往右执行，oracle是从右往左执行， SQL语句的执行过程中，都会产生一个虚拟表，用来保存SQL语句的执行结果（这是重点），执行from语句之后会产生一个虚拟表暂时叫VT1（vitual table 1），VT1是根据笛卡尔积生成（注：个人理解笛卡尔积 就是两个集合相乘的结果）

* 执行on进行过滤 

  >根据on后面的条件过滤掉不符合条件的数据，产生VT2

* 执行链接的类型

  > inner join内连接、left join左链接、right右链接、outer join 外链接、full outer join 全连接
  >
  > 执行完产生VT3

* 执行where后面的条件 

  >这时候使用WHERE条件的时候要注意：不能使用组函数、并且字段的别名不能放到条件中使用
  >
  >例如SELECT city as c FROM t WHERE c='shanghai'

* 执行group by 进行分组

* 执行having过滤

  >HAVING`子句主要和`GROUP BY子句配合使用，having后面可以跟组函数的条件

* 执行select

* 执行distinct，去掉重复的数据

* 执行order by 语句排序

* 执行分页语句

```sql
from    
on 
join
where  
group by  
having  
select  
distinct  
union  
order by  
```

这里就基本能知道sql是怎么执行的了。

但是这样还是不够直观，对于定位低效率的sql语句帮助不是很明显，那么查看***执行计划***是个好办法。

####查看执行计划：

```
EXPLAIN
```

只用把这个关键词放在sql语句的前面即可，效果如下：

![image-20180825173048716](/var/folders/1j/1lyzlyld1pq_3wlxbp_w47t00000gn/T/abnerworks.Typora/image-20180825173048716.png)

>explain的列解释：
>
>* id：代表执行顺序 ,id值相同执行顺序从上到下，id值相同执行顺序从上到下。
>
>* select_type：代表对应行是简单还是复杂SELECT。
>
>  SIMPLE：不包含子查询/union操作的查询
>
>  PRIMARY：查询中如果包含了子查询，那么外层的查询标记为PRIMARY
>
>  SUBQUERY：select列表的中的子查询
>
>  DEPENDEN SUBQUERY：依赖外部结果的子查询
>
>* table：输出数据行所在的表名
>
>* PARTITIONS：对于分区表，显示查询的分区ID，对于非分区表，显示为NULL
>
>* type：这是重要的列,显示连接使用了何种类型。从最好到最差的连接类型为const、eq_reg、ref、range、index和ALL
>
>* possible_keys：显示可能应用在这张表中的索引。如果为空，没有可能的索引。
>
>* key:实际使用的索引。如果为NULL，则没有使用索引。
>
>* key_len:使用的索引的长度。在不损失精确性的情况下，长度越短越好。
>
>* ref:显示索引的哪一列被使用了,如果可能的话，是一个常数
>
>* rows：MYSQL认为必须检查的用来返回请求数据的行数，ROWS值的大小是个统计抽样结果，并不十分准确
>
>* Filtered：表示返回结果的行数占需读取行数的百分比，Filter列的值越大越好
>
>* extra：包含查询mysql解决查询的详细信息。

到这里一个sql语句出来，那么可很直观的定位出哪里太慢了？有没有用到索引？用了那个索引？等等

接下里就可以把一些sql技巧开始应用起来了

#### sql技巧：

* 避免SELECT *，

* 越小的列会越快

* 避免多个范围条件

>实际开发中，我们会经常使用多个范围条件，比如想查询某个时间段内登录过的用户：
>
>```slq
>select user.* from user where login_time > '2017-04-01' and age between 18 and 30;
>```
>
>这个查询有一个问题：它有两个范围条件，login_time列和age列，MySQL可以使用login_time列的索引或者age列的索引，但无法同时使用它们。

* 待完善………………

###MySQL查询过程

![image-20180825190240127.png](https://upload-images.jianshu.io/upload_images/11793647-912a1f61dc64794f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

