---
layout: wiki
title: 「 SpringMVC 」
categories: SpringMVC
description: SpringMVC
keywords: SpringMVC
---

## 概述

Spring MVC 也叫 Spring Web MVC ，属于展示层框架。SpringMVC 是 Spring 框架的一部分。

Spring Web MVC 框架提供了 MVC (模型 - 视图 - 控制器) 架构和用于开发灵活和松散耦合的 Web 应用程序的组件。 MVC 模式导致应用程序的不同方面(输入逻辑，业务逻辑和 UI 逻辑)分离，同时提供这些元素之间的松散耦合。

- 模型 (Model)：封装了应用程序数据，通常它们将由 POJO 类组成。
- 视图 (View)：负责渲染模型数据，一般来说它生成客户端浏览器可以解释 HTML 输出。
- 控制器 (Controller)：负责处理用户请求并构建适当的模型，并将其传递给视图进行渲染。

## DispatcherServlet 组件类

Spring Web MVC 框架是围绕 DispatcherServlet 设计的，它处理所有的 HTTP 请求和响应。 Spring Web MVC DispatcherServlet 的请求处理工作流如下图所示：

![20151003165041682](https://i.loli.net/2021/01/20/sMnapUmA8OGx32W.png)

以下是对应于到 DispatcherServlet 的传入 HTTP 请求的事件顺序：

- 在接收到 HTTP 请求后，DispatcherServlet 会查询 HandlerMapping 以调用相应的 Controller。
- Controller 接受请求并根据使用的 GET 或 POST 方法调用相应的服务方法。 服务方法将基于定义的业务逻辑设置模型数据，并将视图名称返回给 DispatcherServlet。
- DispatcherServlet 将从 ViewResolver 获取请求的定义视图。
- 当视图完成，DispatcherServlet 将模型数据传递到最终的视图，并在浏览器上呈现。

所有上述组件，即: HandlerMapping，Controller 和 ViewResolver 是 WebApplicationContext 的一部分，它是普通 ApplicationContext 的扩展，带有 Web 应用程序所需的一些额外功能。

# 一、SpringMVC

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

###  系统相关配置

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

###   去掉 Spring 配置的重复扫描

由于 `spring-mvc.xml` 中已经配置了 `@Controller` 注解的扫描而 `spring-context.xml` 中配置的是扫描全部注解，故在这里需要将 `@Controller` 注解的扫描配置排除。

修改 `spring-context.xml` 配置：

```xml
<!-- 使用 Annotation 自动注册 Bean，在主容器中不扫描 @Controller 注解，在 SpringMVC 中只扫描 @Controller 注解。-->
<context:component-scan base-package="com.funtl.my.shop">
    <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
```

# 二、SpringMVC拦截器

###  在 `spring-mvc.xml` 中配置拦截器

```text
<!-- 拦截器配置，拦截顺序：先执行后定义的，排在第一位的最后执行。-->
<mvc:interceptors>
    <mvc:interceptor>
        <mvc:mapping path="/**"/>
        <mvc:exclude-mapping path="/static/**"/>
        <mvc:exclude-mapping path="/login"/>
        <bean class="com.funtl.my.shop.web.interceptor.LoginInterceptor"/>
    </mvc:interceptor>
</mvc:interceptors>
```



相关配置说明：

- `mvc:interceptor` ：定义一个拦截器
  - `mvc:mapping`：映射路径，需要拦截的请求路径
  - `mvc:exclude-mapping`：需要排除的请求路径，比如登录页本身是不需要拦截的，这里还包括了静态资源路径也是不需要拦截的
  - `bean class`：配置指定的拦截器对象