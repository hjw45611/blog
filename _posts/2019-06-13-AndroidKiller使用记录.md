---
layout:     post
title:      AndroidKiller使用记录
subtitle:   逆向工具学习
date:       2019-06-13
author:     JovenHe
header-img: img/post-bg-hook.jpg
catalog: true
tags:
    - 反编译
    


---

Android Killer好久前就安装过了，当时尝鲜后看了看就没用了，平时都是直接看反编译得到的java代码，用Jadx比较多，近期觉得自己smali方面还是比较差，所以拿出来学习一下，并对AK有一个完整的了解。

因为是在吾爱破解上下载的压缩包，所以解压缩后点击exe文件直接用的，记得一开始打开apk时反编译失败，网上查找后更新了apktool就可以了。

### 主要窗口

##### 主页

<img src="https://i.loli.net/2019/06/18/5d087c8d44f5b37819.png" alt="开始页面.png" title="开始页面.png" />

直接点击打开，选择一个apk文件即可

经过分析后可查看工程信息

##### 工程信息窗口

能看到app的名称、包名、入口Activity、版本号、以及四大组件信息和权限相关。

<img src="https://i.loli.net/2019/06/18/5d087ecce5f2172992.png" alt="apk工程信息.png" title="apk工程信息.png" />

##### 工程管理器窗口

包含assets、res、smali、manifest等信息

<img src="https://i.loli.net/2019/06/18/5d087ecd1c8f299109.png" alt="apk工程管理器.png" title="apk工程管理器.png" />

##### 工程搜索窗口

包含搜索字符、替换字符、搜索范围、文件类型、字符解码等选项。

<img src="https://i.loli.net/2019/06/18/5d087ecdd194931941.png" alt="apk工程搜索.png" title="apk工程搜索.png" />

在使用上还是实践为主，下面就举两个栗子吧：

### 栗子1

汉化app，因为某些国外app没有中文，所以有人专门做汉化app，Android Killer就是汉化的利器

因为我这个项目没多少英文展示，所以就把“修改”替换为“更改”

直接搜索“修改”

<img src="https://i.loli.net/2019/06/18/5d089006663d642131.png" alt="搜索文本.png" title="搜索文本.png" />

可以看到只有布局文件中有该文本，直接输入替换文本字符，并全部替换。

<img src="https://i.loli.net/2019/06/18/5d0892294ceb822742.png" alt="更改文本.png" title="更改文本.png" />

可以看到布局文件中的文本已被替换。

但实际中在java代码中写的“修改”文本在Smali中是Unicode字符，所以需要转化为Unicode后进行搜索

<img src="https://i.loli.net/2019/06/18/5d0890050951313904.png" alt="搜索文本转化.png" title="搜索文本转化.png" />
<img src="https://i.loli.net/2019/06/18/5d0890056467e51543.png" alt="搜索Unicode文本.png" title="搜索Unicode文本.png" />

可以看到smali中有很多带有“修改”Unicode码的文本。“更改”的Unicode编码是\66f4\6539，直接全部替换

<img src="https://i.loli.net/2019/06/18/5d0894d5554c086273.png" alt="更改Unicode文本.png" title="更改Unicode文本.png" />

可以看到修改手机 变成了更改手机。

至此，”修改“ 的替换全部完成。

然后点击Android菜单下的编译按钮，就可以打包出更改后的apk了。

<img src="https://i.loli.net/2019/06/18/5d0895a8273da71978.png" alt="编译按钮.png" title="编译按钮.png" />



### 栗子2

前两天升级了Android studio，升级过程中需要下载的jar包过多时间很长，正好别的同事让我把项目中的URL地址换成本地IP打个包，方便测试，所以只好拿Android Killer来打个包了

一开始我直接搜索了"http://"，直接搜索出了几百个文件

<img src="https://i.loli.net/2019/06/18/5d08985f626db12473.png" alt="直接搜索http.png" title="直接搜索http.png" />

一看大部分都是res中的文件，想起来XML文件中大部分都有xmlns:android="http://schemas.android.com/apk/res/android"这么一段，所以直接搜索是不行的，需要选择搜索的文件类型为smali。

<img src="https://i.loli.net/2019/06/18/5d08a0fd78e0285382.png" alt="smali搜索http.png" title="smali搜索http.png" />

可以通过搜索结果包名快速定位找到网络请求地址所在位置，然后就可以按照上个例子中的替换字符来替换成本地IP，然后编译就可以了。

### 注意

编译后的apk安装前需要卸载之前安装的app，因为编译得到的apk和之前的签名还是不一样的。