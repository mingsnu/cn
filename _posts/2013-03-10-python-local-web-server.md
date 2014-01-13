---
title: 用Python创建本地web服务器
layout: post
categories:
  - 技术笔记
tags:
  - python
  - 服务器
  - 本地
---
创建本地web服务器最简单的办法之一就是用Python提供的`SimpleHTTPServer`函数，例如：

{% highlight python %}
python -m SimpleHTTPServer 8888
{% endhighlight %}

可以创建一个端口为`8888`的本地web服务器(在浏览器中输入`http://localhost:8888`查看)

需要注意的是所建的服务器的根目录默认为当前运行`python`命令的目录。
