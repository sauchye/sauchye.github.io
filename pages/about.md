---
layout: page
title: About
description: About Sauchye
keywords: sauchye
comments: true
menu: 关于
permalink: /about/
---

嗨！你好呀，我是叶秀昌 (@Sauchye)，现居深圳，iOS开发者，正在努力前行。

## 联系

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## Skill Keywords

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}