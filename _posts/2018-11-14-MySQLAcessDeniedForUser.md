---
layout:     post
title:      Deal with Acess denied for user 'root'@'%' by MySQL
subtitle:   MySQL Debug
date:       2018-11-14
author:     JIAWEI HUANG
header-img: img/post-bg-net.jpg
catalog: true
tags:
    - 笔记
    - 个人
    - MySQL
    -Debug
---

Today, I want to use mysql to connect my python program, but when I logined in mysql, it was wrong.  It print that 
**'access denied for user 'root'@'localhost' (using password yes)'**. 

The reason for this problem is that 
**the reload permission(权限) is reclaimed ,making it impossible to reassign(重新分配) permissions. Other similar permission issues can alse refer to this method**.

The solution is as follow:
####1.Stop Mysql service
* go to the mysql directory and use console to run :
**$ service mysql stop**
####2.Skip password verification
* go to find mysql's configuration file,which name is my.cnf I searched.But In my linux, this file is named **mysqld.cnf in the /etc/mysql/mysql.conf.d.** It may be different between versions.
* Open it and add **'skip-grant-tables'** after [mysqld] to save and exit.
####3.restart mysql service
* **$ service mysql restart**
####4.Login in
* $ mysql -uroot -p
no password is required here to enter.
####5. Change your root password
$ use mysql;
$ update user set password=password('root') where user ='root';

if your mysql doesn't have password colum, run other console:

$ update user set authentication_string=password('root') where user ='root';

$ flush privileges;
$ exit;

####6.Delete 'skip=grant-tables' in mysqld.cnf
* restart mysql

