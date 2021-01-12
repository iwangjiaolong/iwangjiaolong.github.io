---
layout: wiki
title: Spring
categories: Spring
description: Spring
keywords: Spring
---

# 一、Spring体系结构

![Spring的体系结构](https://i.loli.net/2021/01/08/omCJExvtg3FQ19f.gif)





# 二、Template

## spring-context.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">


</beans>
```

## web.xml

```xml
<context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:spring-context*.xml</param-value>
</context-param>
<listener>
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
</listener>
```





# 三、Spring注入Bean的方法

## 方法一：xml配置

```xml
<bean id="springContext" class="com.jiaolong.myshop.commons.context.SpringContext"/>
```

> 若使用此方法，`springContext`必须放置第一行，首先注入。

## 方法二：注解

**`spring-context.xml`**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

	<!--开启注解-->
    <context:annotation-config/>
    <context:component-scan base-package="com.jiaolong.name"/>
</beans>
```

| 注解             | 描述                                                         |
| ---------------- | ------------------------------------------------------------ |
| *`@Component`    | 需要在类上使用注解`@Component`，该注解的value属性用于指定该bean的id值。 |
| *`@Repository`   | 用于对Dao实现类进行注解                                      |
| *`@Service`      | 用于对Service实现类进行注解                                  |
| *`@Controller`   | 用于对Controller实现类进行注解                               |
| `@Scope`         | 需要在类上使用，其value属性用于指定作用域。默认为singleton。 |
| `@Value`         | 需要在属性上使用，该注解的value属性用于指定要注入的值。      |
| `@Autowired`     | 需要在域属性上使用，该注解默认使用`按类型自动装配Beam`的方式。 |
| `@Resource`      | 需要在域属性上使用，该注解有`name`属性，用于创建指定bean。如`@Resource(name="userService")` |
| `@PostConstruct` | 初始化方法                                                   |



> **注解与XML配置的区别：**
>
> - 注解的好处是配置方便，只管，但是以硬编码的方式写入到了Java代码中，其修改是需要重新编译代码的。
> - XML配置方式的最大好处是，对其所做修改，无需编译代码，只需重启服务器即可将新的配置加载。
> - 若注解与XML同用，XML的优先级高于注解。这样的好处是，需要对某个Bean做修改，只需修改配置文件即可。



# 四、SpringMVC

## 配置`web.xml`

###  CharacterEncodingFilter

> 配置字符集过滤器，用于解决中文编码问题

```xml
<filter>
    <filter-name>encodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
    <init-param>
        <param-name>forceEncoding</param-name>
        <param-value>true</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>encodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

###  DispatcherServlet

> 配置 Spring 的 Servlet 分发器处理所有 HTTP 的请求和响应

```xml
<servlet>
    <servlet-name>springServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <init-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>classpath*:/spring-mvc*.xml</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
    <servlet-name>springServlet</servlet-name>
    <url-pattern>/</url-pattern>
</servlet-mapping>
```

### 配置`spring-mvc.xml`

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd">

    <description>Spring MVC Configuration</description>

    <!-- 加载配置属性文件 -->
    <context:property-placeholder ignore-unresolvable="true" location="classpath:myshop.properties"/>

    <!-- 使用 Annotation 自动注册 Bean,只扫描 @Controller -->
    <context:component-scan base-package="com.lusifer.myshop" use-default-filters="false">
        <context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
    </context:component-scan>

    <!-- 默认的注解映射的支持 -->
    <mvc:annotation-driven />

    <!-- 定义视图文件解析 -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="${web.view.prefix}"/>
        <property name="suffix" value="${web.view.suffix}"/>
    </bean>

    <!-- 静态资源映射 -->
    <mvc:resources mapping="/static/**" location="/static/" cache-period="31536000"/>
</beans>
```

相关配置说明：

- `context:property-placeholder`：动态加载属性配置文件以变量的方式引用需要的值
- `context:component-scan`：当前配置文件为 MVC 相关，故只需要扫描包含 `@Controller` 的注解即可，由于 `spring-context.xml` 配置文件中也配置了包扫描，所以还需要排除 `@Controller` 的注解扫描。
- `InternalResourceViewResolver`：视图文件解析器的一种，用于配置视图资源的路径和需要解释的视图资源文件类型，这里有两个需要配置的属性 `prefix`（前缀）以及 `suffix`（后缀）。
  - `prefix`：配置视图资源路径，如：`/WEB-INF/views/`
  - `suffix`：配置视图资源类型，如：`.jsp`
- `mvc:resources`：静态资源映射，主要用于配置静态资源文件存放路径，如：JS、CSS、Image 等

### 系统相关配置

在 `spring-mvc.xnl` 中，我们配置了 `<context:property-placeholder ignore-unresolvable="true" location="classpath:myshop.properties"/>` 用于动态加载属性配置文件，实际开发中我们会将系统所需的一些配置信息封装到 `.properties` 配置文件中便于统一的管理。

创建一个名为 `myshop.properties` 的配置文件，内容如下：

```properties
#============================#
#==== Framework settings ====#
#============================#

# \u89c6\u56fe\u6587\u4ef6\u5b58\u653e\u8def\u5f84
web.view.prefix=/WEB-INF/views/
web.view.suffix=.jsp
```

### 去掉 Spring 配置的重复扫描

由于 `spring-mvc.xml` 中已经配置了 `@Controller` 注解的扫描而 `spring-context.xml` 中配置的是扫描全部注解，故在这里需要将 `@Controller` 注解的扫描配置排除。

修改 `spring-context.xml` 配置：

```xml
<!-- 使用 Annotation 自动注册 Bean，在主容器中不扫描 @Controller 注解，在 SpringMVC 中只扫描 @Controller 注解。-->
<context:component-scan base-package="com.funtl.my.shop">
    <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
```