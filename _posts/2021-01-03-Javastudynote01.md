---
layout: post
title: Java单体应用（一）
categories: Java学习笔记
description: some word here
keywords: Java
topmost:false
---


> 有道无术，术尚可求，有术无道，止于求     ——道德经 
> 最有效的教育方法不是告诉人们答案，而是向他们提问。——苏格拉底

 要有批判性思维，

 面向对象的设计原则

![Untitled.png](https://i.loli.net/2021/01/03/Y9uL26zhnHpSy7U.png)

 产品创新思维的三重境界

 - 看山是山：学会借用，看山是山看的是山的本身，是现象
 - 看山不是山：学会遗忘，看山不是山看的是山背后的道理，是本质
 - 看山还是山：学会学习，看山还是山看的是现象和本质的统一是融会贯通

 开发工具：Eclipse、MyEclipse、Spring STS、IntelliJ IDEA

# 第 01 章 使用IDEA



# 第 02 章 使用Maven构建应用

 ```xml
<?xml version="1.0" encoding="UTF-8" ?>
<web-app xmlns="<http://xmlns.jcp.org/xml/ns/javaee>"
          xmlns:xsi="<http://www.w3.org/2001/XMLSchema-instance>"
          xsi:schemaLocation="<http://xmlns.jcp.org/xml/ns/javaee> <http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd>"
          version="4.0">
 </web-app>
 ```

------



> 错误：请使用5，6以上

 ```xml
<properties>
     <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
     <maven.compiler.encoding>UTF-8</maven.compiler.encoding>
     <java.version>11</java.version>
     <maven.compiler.source>11</maven.compiler.source>
     <maven.compiler.target>11</maven.compiler.target>
</properties>
 ```



# 第 03 章 三层架构 + MVC

##  三层架构

### 什么是系统架构

所谓系统架构是指，整合应用系统程序大的结构。经常提到的系统结构有两种:三层架构与MVC。这两种结构既有区别，又有联系。但这两种结构的使用，均是为了降低系统模块间的耦合度。

### 什么是三层架构

三层架构是指：视图层View、服务层Service、持久层Dao，他们分别完成不同的功能。

- View层：用于接收用户提交请求的代码
- Service：系统的业务逻辑主要在这里完成
- DAO层：直接操作数据据库代码

为了更好的降低各层间的耦合度，在三层架构程序设计中，采用面向抽象编程。即上层对下层的调用，是通过接口实现的。而下层对上层的真正服务提供者，是下层接口的实现类。服务标准（接口)是相同的，服务提供者（实现类)可以更换。这就实现了层间解耦合。

![image-20210103115212314](https://i.loli.net/2021/01/03/GWJmfdMUCQxtqaL.png)





## MVC模式

### 什么是MVC模式

MVC，即 Model模型、View视图，及 Controller控制器。

- View :视图，为用户提供使用界面，与用户直接进行交互。

- Model :模型，承载数据，并对用户提交请求进行计算的模块。其分为两类，一类称为数据承载Bean，一类称为业务处理Bean。所谓数据承载 Bean是指实体类，专门用户承载业务数据的，如Student、User等。而业务处理Bean则是指Service或 Dao 对象，专门用于处理用户提交请求的。
- Controller:控制器，用于将用户请求转发给相应的Model进行处理，并根据Model的计算结果向用户提供相应响应。

### MVC架构程序的工作流程

- 用户通过View页面向服务端提出请求，可以是表单请求、超链接请求、AJAX请求等
- 服务端Controller控制器接收到请求后对请求进行解析，找到相应的 Model对用户请求进行处理。 Model处理后，将处理结果再交给Controller
- Controller在接到处理结果后，根据处理结果找到要作为向客户端发回的响应View页面。页面经渲染(数据填充)后，再发送给客户端。

![MVC架构](https://i.loli.net/2021/01/03/mlXqnhEVAfTbwIg.png)

![三层架构+MVC示意图](https://i.loli.net/2021/01/03/5qSrfOZ7l28G93R.png)