---
layout: default
title: Github Pages 和 Jekyll 入门
date: 2018-10-10
author: HAO Xuguang
---

<h1>{{ page.title }}</h1>
<p>{{ page.author }}</p>
<p>{{ page.date }}</p>

<!-- TOC -->autoauto- [1. 创建项目](#1-创建项目)auto- [2. clone 项目到本地](#2-clone-项目到本地)autoauto<!-- /TOC -->

[Jekyll](https://jekyllrb.com/)（发音/'dʒiːk əl/，"杰克尔"）是一个静态站点生成器，它会根据网页源码生成静态文件。它提供了模板、变量、插件等功能，所以实际上可以用来编写整个网站。

# 1. 创建项目

在 Github 上创建名为 username.github.io 的 repository. 其中, _username_ 是 Github 上的用户名.
<!--
在项目的 _Settings_ 中的 _GitHub Pages_ 栏下点击 _Choose theme_, 选择一个 theme.
则 Github 自动在项目中插入 __config.yml_ 文件.
例如, 选择了 _Architect_ 主题后, 其内容为:
```
theme: jekyll-theme-architect
```
-->

# 2. clone 项目到本地
```bash
git clone git@github.com:username/username.github.io.git
```

# 3. 添加配置文件

创建空的 __config.yml_ 文件

```yml
asdfjsoaeir
```

# 4. 创建 layout

创建 文件夹 __layouts_.
在目录中创建 _default.html_. 其内容如下:
```html
<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="content-type" content="text/html; charset=utf-8" />
        <title>{{ page.title }}</title>
    </head>
　　<body>

        {{ content }}

    </body>
</html>
```

# 5. 创建 posts

创建文件夹 __posts_
在其下创建第一个post
```html
---
layout: default
title: 你好，世界
---

<h2>{{ page.title }}</h2>
<p>我的第一篇文章</p>
<p>{{ page.date | date_to_string }}</p>
```

# 创建 index.html

_index.html_ 的内容如下:
```html
---
layout: default
title: 我的Blog
---

<h2>{{ page.title }}</h2>
<p>最新文章</p>
<ul>
    {% for post in site.posts %}
        <li>{{ post.date | date_to_string }} <a href="{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
</ul>
```

# Jekyll博客安卓客户端

[知乎](https://zhuanlan.zhihu.com/p/27507830)
[GitHub](https://github.com/tsangiotis/JekyllForAndroid)