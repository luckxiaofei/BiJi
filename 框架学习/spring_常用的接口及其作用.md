## 常用的接口及其作用

```java
ApplicationContextAware
  作用：spring启动时，会扫描实现了该接口的bean，然后把上下文（ApplicationContext）注入进来。

BeanPostProcessor
  作用：每个bean实例化完成之后，都会调用该接口的方法

ApplicationListener
  作用：每当ApplicationContext发布ApplicationEvent时，ApplicationListener Bean将自动被触发
  >>>
  
 
  
InvocationHandler
  作用：代理接口
  
InitializingBean
  作用：bean初始化时执行


```





> 1	
> ContextRefreshedEvent
>
> ApplicationContext 被初始化或刷新时，该事件被发布。这也可以在 ConfigurableApplicationContext接口中使用 refresh() 方法来发生。此处的初始化是指：所有的Bean被成功装载，后处理Bean被检测并激活，所有Singleton Bean 被预实例化，ApplicationContext容器已就绪可用
>
> 2	
> ContextStartedEvent
>
> 当使用 ConfigurableApplicationContext （ApplicationContext子接口）接口中的 start() 方法启动 ApplicationContext 时，该事件被发布。你可以调查你的数据库，或者你可以在接受到这个事件后重启任何停止的应用程序。
>
> 3	
> ContextStoppedEvent
>
> 当使用 ConfigurableApplicationContext 接口中的 stop() 停止 ApplicationContext 时，发布这个事件。你可以在接受到这个事件后做必要的清理的工作。
>
> 4	
> ContextClosedEvent
>
> 当使用 ConfigurableApplicationContext 接口中的 close() 方法关闭 ApplicationContext 时，该事件被发布。一个已关闭的上下文到达生命周期末端；它不能被刷新或重启。
>
> 5	
> RequestHandledEvent
>
> 这是一个 web-specific 事件，告诉所有 bean HTTP 请求已经被服务。只能应用于使用DispatcherServlet的Web应用。在使用Spring作为前端的MVC控制器时，当Spring处理用户请求结束后，系统会自动触发该事件。