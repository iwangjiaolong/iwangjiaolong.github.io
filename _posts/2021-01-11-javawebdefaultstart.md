---
layout: post
title: Web项目默认打开'index.jsp'文件
categories: [JavaWeb,Tomcat]
description: Web项目默认打开'index.jsp'文件
keywords: JavaWeb,Tomcat
topmost: false
---

> 在JavaWeb项目里，启动项目时，会默认打开`index.jsp`或`index.html`。

# 原因：

tomcat启动时，会首先读取自带的web.xml文件（`tomcat`/`conf`/`web.xml`），该文件中存在以下配置

![image-20210111094338872](https://i.loli.net/2021/01/11/kxutNe2IL9Ep6O8.png)

根据注释：

```xml
  <!-- ==================== Default Welcome File List ===================== -->
  <!-- When a request URI refers to a directory, the default servlet looks  -->
  <!-- for a "welcome file" within that directory and, if present, to the   -->
  <!-- corresponding resource URI for display.                              -->
  <!-- If no welcome files are present, the default servlet either serves a -->
  <!-- directory listing (see default servlet configuration on how to       -->
  <!-- customize) or returns a 404 status, depending on the value of the    -->
  <!-- listings setting.                                                    -->
  <!--                                                                      -->
  <!-- If you define welcome files in your own application's web.xml        -->
  <!-- deployment descriptor, that list *replaces* the list configured      -->
  <!-- here, so be sure to include any of the default values that you wish  -->
  <!-- to use within your application.                                      -->
```



> 当请求URI指向一个目录时，默认的servlet会查看该目录中的`welcome file`，如果存在，就会显示相应URL的资源。如果不存在，默认的servlet则会提供一个默认目录列表或返回404状态，这取决于列表的值。
>
> 如果你在自己项目里的`web.xml`中定义`welcome file`部署，该列表会取代默认配置的列表，因此，请确保在你项目里包含默认设置的值。

即当我们没有设置该配置时，会默认使用tomcat自带的配置，自己手动设置该配置可替代默认值。          