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

曾经的我，只追求「走马观花」，去获得表面的一知半解。

现在的我，更坚信「真正的聪明人，都在下笨功夫」。

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
