---
layout:     post
title:      Android Device Monitor报错
subtitle:   报错分析
date:       2020-05-23
author:     JovenHe
header-img: img/tag-bg.jpg
catalog: true
tags:
    - 分析
    



---

An error has occurred. See the log file

报错log中显示

```
java.lang.NullPointerException
	at org.eclipse.core.runtime.URIUtil.toURI(URIUtil.java:280)
	at org.eclipse.e4.ui.internal.workbench.ResourceHandler.loadMostRecentModel(ResourceHandler.java:127)
	at org.eclipse.e4.ui.internal.workbench.swt.E4Application.loadApplicationModel(E4Application.java:370)
	at org.eclipse.e4.ui.internal.workbench.swt.E4Application.createE4Workbench(E4Application.java:220)
	at org.eclipse.ui.internal.Workbench$5.run(Workbench.java:557)
	at org.eclipse.core.databinding.observable.Realm.runWithDefault(Realm.java:332)
	at org.eclipse.ui.internal.Workbench.createAndRunWorkbench(Workbench.java:543)
	at org.eclipse.ui.PlatformUI.createAndRunWorkbench(PlatformUI.java:149)
	at com.android.ide.eclipse.monitor.MonitorApplication.start(MonitorApplication.java:63)
	at org.eclipse.equinox.internal.app.EclipseAppHandle.run(EclipseAppHandle.java:196)
	at org.eclipse.core.runtime.internal.adaptor.EclipseAppLauncher.runApplication(EclipseAppLauncher.java:110)
	at org.eclipse.core.runtime.internal.adaptor.EclipseAppLauncher.start(EclipseAppLauncher.java:79)
	at org.eclipse.core.runtime.adaptor.EclipseStarter.run(EclipseStarter.java:353)
	at org.eclipse.core.runtime.adaptor.EclipseStarter.run(EclipseStarter.java:180)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(Unknown Source)
	at java.lang.reflect.Method.invoke(Unknown Source)
	at org.eclipse.equinox.launcher.Main.invokeFramework(Main.java:629)
	at org.eclipse.equinox.launcher.Main.basicRun(Main.java:584)
	at org.eclipse.equinox.launcher.Main.run(Main.java:1438)
```

就是先在任务管理器进程里面关掉所有 monitor.exe 进程。 
再去删除monitor-workspace整个目录，我的在C:\Users\huangzhencheng\\.android里面，删除完重新打开成功。

