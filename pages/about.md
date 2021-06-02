---
layout: page
title: About
description: 打码改变世界
keywords: mowenliunian, 莫问流年
comments: true
menu: 关于
permalink: /about/
---

我是莫问流年，一个普普通通的「码农」。

编码是我的工作，也塑造了我的思维模型，改变着我的生活。

## 联系

{% for website in site.data.social %}
{% if website.type == 'link' %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% else %}
* {{ website.sitename }}：*{{ website.name }}*
{% endif %}
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
