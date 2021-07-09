---
layout:     post
title:      Oppo设置deviceOwner为什么失败
subtitle:   系统分析
date:       2021-04-23
author:     JovenHe
header-img: img/post-bg-hook.jpg
catalog: true
tags:D
    - deviceOwner
	- framework
    

---

首先设置adb设置一下，可以看到报错

![oppo_adb_deviceOwner_fail.png](https://i.loli.net/2021/06/17/HjVrPzfJIEOU6nk.jpg)

是一个系统方法报的错，不是账户多用户的原因，所以应该去framework中去寻找，使用studio-Device File Explorer-system-framework下的jar包等文件中去查找

从报错路径可以知道应该是service和dpm相关的jar包

直接把相关jar包另存到文件夹

![oppo_framework.png](https://i.loli.net/2021/06/17/sNdjyWRYDogmQMc.jpg)

使用jadx反编译jar包，查找com.android.server.devicepolicy.DevicePolicyManagerService，并找到调用enforceCanSetDeviceOwnerLocked方法的位置

![oppo_setDeviceOwner.png](https://i.loli.net/2021/06/17/ZoObNriJIVWtdum.jpg)

找到后，可以看到是setDeviceOwner方法中调用了，与异常处符合，深入分析enforceCanSetDeviceOwnerLocked方法

![oppo_exception.png](https://i.loli.net/2021/06/17/SXurZAOY58TFBPh.jpg)

而异常处是Unexpected @provisioningPreCondition 99，所以应该分析checkDeviceOwnerProvisioningPreConditionLocked方法为什么返回的code是99

![oppo_deviceOwner_errorCode.png](https://i.loli.net/2021/06/17/aKJN5c4UgDm6Bxo.jpg)

其他都有固定的返回值，所以跟进OplusDevicePolicyUtils.checkPakcageState

![oppo_deviceOwner_checkPackageName.png](https://i.loli.net/2021/06/17/ZiTpINhVnx7qDeQ.jpg)

可以看到设备不支持deviceOwner的情况下，校验了应用的签名md5值，只有系统签名才能成功

至此分析完成