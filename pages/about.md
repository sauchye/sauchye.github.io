---
layout: page
title: About
description: About Sauchye
keywords: sauchye
comments: true
menu: 关于
permalink: /about/
---

嗨！你好呀，很高兴在这里遇见你:)，我是scy (@Sauchye)，现居深圳，iOS开发，正在努力前行，喜欢尝试一些新事物。

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