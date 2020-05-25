## 杂记

```java
//基本数据类型
byte、short、int、long
float、double
char
boolean
```

```java
//==和equals的区别
基本数据类型 == 比较的是值，没有equals方法
object类 equals方法 实际上还是用了 == 进行比较
引用数据类型 == 比较对象，内存地址
引用数据类型都重写了 equals方法，
String 先比较对象，然后比较字符串
其他引用数据类型，先判断是否是引用数据类型，然后拆箱为基本数据类型 用==比较值
```









集合

集合不能直接遍历然后 remove，要通过迭代器遍历，remov才行 



##    1、对象锁

​     包括方法锁（默认锁对象为this当前实例对象）和同步代码块锁（自己指定锁对象）

##    2、类锁

​     指定synchronize修饰静态的方法或指定锁为class对象

