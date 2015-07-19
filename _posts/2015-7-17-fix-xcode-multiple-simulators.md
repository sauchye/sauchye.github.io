---
layout: post
title: Fix Xcode multiple simulators
description: 解决Xcode出现多个模拟器的问题
---
##前言
自从Apple向开发者开放Xcode 7 Beta版本时，我就下载了Xcode 7 Beta，安装Xcode 6.4和 Xcode 7 Beta 2个Xcode版本，但是最近出现以下问题截图：
![muti simulators](http://sauchye.com/images/dev/multi_simulators.png)
看到如上截图，说实话每次调试程序时也是dt，强迫症患者，估计更加难受。昨天在微博上看到，阳神<a href="http://weibo.com/p/1005051364395395/home?from=page_100505&mod=TAB#place">我就叫Sunny怎么了</a>微博，解决此问题，2句命令即可，亲测有效。

####首先退出Xcode并且关闭模拟器：

####然后在终端(Terminal)输入如下2行命令:

1. **sudo killall -9 com.apple.CoreSimulator.CoreSimulatorService**

2. **rm -rf ~/Library/Developer/CoreSimulator/Devices**

####最后重启Xcode，还你清爽的模拟器列表
![clear simulators](http://sauchye.com/images/dev/clear.png)




##结语

注：此博客如没有任何申明，皆属于原创，欢迎转载，转载请注明:<a href="http://sauchye.com/2015/07/17/fix-xcode-multiple-simulators.html">http://sauchye.com/2015/07/17/fix-xcode-multiple-simulators.html</a>不胜感激。



