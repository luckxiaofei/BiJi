# spring mvc

1. **初始化 DispatcherServlet**

   方式一：以xml的形式，在web.xml文件中配置

   ```xml
   	<servlet>
   		<servlet-name>mvc-dispatcher</servlet-name>
   		<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
   		<!-- 配置springMVC需要加载的配置文件
   			spring-dao.xml,spring-service.xml,spring-web.xml
   			Mybatis - > spring -> springmvc
   		 -->
   		<init-param>
   			<param-name>contextConfigLocation</param-name>
   			<param-value>classpath*:spring/spring-*.xml</param-value>
   		</init-param>
   	</servlet>
   	<servlet-mapping>
   		<servlet-name>mvc-dispatcher</servlet-name>
   		<!-- 默认匹配所有的请求 -->
   		<url-pattern>/</url-pattern>
   	</servlet-mapping>
   ```

   

   方式二：以java代码的形式配置

```java
import org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;

import spittr.web.WebConfig;

public class SpitterWebInitializer extends AbstractAnnotationConfigDispatcherServletInitializer {

  @Override
  protected Class<?>[] getRootConfigClasses() {
    return new Class<?>[] { RootConfig.class };
  }

  @Override
  protected Class<?>[] getServletConfigClasses() {
    return new Class<?>[] { WebConfig.class };
  }

  @Override
  protected String[] getServletMappings() {
    return new String[] { "/" };
  }

}
```

