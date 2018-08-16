---
layout:     post
title:      使用github pages开源项目搭建博客遇到的一些问题
subtitle:   慢慢来,总会成功的
date:       2018-08-16
author:     YELLOW
header-img: img/post-bg-road.jpg
catalog: true
tags:
    - debug
    - 个人
---

## 前言
gitHub上作者的ReadMe文档说的很明白也很清晰,但是即使如此还是会出现一些问题,毕竟一帆风顺总是困难的,在这里将问题总结起来,顺带附上[原作者git链接](https://github.com/qiubaiying/qiubaiying.github.io)和[作者的简书链接](https://www.jianshu.com/p/e68fba58f75c)。


## 更改GitHUb的Username
如果你对自己的GitHub的Username不是很满意的话,请务必更改,虽然后面购买域名后也不会见到username,但是在配置文件和需要github的一些功能上需要填自己的username,你会在后面和它打很多次交道.像博主这样本来的GitHub是全数字的就显得很别扭也不美观.
![](https://raw.githubusercontent.com/yellowprogramer/yellowprogramer.github.io/master/img/debugWithBlog01.png) 
只要点击下方的**change username**就可以了就会提示让你该名字,注意如果出现你更改的名字已经有人在用了,那么更改就会失败.


## 更改仓库名为后出现404
在将fork下来的仓库名改为<font color=#A52A2A>你的git账号名.github.io </font>,浏览器输入<font color=#A52A2A>你的git账号名.github.io</font>后网页出现404 not found.一般来说,更改了仓库名后是需要几分钟的时间才会显示页面,如果几分钟后也是404,那么请注意你的链接是否和你的账号名相同,如果相同,请清理缓存,在等几分钟就可以了.

## 评论系统显示出问题
现在我博客用的是gittalk是与github账号连同的,具体评论原理其实就是在仓库里开一个issuse.问题有三种:
### 1.ERROR:
出现这个证明配置出现错误,有可能在配置文件种的clientId或者秘钥不正确,也有可能是你的输入输出链接有问题,重新审核一边或者换个秘钥重新配置.
### 2.Not Found Issues
你fork的库没有开启issues,在setting中把issues的框勾上就可以了.
### 3.Validation Failed
这个问题有些微妙,因为这是GitHub的字长限制问题,博客使用的后台传给GitTalk的id是文件名转化过来的,不能超过50个字长,但是如果你的博客文件名存在中文名,中文转码解析的时候就很容易超过这个值,有些写程序经验且熟悉项目的可以去更改代码解决这个问题,只是想使用博客的人只要把文件名写得尽量不要出现中文就好了,而且文件名的格式必须是"2018-08-16-XXXX.md"类似这样的格式,XXXX是标题.
经过了这三个问题的折磨后一般都能够成功显示评论功能

## 写文章上传到GItHub后显示异常
我在本地用remarkable写的文件然后push上GItHub结果显示得和结果不一样,需要我直接在项目上更改,我remarkable显示是正常的但是到GitHub上后就异常了,很迷,暂时还发现不了原因.

## 有关自定义域名的问题
这个问题比较简单,我买的阿里云的域名,按照教程来却没能用自己的域名打开页面,遇到这种问题一般是粗心大意,域名解析设置的时候没有和自己的<font color=#A52A2A>你的git账号名.github.io</font>一样.如果你设置的是IP地址,也就是A类性,请你在自己电脑控制命令下运行 ping <font color=#A52A2A>你的git账号名.github.io</font>查看IP地址再填.配置完后一般要等10分钟左右生效,再不行,就清理下缓存试试.

## Linux系统没有GitHub Desktop
我的操作系统是Liunx系统,而GitHUb Desktop图形界面官方发行的只有windows和Mac,我也暂时找不到好用的图形界面,不过用得了Linux的一般都是用终端的吧,我是先在本地写好文档,放置好图片后,然后调用<font color=#A52A2A>git add, git commit -m"</font>此处是上传信息",最后在<font color=#A52A2A >git push</font>,总的来说不算太方便,但是出错能够很容易知道出处.如果你的项目是放在有权限的目录下的话建议先把权限去掉,不然在需要root权限的文件中,即使你用权限打开了也是无法使用输入法的,所以先用<font color=#A52A2A>git chomd 777 xxx(xxx为文件名或文件夹名)</font>,这样运行后就不用sudo来用权限打开了.

**最后祝大家都能顺利搭起自己的博客**
