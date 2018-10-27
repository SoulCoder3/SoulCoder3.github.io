---
layout:     post
title:       Internet Client Programming
subtitle:   旧的回忆,慢慢积累
date:       2018-10-26
author:     JIAWEI HUANG
header-img: img/post-bg-net.jpg
catalog: true
tags:
    - 笔记
    - 个人
    -Python
---

# Internet Client Programming

##Internet Client
  What is internet client? We can know that internet is where data is transmitted between client and server. The server is producer and the client is consmer. For a particular service , there is usually only one server(process or host), but there are multiple consumers.
##File Transfer Protocol(FTP)
On the Internet, transferring files is very common .FTP is a protocol used to tansfer file. You can transfer and download files by the FTP.  FTP workflow is as follows:
#####1.The client connects to the FTP server on the remote host.
#####2.The client enter username and password.
#####3.The client transfers files and inquiries information.
#####4.The client exits from the remote FTP server and ends the transfer.

##Network News Transport Protocol(NNTP)
Users use NNTP to download or post in newsgroups.NNTP and FTP operate in a similar way, but NNTP is simpler than FTP. In the FTP, you should sign in, transfer data and control using different ports. However, in the NNTP, it just use only one standard ort 119. The user sends a request to the server and the server responds accordingly.

#Simple Mail Transfer Protocol (SMTP)
SMTP is a relatively simple text-based protocol. One or more recipients of a message are specified on it and the message text is transmitted. It is very easy to easy to test an SMTP  servr through the telnet program. 

#Post Office Protocal(POP)
The purpose of POP is to allow the user's workstation to access the mailbox in the mail server and send the mail to the mail server by the SMxinxiTP.

