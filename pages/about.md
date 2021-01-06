---
layout: page
title: About
description: Stay Hungry, Stay Foolish.
keywords: Jiaolong
comments: true
menu: 关于
permalink: /about/
---

我是Jiaolong

一个不懂艺术的艺术家

一个还没想好做什么的个人开发者

一个正在成长的程序员

## 联系

<ul>
{% for website in site.data.social %}
<li>{{website.sitename }}：<a href="{{ website.url }}" target="_blank">@{{ website.name }}</a></li>
{% endfor %}
{% if site.url contains 'jiaolong.space' %}
<li>
<img style="height:192px;width:192px;border:1px solid lightgrey;" src="{{ assets_base_url }}/assets/images/qrcode.jpg"/>
</li>
{% endif %}
</ul>


## Skill Keywords

{% for skill in site.data.skills %}
### {{ skill.name }}
<div class="btn-inline">
{% for keyword in skill.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
