---
title: Tex家族简述
layout: post
categories: 技术笔记
tags: [CTeX, LaTeX, LaTeX2e, MikTeX, TeX, Tex Live, TeX家族]
---
记得我是2010年8月份才开始接触Latex的，当时是通过看[益辉哥的博客](http://yihui.name/cn)知道这个东西的。强大灵活的排版功能，高质量的文件输出，以及非常好的拓展性使得它成为一款极品的排版工具。

在后来的学习过程中又陆续得遇到了很多新的名词，像Latex2e,pdfLatex,AMSLatex,Ctex等等。他们都属于Tex家族的成员，但成员一多就不免把他们弄混了，好像网上也没有个所谓的“Tex家族系普图”的东西，所以我就来理一理，看看这些成员之间到底啥关系。

* TeX：TeX家族的老祖宗，其他一切的TeX宏包等都是在TeX的基础上建立的，TeX提供了强大的算法和命令可以帮助你调节最微小的细节。但对于普通用户来说没有必要学习它，除非自己也想写个宏包玩玩。
* TeX系统：最流行的是TeX Live和MiKTeX. 它们是指一系列的与TeX有关的软件的下载与安装，如果有人说他要安装LaTeX,那么就是指要安装Tex系统。TeX Live在UNIX，Windows以及Mac下都有可安装的版本，一般Linux用户大多会选择安装TeX Live， 而Windows用户更喜欢用MiKTeX。最后说下CTeX，CTeX是基于Windows下的MiKTeX系统，对中文提供完整支持，所以在国内CTeX是应用最广泛的TeX系统。
* TeX引擎：PDFTeX，XeTeX，LuaTeX，e-TeX等。它们可以看作是TeX的变体，都有各自不同的特点，相当于给TeX插上了三头六臂，方便与其他软件的交互。后面将要说到的LaTeX宏包就是基于pdfTeX和XeTeX引擎的。
* TeX宏包（TeX版本）：有Plain TeX，LaTeX，ConTeXt，Texinfo，Eplain，AMSTeX等。所谓的TeX宏包就是建立在TeX的基础上，为了用户能更方便的应用TeX而添加了许多宏的升级版TeX。LaTeX是最流行的宏包之一，学习LaTeX要比学习TeX简单许多，用户可以在不懂TeX的情况下很快的掌握LaTeX. 另外LaTeX2e是LaTeX现在的一个版本而已，LaTeX2e就是LaTeX.

