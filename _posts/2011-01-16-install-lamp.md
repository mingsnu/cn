---
title: 零基础搭建LAMP服务器（Ubuntu版）
layout: post
categories: 技术笔记
tags: [LAMP, Ubuntu, phpMyAdmin]
---

*注: 本文简述了搭建本地LAMP服务器的流程，旨对零基础的初学者提供简单的参考，非零基础初学者请绕行，以免打扰您宝贵的时间：)*

`LAMP`为`Linux+Apache+MySQL+Php`的缩写，顾名思义要搭建`LAMP`平台就要在`Linux`下安装配置`AMP`三种软件。而在`Ubuntu`下安装软件又是那么的容易，只用简单的命令行或者直接到新得力里点击下载就可以了。剩下的问题就是如何配置，参照下面的步骤，就可以轻松搞定了：)

先进行下简单的名词解释，免得有像我一样菜的童鞋连`Apache`是干啥的都不知道：D

`Apache`：这里所说的`Apache`是`Apache HTTP Server`的简称。是一款开源的伺服器软件，功能灰常强大，维基百科的服务器就是用的`Apache`。如果在自己的电脑上安装了它你就可以拥有本地的web服务器了，可以很方便得在自己的电脑上调试网站了。

`MySQL`：如今最流行的开源数据库。维基，Facebook,Google都是用的这货！

`Php`：一种开源免费的脚本语言，用于制作动态网页。

现在正试进入实战演练，跟着步骤走，你会发现一个又一个的惊喜：）

* 第一步，安装`Apache`。直接终端（`Alt+Ctrl+T`）输入：`sudo apt-get install apache2`安装即可。
* 第二步，测试`Apache`，打开任何一款浏览器在地址栏输入 http://localhost/ ，看见“It works!”出现了么？惊喜吧？继续！
* 第三步，安装`Php`。直接在终端输入：`sudo apt-get install php5 libapache2-mod-php5`和`sudo /etc/init.d/apache2 restart`
* 第四步，测试`Php`，用任意一款编辑器在`/var/www/`下建立`testphp.php`文件，例如：`sudo gedit /var/www/testphp.php`然后把 `<?php phpinfo(); ?>` 粘贴到`testphp.php`文件中去并保存。好了，下面你就要看到第二个惊喜了，打开浏览器，在地址栏里输入下面的地址： http://localhost/testphp.php 。怎么样，看见了么，有个很长的全是表格的页面出现了，非常好，我们离胜利更近了一步。
* 第五步，安装`MySQL`。在终端输入：`sudo apt-get install mysql-server`。如果你想让你的网络上的其他电脑也能看到你建的服务器的话要进行下一步，如果你是自己用的话下面的一步可以省略：终端输入`gksudo gedit /etc/mysql/my.cnf`找到`bind-address = 127.0.0.1`这一行把后面的`ip`改成自己电脑的`ip`即可（自己的`ip`可以用 `ifconfig`命令得到）。
* 其实到此为止可以结束了，但是通常为了方便管理我们的数据库我们还会安装`phpMyAdmin`，终端：`sudo apt-get install libapache2-mod-auth-mysql php5-mysql phpmyadmin`。为了让`PHP`与`MySQL`能够协调配合，我们要对`php.ini`进行一点修改：终端输入`gksudo gedit /etc/php5/apache2/php.ini` 找到`;extension=mysql.so`删除前面的`；`号编变成这个样子 `extension=mysql.so`。 重启`Apache`：`sudo /etc/init.d/apache2 restart`。最后打开浏览器输入： http://localhost/phpmyadmin/ 如果出现了`phpMyAdmin`的登录界面的话就大功告成了！！
