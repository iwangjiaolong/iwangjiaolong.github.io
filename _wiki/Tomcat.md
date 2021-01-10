---
layout: wiki
title: Tomcat
categories: Tomcat
description: Tomcat
keywords: Tomcat
---

# Q & A

## Tomcat控制台乱码问题

> ### Q：
>
> 控制台中 `Server` 、`Tomcat Localhost Log`、 `Tomcat Catalina Log` 乱码问题
>
> ![image-20210109225057638](https://i.loli.net/2021/01/11/JG4BSQXijWrZg5d.png)

> ### A：
>
> 1. 进入`tomcat`安装目录，打开`conf` / `logging.properties` 文件
>
> 2. 修改以下编码`UTF-8`为`GBK`
>
>    <img src="https://i.loli.net/2021/01/09/GJ9ZlUxR4fy5Es3.png" alt="image-20210109224635983" style="zoom: 80%;" />
>
> 3. 重启服务即可。
>
>    ![image-20210109225325580](https://i.loli.net/2021/01/11/lYHmaJtoEWiBbPg.png)

