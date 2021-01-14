---
layout: wiki
title: 『Spring』
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



```xml
<!-- 使用 Annotation 自动注册 Bean，在主容器中不扫描 @Controller 注解，在 SpringMVC 中只扫描 @Controller 注解。-->
<context:component-scan base-package="com.funtl.my.shop">
    <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
```

```xml
<!-- 使用 Annotation 自动注册 Bean，在主容器中不扫描 @Controller 注解，在 SpringMVC 中只扫描 @Controller 注解。-->
<context:component-scan base-package="com.funtl.my.shop">
    <context:exclude-filter type="annotation" expression="org.springframework.stereotype.Controller"/>
</context:component-scan>
```