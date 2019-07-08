---
layout:     post
title:      AndroidKiller工具使用详解
subtitle:   逆向工具学习
date:       2019-06-13
author:     JovenHe
header-img: img/post-bg-hook.jpg
catalog: true
tags:
    - 反编译
    


---

Android Killer好久前就安装过了，当时尝鲜后看了看就没用了，平时都是直接看反编译得到的java代码，用Jadx比较多，近期觉得自己smali方面还是比较差，所以拿出来学习一下，并对AK有一个完整的了解。

因为是在吾爱破解上下载的软件，在使用中遇到的配置、卡死等问题直接参考的[相关帖子](https://www.52pojie.cn/thread-726176-1-1.html)即可解决。

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

### 工具

##### 编码转换

点击工具栏中的编码转换按钮后，弹出编码转换窗口，可以使用编码的转换，我之前不知道有这个工具，都是找网上的在线转码的工具网站，没想到软件本来就自带了。

<img src="https://i.loli.net/2019/07/05/5d1f187fc3ba345691.png" alt="工具-编码转换.png" title="工具-编码转换.png" />

##### MD5查看器

点击工具栏中的MD5查看器按钮后，弹出MD5查看器窗口，可以计算出字符串的密文。

<img src="https://i.loli.net/2019/07/05/5d1f24cc7e4f434889.png" alt="工具-MD5查看器.png" title="工具-MD5查看器.png" />

##### 文件搜索器

点击工具栏中的文件搜索器按钮后，弹出文件搜索器窗口，可以搜索指定文件夹下包含搜索字符的文件，这个功能类似Mac中Finder的搜索，可以看到连某些js文件也可以查找到。

<img src="https://i.loli.net/2019/07/05/5d1f262cc71ad85270.png" alt="工具-文件搜索器.png" title="工具-文件搜索器.png" />

##### 自定义

调用的windows的自带的文本编辑和计算器，方便记录和计算

<img src="https://i.loli.net/2019/07/05/5d1f291c2526639411.png" alt="工具-自定义.png" title="工具-自定义.png" />

##### 签名

点击工具栏中的按钮后，弹出MD5查看器窗口，在apk路径中选择要签名的apk文件，并且在手机连接电脑后，窗口底部的签名成功后自动安装后面的下拉框会显示已连接手机信息。勾选复选框后执行即可。

<img src="https://i.loli.net/2019/07/05/5d1f2aed694af36240.png" alt="apk签名.png" title="apk签名.png" />

##### 查壳

查壳是为了查看apk有没有使用加固壳，点击工具栏中的APK查壳按钮后，弹出APK信息查看窗口，在apk路径选择apk文件后即可检测信息，但不会很准确。

<img src="https://i.loli.net/2019/07/05/5d1f2e4f8046711439.png" alt="apk查壳.png" title="apk查壳.png" />

可以看到这个apk并没有查出有用信息，但工程管理器中smali代码中只有qihoo的文件夹，这明显是360的壳，所以还是要通过工程信息凭常见壳的特征来确定是否有壳。

##### 伪加解密

说实话这个我还真不知道是干嘛的，但弹窗底部提示适用于Android版本4.2之前，现在的应用最起码都是4.4之后的了，所以不用管这个工具了。

<img src="https://i.loli.net/2019/07/05/5d1f304e2017f82125.png" alt="伪加解密.png" title="伪加解密.png" />

### Android工具

<img src="https://i.loli.net/2019/07/08/5d229f9b597de84511.png" alt="Android工具.png" title="Android工具.png" />

##### 编译

对当前项目打包修改后的apk

##### 批量编译

对所有打开项目打包修改后的apk

##### 字符串

查找当前项目中字符串引用，而且支持转码显示

<img src="https://i.loli.net/2019/07/08/5d22a780cb75e32915.png" alt="搜索字符串.png" title="搜索字符串.png" />

##### 方法声明

查找当前项目中方法声明

<img src="https://i.loli.net/2019/07/08/5d22aacd76b3786676.png" alt="方法声明.png" title="方法声明.png" />

##### 插入代码管理器

是常用代码的一个管理，提供了三个默认模版，也可新建或删除

例如我们想要在被修改app的某个位置弹出重要信息，可以复制Toast中的代码，粘贴在Smali代码的相应方法内，简单修改即可使用。

<img src="https://i.loli.net/2019/07/08/5d22b297ab81e91490.png" alt="插入代码管理器.png" title="插入代码管理器.png" />

##### ApkTool管理器

用于管理使用的Apktoll.jar的版本使用

##### 设备相关工具

需要连接Android设备后，可以对当前项目的安装、运行、卸载，可以查看设备的进程、打印日志、设备内文件

<img src="https://i.loli.net/2019/07/08/5d22bca85d2ac55208.png" alt="设备工具.png" title="设备工具.png" />

### Smali工具

指的是在Smali代码页面的可用工具，smali代码页面如下：

<img src="https://i.loli.net/2019/07/08/5d22eb353b55253199.png" alt="smali代码页.png" title="smali代码页.png" />

##### 1.命令释义

鼠标悬停在命令上后，会浮出命令释义，对于Smali命令初学者很友好

<img src="https://i.loli.net/2019/07/05/5d1f14d466ef676169.png" alt="smali命令释义.png" title="smali命令释义.png" />

##### 2.当前文件框

展示当前Smali文件，可切换相同java类生成的其他smali文件

<img src="https://i.loli.net/2019/07/08/5d22ec8e1f31494707.png" alt="切换Smali文件框.png" title="切换Smali文件框.png" />

##### 3.当前方法

展示光标所在位置的方法，点击可展示当前smali文件的所有方法，并可点击切换其他方法

##### 4.锁定当前文件为只读模式

点击后文件只读不能编辑，再次点击可解锁

##### 5.保存修改

##### 6.复制、剪切、粘贴

编辑smali文件时，代码的复制、剪切、粘贴

##### 7.撤销与重做

编辑smali文件时，代码的撤销与重做

##### 8.跳转到光标位置上次与下次

编辑smali文件时，跳转到上次光标位置或下次光标位置

##### 9.自动换行

点击后过长的代码会自动换行展示，再次点击可恢复

##### 10.查看java源码

展示反编译得到的java源码，默认展示当前Smali文件的反编译java类。

<img src="https://i.loli.net/2019/07/08/5d22f4d7ba82e24745.png" alt="查看java源码.png" title="查看java源码.png" />

##### 11.查看当前Smali文件中使用的所有字符串和调用的所有方法

点击后可查看当前Smali文件中使用的所有字符串和调用的所有方法，并且可以过滤，可以更快的定位出要找的代码段。

<img src="https://i.loli.net/2019/07/08/5d22f8ab7864d69258.png" alt="所有字符串.png" title="所有字符串.png" />

<img src="https://i.loli.net/2019/07/08/5d22f8ab673a554698.png" alt="所有方法.png" title="所有方法.png" />



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

可以看到smali中有很多带有“修改”Unicode码的文本。然后使用编码转换得到“更改”的Unicode编码，是\66f4\6539，直接全部替换

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