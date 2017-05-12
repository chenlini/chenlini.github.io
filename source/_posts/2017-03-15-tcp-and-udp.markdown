---
layout: post
title: "TCP and UDP"
date: 2017-03-15 22:40:05 +0800
comments: true
categories: OS 
---

###TCP(Transmission Control protocal)
TCP is based on **connection** which means sending end must creat a stable connection to receiving end. This operation called **three-way handshake**.

###UDP(User Data protocal)
Data transmission based on UDP don't need to build connection before. The sending post send out data as soon as possible. It doesn't make sure the receiver can receive data completely and correctly.

<!--more-->

 TCP | UDP
------|----
reliable and stable| not reliable
mass of data  | small data 
   slow |fast
     O2 byte stream   | O2 message
     one to one| one to many
     more system resource|less system resourse
     HTTP,FTP|QQ Voice QQ video




　　
###UDP应用场景：
  1. 面向数据报方式
  2. 网络数据大多为短消息 
  3. 拥有大量Client
  4. 对数据安全性无特殊要求
  5. 网络负担非常重，但对响应速度要求高
 
###其他区别
1. socket()的参数不同 
2. UDP Server不需要调用listen和accept 
3. UDP收发数据用sendto/recvfrom函数 
4. TCP：地址信息在connect/accept时确定 
5. UDP：在sendto/recvfrom函数中每次均 需指定地址信息 
6. UDP：shutdown函数无效
