---
layout: post
title: Jekyll 模板引擎简介
categories: [Blog, Jekyll]
description: 简单来说，Jekyll 就是一个简单的、可扩展的静态网站生成器。
keywords: Blog, Jekyll
topmost: true
---

> [Jekyll](https://jekyllrb.com/docs/) is a simple, extendable, static site generator. 
You give it text written in your favorite markup language 
and it churns through layouts to create a static website. 
Throughout that process you can tweak how you want the site URLs to look, 
what data gets displayed in the layout, and more.

{% raw %}
## Jekyll是什么
简单来说，Jekyll 是一个简单的、可扩展的静态网站生成器。Jekyll 有着特定的模板目录结构，我们只要选择一种我们喜欢的标记语言，专注于写好每一篇文档，并将它们保存到指定的目录中，Jekyll 就会自动把这些文档编译为特定布局的页面，在网站中进行展示。在掌握 Jekyll 基本结构和语法的基础上，我们还可以对网站的外观和行为进行一些个性化配置。

## 环境准备与安装
Gem 可以理解为封装一定功能的 Ruby 代码包，Jekyll 也是一个 Gem。因此要安装 Jekyll，首先要安装 Ruby 和 RubyGems（Ruby 的包管理框架）。
所以安装顺序为：
1. Ruby 
2. RubyGems
3. Jekyll

不同操作系统下的具体安装和配置方式请自行 Google。

## Jekyll 目录结构
安装 jekyll 后就可以利用 jekyll 命令创建静态站点（`jekyll new myblog`）了，以下是由 Jekyll 生成的一个站点的基本目录结构：
```
.
├── _config.yml
├── _data
|   └── members.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.md
|   └── on-simplicity-in-technology.md
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.md
|   └── 2009-04-26-barcamp-boston-4-roundup.md
├── _sass
|   ├── _base.scss
|   └── _layout.scss
├── _site
├── .jekyll-metadata
└── index.html # can also be an 'index.md' with valid front matter
```
+ _config.yml

Jekyll 的全局配置文件。
+ _drafts

存放未发表的博客，博客文件命名格式：`title.MARKUP`。
+ _includes

存放页面可重用的部分，比如存在 `_includes/file.ext`，在需要的地方用 Liquid 标签 `{% include file.ext %}` 就可以引入这个片段。
（关于 Liquid 的语法，本文后面会有简单介绍。）

+ _layouts

存放网页模板布局，我们只要在文本页面中通过特定格式指定所用的模板，页面就会被渲染成模板对应形式的页面。
在模板中，对使用此模板的页面内容进行引用的占位符为 `{{ content }}`。
+ _posts

存放发表的博客，博客文件命名格式：`YEAR-MONTH-DAY-title.MARKUP`。
+ _data

存放一些标准格式化的配置，页面中可以通过 `site.data.文件名` 的形式访问。
+ _site

存放 Jekyll 编译生成的静态站点，建议加到 `.gitignore` 中忽略。
+ .jekyll-metadata

记录 Jekyll 最近一次编译以来哪些文件是变化的，这样下次编译时就可以只编译变化的部分，提高编译效率，
建议加到 `.gitignore` 中忽略。

## Liquid 语法
Liquid 是一种开源的模板语言，Jekyll 使用 Liquid 作为模板引擎，构建静态站点页面。在 Liquid 语言中，主要包含三类元素：对象（Objects）、
标签（Tags）和过滤器（Filters）。`{{ variable }}` 表示输出一个变量的内容，`{{ variable | filter1 | filter2 }}` 表示输出一个对象进行 filter1 和 filter2 两级过滤后的内容，`{% expression %}` 表示执行一个逻辑表达式。Liquid 支持的主要标签有：注释、变量定义和运算、
条件判断和循环遍历，使用方式如下：

```$xslt
# 注释
{% comment %}
add your comment here
{% endcomment %}

# 变量定义
{% assign gender="female" %}

# 条件判断
{% if gender='female' %}
女
{% elsif gender='male' %}
男
{% else %}
其它
{% endif %}
```
除了 Liquid 语言定义的语法外，Jekyll 为方便构建站点也扩展了一些自己的过滤器和标签。

## 内置配置
为了灵活定制站点的构建方式，Jekyll 提供了很多不同种类的配置项。这些配置项既可以在根目录的 _config.yml 中进行配置，也可以在以 Jekyll 命令行选项的方式指定。这些配置信息主要包括一下几类（具体有哪些配置详见 [Jekyll 官网](https://jekyllrb.com/docs/configuration/)）：
1. Jekyll 配置
2. Front Matter 默认配置
3. 环境配置
4. Markdown 配置
5. Liquid 配置
6. Webrick 配置
7. 增量重生成配置

对于一些常用的配置项，Jekyll 都提供了默认值。如果我们没有特殊配置，Jekyll 将按默认配置进行编译。这样，我们就可以仅针对我们关心的内容进行配置，就能达到不错的编译效果。

## 头信息和默认值
在每个页面文件的最上方，有一块由两组`---`包围的区域，称为 Front Matter。在 Front Matter 的内部，可以按照 YAML 语法
对一些预定义变量（包括全局变量或 Posts 专用变量）的赋值或自定义一些变量。然后，就可以利用 Liquid 标签在当前页面文件、文件引用的 layouts 
或文件包含的 includes 中访问到这些变量。具体使用方式如下：
```$xslt
---
# 预定义全局变量
layout: post # 布局
permalink: /:categories/:year/:month/:title.html # 永久链接
published: true # 是否发布

# 预定义Posts变量
categories: [Cat1, Cat2] # 不用目录情况下的分类管理
date: 2019-01-01 00:00:00 # 

# 自定义变量
title: This is a title
keywords: key1, key2
description: Here is the description.
---
```

## 数据文件
Jekyll 支持从 YAML、JSON 和 CSV 等文件中加载数据，利用这个特性，可以在不改变 _config.yml 的情况下有效避免模板内容的重复或改变站点配置选项。假设 _data 目录下存在文件 members.yml：
```$xslt
- name: Eric Mill
  github: konklone

- name: Parker Moore
  github: parkr
```
在模板中就可以通过 `site.data.members` 访问这些数据：
```$xslt
<ul>
{% for member in site.data.members %}
  <li>
    <a href="https://github.com/{{ member.github }}">
      {{ member.name }}
    </a>
  </li>
{% endfor %}
</ul>
```
## Includes 和 Layouts
对于一些**重复被使用的页面元素**，比如 header、footer 和 sidebar 等，可以单独抽取出来存储为 _includes 目录下的一个个独立的页面元素文件。
当页面需要用到这些元素时，通过 include 标签引入即可，如 `{% include footer.html %}`。

对于一些**布局相同仅仅内容不同的页面**，比如每篇博客除了博客内容不同外，其它部分都是相同的，可以把相同的部分抽取出来存储为 _layouts 
目录下的一个个独立的页面布局文件。在需要采用这种布局的页面中，通过 Front Matter 的形式指定所用的布局结构，如 `layout: post`。
## 静态文件
静态文件指的是项目中那些无法包含 Front Matter 的，不被 Jekyll 渲染的文件，比如图片、PDF 文档等。虽然这些文件本身不能直接添加 Front Matter，
我们依然可以通过在全局配置文件中为其配置 Front Matter 默认值。
在项目中，可以通过 `site.static_files` 访问到这些静态文件。对于每个静态文件，都包含了 `file.path`，`file.modified_time`，`file.name`,
`file.basename`，`file.extname` 这些元属性。

{% endraw %}