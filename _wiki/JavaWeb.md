---
layout: wiki
title: - JavaWeb -
categories: JavaWeb
description: JavaWeb
keywords: Java
---

# Template

## 完整项目目录结构

![image-20210104081421602](https://i.loli.net/2021/01/04/8UuOJNQ1pEf3Thm.png)



## web.xml

~~~xml
<?xml version="1.0" encoding="UTF-8" ?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
</web-app>
~~~



## Servlet配置web.xml

~~~xml
<servlet>
    <servlet-name></servlet-name>
    <servlet-class></servlet-class>
</servlet>
<servlet-mapping>
    <servlet-name></servlet-name>
    <url-pattern></url-pattern>
</servlet-mapping>
~~~



## Jstl

```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```