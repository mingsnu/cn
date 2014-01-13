---
title: 本地WordPress如何添加控件？
layout: post
categories: 技术笔记
tags: [code, latex maths, local wordpress, plugin, R]
---
WordPress里的插件是真多，随便揪出个功能来你就能找到一片插件，看出开源软件的好处来了：） 不过随之带来的问题是你要在这些良莠不齐的插件中找到最满足你胃口的，这是个麻烦事，就跟一群人要跟你相亲一样，虽然看着这个长得不错，但还是想看看下面一位是不是长得更漂亮？！

利用昨天基于[LAMP]({% post_url 2011-01-16-install-lamp %})搭建的[本地WordPress]({% post_url 2011-01-16-install-wordpress-locally-for-beginner %}), 可以很方便得测试各种插件的性能 。

最后说一下成果，主要找了两个插件：

一是在WordPress里编辑数学公式的[WP QuickLaTeX](http://wordpress.org/plugins/wp-quicklatex/)插件。另一个是支持代码高亮的[WP CodeBox](http://wordpress.org/plugins/wp-codebox/)插件。

先说WP QuickLaTeX插件，选择这个插件的理由是它功能特别强大，产出的数学公式的质量特别高，缺点就是有点慢，如果速度能再快点就完美了。如果您发现比这货还好的插件的话请您跟我说一声，有福同享嘛，哈哈：D

再说一下WP CodeBox插件。选择它的主要理由是图个省劲，因为除了这个插件外其他的插件似乎都不支持R语言（作者注：当时写这篇博文时还很少有支持R高亮的插件，现在大多支持了，CodeBox也已经是个非常落后的插件了）。 这个插件的功能还是比较强大，可以折叠代码，直接复制和下载代码，并且支持灰常多的语言。唯一我不满意的地方是虽然对R语言有语法高亮效果，但是不怎么好看。我个人觉得[这位大神](http://yihui.name/en/2010/09/syntaxhighlighter-brush-for-the-r-language/)的代码高亮最好看，可惜需要手动配置，由于嫌麻烦就忍痛割爱了……
