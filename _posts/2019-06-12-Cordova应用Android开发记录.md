---
layout:     post
title:      Cordova应用Android开发记录
subtitle:   使用记录
date:       2019-06-12
author:     JovenHe
header-img: img/post-bg-hook.jpg
catalog: true
tags:
    - 大前端
    


---

Cordova应用我初步的理解就是类似JsBridge这个框架，通过Js调用原生方法，并回调结果。

## 1.安装Node

电脑未安装Node的话，下载安装载和安装[`Node.js`](https://nodejs.org/en/download/)

## 2.安装`cordova` 模块

```bash
$ sudo npm install -g cordova
```

## 3.创建cordova项目

在指定目录下

```bash
$ cordova create [项目目录] [项目包名] [项目名]
```

## 4.添加平台

进入项目目录

```bash
$ cd [项目目录]
```

添加目标平台

```bash
$ cordova platform add android --save
```

## 5.创建插件

电脑安装plugman 功能模块

```bash
$ npm install -g plugman
```

创建插件

```bash
$ plugman create --name helloPlugin --plugin_id com.ido.plugin --plugin_version 0.0.1
```

为插件增加平台

```bash
$ cd helloPlugin
```

```bash
$ plugman platform add  --platform_name android
```

## 6.安装插件

项目增加插件

```bash
$ cordova plugin add [插件路径]
```