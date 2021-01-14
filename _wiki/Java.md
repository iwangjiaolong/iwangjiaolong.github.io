---
layout: wiki
title: 「 Java 」
categories: Java
description: Java
keywords: Java
---

# Java基础

## 基本数据类型

> Java语言提供了八种基本类型。六种数字类型（四个整数型，两个浮点型），一种字符类型，还有一种布尔型。

| 类型    | 位   | 字节 | 表示范围         | 默认值  | 例                  |
| ------- | ---- | ---- | ---------------- | ------- | ------------------- |
| byte    | 8    | 1    | (-2^7 , 2^7-1)​   | 0       | `byte b = 10;`      |
| short   | 16   | 2    | (-2^15 , 2^15-1)​ | 0       | `short s = 10;`     |
| int     | 32   | 4    | (-2^31 , 2^31-1) | 0       | `int i = 10;`       |
| long    | 64   | 8    | (-2^63 , 2^63-1) | 0L      | `long l = 10l;`     |
| float   | 32   | 4    | (-2^31 , 2^31-1) | 0.0f    | `float f = 10.0f;`  |
| double  | 64   | 8    | (-2^63 , 2^63-1) | 0.0d    | `double d = 10.0d;` |
| boolean | 1    | 8    | `true`、`false`  | `false` | `boolean b = true;` |
| char    | 16   | 2    |                  | 空      | `char c = 'c';`     |

Q & A

> Q：为什么表示范围要减1，
>
> A：因为最高位为符号位。

> https://www.docin.com/p-109442587.html



