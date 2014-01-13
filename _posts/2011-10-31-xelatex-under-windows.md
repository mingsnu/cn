---
title: windows下XeLaTex处理中文问题
layout: post
categories:
  - 技术笔记
tags:
  - LaTeX
  - Windows
  - xelatex
  - 中文
---
虽然接触$LaTeX$快有一年时间了，但是还从未用其编译过中文，曾经也试图在`Linux`配置过，但是由于过程十分繁琐，不了了之。最近由于女朋友想要用$LaTeX$写毕业论文，于是我硬着头皮再次尝试解决用$LaTeX$处理中文的问题。

大家都说`xelatex`从底层支持中文，所以果断选择`xelatex`。很多东西就是明白的人看来非常简单，但是不明白的人几乎无从下手。

首先我下载了[Basic MiKTeX 2.9][1]，`MiKTeX`默认选用[TeXworks][2]作为编辑器，我对`TeXworks`印象还不错，主要原因是界面简洁大方，当然也支持语法高亮。

安装完以后运行`TeXworks`, 然后将下面的测试代码复制过去，在菜单栏的运行按钮右边选择`XeLaTeX`, 然后运行。如果能顺利运行，那么恭喜你，你运气真好，一定要去抓彩票哈！

{% highlight latex %}
\documentclass[a4paper,10pt]{article}
\usepackage{xltxtra}
\usepackage{fullpage}
\usepackage{fontspec}
\setromanfont{STSong}
\setsansfont{STKaiti}
\XeTeXlinebreaklocale "zh"
\XeTeXlinebreakskip = 0pt plus 1pt
\usepackage{setspace}
\onehalfspacing
\title{第一篇中文\LaTeX{}文档}
\author{我高兴}
\date{}
\begin{document}
\maketitle
我的\XeLaTeX{}的处女作！！留作纪念吧~
\ldots
\end{document}
{% endhighlight %}

当然你有很大的可能性在运行的过程中会报错，就像我。下面给出一些我遇到过的问题的解决方案。

如果是提示少某些包的话，那么会弹出对话框让你安装缺失的包，这个还是比较方便的。

我在安装的过程中还遇到过这样的错误：一个是说少`expl3.sty`，需要加载一个叫`expl3`的包。另一个报错：`\char_make_active:n {"20}%`。

解决办法是要更新字体库，更新方法是找到如下目录`C:\Program Files\MiKTeX 2.9\miktex\bin\internal`（每个人的`MiKTeX`位置不同目录也不一样哦），运行一个叫`miktex-update_admin.exe`的文件，当然保险起见最好以管理员身份运行。更新完后再次运行上面的代码，安装依赖的包就可以得到一份显示汉字的pdf文件啦，Cheers! 

BTW: 如果没有STSong和STKaiti字体的的话，可以去网上搜索下载安装，如这个网址 <http://ishare.iask.sina.com.cn/f/11651017.html?from=isnom>

Good luck!

[1]: http://miktex.org/2.9/setup
[2]: http://www.tug.org/texworks/
