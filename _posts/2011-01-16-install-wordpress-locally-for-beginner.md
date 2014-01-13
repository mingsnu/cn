---
title: 零基础搭建本地WordPress(Ubuntu版)
author: dreamhunter
layout: post
categories: 技术笔记
tags: [LAMP, Ubuntu, WordPress, 本地]
---
*注：本文主要介绍了如何在Ubuntu下基于LAMP搭建wordpress的本地测试。Windows用户请参考: [http://fairyfish.net/2007/06/25/installing-wordpress-locally](http://fairyfish.net/2007/06/25/installing-wordpress-locally)。*

今天是本小站建立的第三天了，从起初的一无所知到今天成功搭建本地的wordpress，感觉自己向前迈进了一大步，对整个网站的工作原理有了更深一层的了解。虽然时间已经是凌晨两点半了，我决定还是要坚持写完这篇博文，为我的“迪木亨特”补充新鲜的血液。由于个人水平的限制，文中不免有疏漏和谬误，敬请各位客官恨劲拍砖——您的“一顿拍”是我前进的动力：）

为什么要搭建本地的wordpress呢？就是为了方便测试，不用一遍遍的往服务器上传，节省宝贵的时间。这对于想制作或修改自己的wordpress模板的童鞋十分有用。我就是因为想修改一下自己的模板的一个小小的地方才掉进这个大“坑”里的。

好了，正式开始我们的旅程：

* 第一步：搭建LAMP（Linux+Apache+MySQL+Php）,如果您还没有搭建好请先看[这里]({% post_url 2011-01-16-install-lamp %})：）
* 第二步：下载解压wordpress。直接复制如下命令到终端:
{% highlight bash%}
wget http://wordpress.org/latest.tar.gz
sudo tar -xzvf latest.tar.gz -directory=/var/www/
{% endhighlight %}
或者，您可以从[这里](http://wordpress.org/download/)下载wordpress并解压到`/var/www/`文件夹下。

* 第三步：创建数据库和用户名。这里我们用第一步里安装好的phpMyAdmin来创建wordpress的数据库和用户名。先登录phpMyAdmin(http://localhost/phpmyadmin/)，操作步骤如下：
    1. 在`Create new database`的文本输入框里输入要创建的WordPress数据库名称（以`wordpress`为例），点击`Create`按钮。
    2. 点击左上角的`Home`图标然后点击`Privileges`, 点击`Add a new User`，在`User name`后输入与WordPress相关连的用户名（以`wordpress`为例）。（下拉菜单中选择`Use text file`）。
    3. 输入密码，可以用下面的密码生成器，自己用的话没必要设那么麻烦的密码。（下拉菜单中选择`Use text file`）
    4. 在`Global privileges`选项中选择`Check All`，点击`Go`。

* 第四步：很多教程这一步都是设置`wp-config.php`文件，但是我觉的新手很可能不知到改怎样修改。所以我建议直接运行“Install Script”。直接打开浏览器，在地址栏里输入：http://localhost/wordpress/wp-admin/install.php，按照提示依此输入 Database name, User name等信息，然后提交，wordpress会提示你把一段代码复制粘贴到`wp-config.php`文件中。按照要求用编辑器编辑此文件后保存。再次在地址栏中输入：http://localhost/wordpress/wp-admin/install.php， 然后依次输入Site Title, Username 等信息，点击 Install WordPress，于是WordPress 就安装成功了！

是不是很兴奋？！哈哈，开始你的自由之旅吧：）
