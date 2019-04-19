---
layout:     post
title:      AndroidManifest标签说明
subtitle:   application标签
date:       2019-04-11
author:     JovenHe
header-img: img/post-bg-2019-01-10.jpg
catalog: true
tags:
    - Android
    - AndroidManifest
    


---

在项目开发中可能并没有什么问题，但真正运行到用户手机上却出现很多奇奇怪怪的问题，本文就是讲解遇到的一些因为AndroidManifest中的配置引发的问题

## 明文通信

把项目发给客户后发现项目运行在个别手机上接口返回数据报错，一开始我以为是网络问题，但多次尝试后发现所有接口都报错，拿来同事的手机debug一下。

#### 报错信息

CLEARTEXT communication to xx.xx.xx.xx not permitted by network security policy

因为网络安全政策不允许明文通信到这个服务器。

看到这个报错信息，我就知道是新系统的特性问题，因为拿到同事的手机的时候看了一下系统版本是Android 9.0，而且日常浏览微信公众号时看到过新系统有个什么安全特性，有个印象，直接查找Android 9网络安全，就找到原因和解决方案了，是因为Android Pie上的所有应用程序默认都使用HTTPS，我们在项目上使用的是HTTP，所以就报错了。

#### 方案1

在build.gradle中把targetSdkVersion 降级回到 27或以下

意在App没有兼容到系统P这一高版本

#### 方案2

在 res 下的xml 目录中创建一个名为network_security_config.xml 文件 ，写入内容

```xml
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <base-config cleartextTrafficPermitted="true" />
</network-security-config>
```

然后在清单文件AndroidManifest中application 标签内加入

android:networkSecurityConfig="@xml/network_security_config" 

意在告诉系统，允许明文通信

#### 方案3

和服务器通信都改为HTTPS。

#### 总结

三种方案都能解决问题，最好的方案是方案3，从根本上解决问题，但在实施上不一定能得到支持，其余两种方案都能解决问题，但不确定系统会不会提示用户应用不安全、应用未兼容本系统等问题。

就像当年Android6推出运行时权限一样，不少开发者都觉得麻烦，直接把targetSdkVersion设置为22来逃避这一问题，但这就是趋势，是未来，未来一定是越来越注重信息安全的。

## 备份

看到微信公众号上推送了一篇文章。[不关 Android 云备份，坑了开发和测试！](https://mp.weixin.qq.com/s/4EukdqbeKAHIdp6FyVLqLA)

简单说就是app登录了A账号，卸载完，再次安装后，登录了B账号，后来发现账号又变成了A，因为是系统开启了云备份，在某个时间备份了app内的SharedPreferences账号信息，重装后，恢复了云端信息。

#### 问题原因

因为国内Android厂商纷杂，碎片化严重的原因，某些厂商会在自己的 ROM 中实现备份功能，有的没有，而且备份还是不定时的，这就引发了备份的数据不可控的问题。

同时在建项目的时候，清单文件AndroidManifest中application 标签内 allowBackup默认是true的，不注意的话根本不会想到有这个坑。

#### 安全风险

备份本身是一个好功能，但是不可控的话，上线App还是关闭备份功能吧。

同时，在手机未Root的情况下，通过adb命令可以得到指定app的备份数据，通过几个命令就可以逆向得到数据，这本身是很危险的。如果某些app不注重安全，把某些数据存在SharedPreferences中，很容易就能拿到数据。

#### 解决方法

在清单文件AndroidManifest中application 标签内改为

```xml
android:allowBackup="false"
```

运行如果报错的话，再加入一句

```xml
tools:replace="android:allowBackup"
```

当然问题的产生还是由于没有总结日常开发中需要了解的Android新版本新特性，所以还是要多关注Android的一些新动态的，尤其是和开发相关的。