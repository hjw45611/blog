---
layout:     post
title:      Kali中密码爆破工具Hydra的使用
subtitle:   渗透测试工具学习
date:       2019-08-03
author:     JovenHe
header-img: img/post-bg-kali.jpg
catalog: true
tags:
    - 工具
    

---

最近在学渗透测试，在课程中老师通过Hybra成功爆破另一台主机的密码，他是在网上下载的Hybra，我在Kali中看到过有这个工具，所以姑且拿来一用

### 环境

Hybra使用的前提是两个主机需要在同一网段下，我是用WMware虚拟机搭建的，两台模拟器的网络适配器都调成桥接模式。确保两者能ping通。

<img src="https://i.loli.net/2019/08/03/xDp9rNjnaftvJzB.png" alt="虚拟机网络适配器.png" title="虚拟机网络适配器.png" width="50%" />

### 启动应用

直接在kaili中搜索应用Hybra，点击打开进入终端

<img src="https://i.loli.net/2019/08/03/Rtep1hMYfAaqrik.png" alt="搜索应用.png" title="搜索应用.png" />

<img src="https://i.loli.net/2019/08/03/1fneyCpAS4YGEbP.png" alt="Hybra说明1.png" title="Hybra说明1.png" />

<img src="https://i.loli.net/2019/08/03/2FLNqMOBzGyblI1.png" alt="Hybra说明2.png" title="Hybra说明2.png" />

终端中说明了使用方法、参数介绍以及使用例子，

### 使用

我使用的密码本是kali自带的unix常用的1000个的密码字典，使用如下

hydra -l administrator -P /usr/share/wordlists/metasploit/unix_passwords.txt 192.168.31.240 smb

-l指定登录名

-P指定密码本文件

192.168.31.240 smb 指定了爆破的是指定IP的指定协议

<img src="https://i.loli.net/2019/08/03/oQPt18L7EfvhxmF.png" alt="得出密码.png" title="得出密码.png" />

可以得出用户名是 administrator，密码是12345