---
title: HTML5幻灯片
layout: post
categories: [小想法]
tags: [html5, R, reveal.js, 幻灯片]
---
近两年HTML5幻灯片越来越火，好的模板也层出不穷。最近个人比较喜欢[reveal.js][1]，简洁大方，功能齐全，3D效果，用它做过几次报告，效果很不错，十分推荐。

最近刚刚更新的版本新增了支持[Markdown][2]的功能,  但仍然存在一些问题和不便：

1. 需要直接编辑html文件，把markdown文件链接进去；
2. markdown的功能需要web server的支持，要在本地浏览还需要建个[本地的web服务器][3]，稍有不便。

于是操刀写了个小的`R`程序，利用了`markdown`包把markdown转化为html再套到reveal.js模板里，好处如下：

1. 只需要一行R代码就可以把markdown完美转化成html；
2. 不需要在server上运行；
3. 如果有网络的话，都不需要下载reveal的模板文件(包括css, javascript等)，会自动利用我网站上上传的模板文件。

于是乎，制作html5幻灯片变得如此简单：

1. 编写markdown文件，前三行以%开头，分别表示标题，作者和日期，幻灯片用`===`或`---`来分隔，`===`表示生成水平方向的，`---`表示生成竖直方向的，[这里][4]有样本文件；
2. 打开R，`setwd`到markdown文件目录下；
3. 读取并运行[reveal函数][5]。`reveal`函数有三个参数: `file`, `output`和`internet`(默认为`TRUE`)，分别表示输入文件，输出文件和是否用网络服务器上的reveal模板。

等不急了想现在就看效果的客观，可以运行下面的代码查看效果：

{% highlight r %}
source("http://dreamhunter.me/share/reveal.R")
reveal("http://dreamhunter.me/share/reveal.md", "reveal.html")
{% endhighlight %}

到R的工作目录下找到`reveal.html`看看效果吧:D

**补充说明**：目前`reveal`函数只实现了最简单的转换功能，还有许多功能有待添加，如模板的选择，自定义幻灯片的分隔符等，这些功能添加起来并不难，有兴趣的客观可以试试。reveal函数中需要的模板文件都可以在[此处][6]找到(`index_local.html`, `index_web.html`)。

[1]: http://lab.hakim.se/reveal-js/#/ "reveal.js"
[2]: http://daringfireball.net/projects/markdown/syntax "Markdown"
[3]: {% post_url 2013-03-10-python-local-web-server %} "python本地web服务器"
[4]: https://github.com/mingsnu/cn/blob/gh-pages/uploads/2013/03/xxx" "样本文件"
[5]: https://github.com/mingsnu/cn/blob/gh-pages/uploads/2013/03/reveal.R "reveal.R"
[6]: https://github.com/mingsnu/cn/blob/gh-pages/uploads/2013/03 "模板文件"
