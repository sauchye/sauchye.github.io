---
layout: post
title: 处理Xcode出现多个模拟器
categories: Xcode
description: Xcode出现多个模拟器
keywords: Xcode、simulator
---



自从Apple向开发者开放Xcode 7 Beta版本时，我就下载了Xcode 7 Beta，安装Xcode 6.4和 Xcode 7 Beta 2个Xcode版本，但是最近出现以下问题截图：

看到如上截图，说实话每次调试程序时也是dt，强迫症患者，估计更加难受。在微博上看到，阳神@[我就叫Sunny怎么了](http://weibo.com/p/1005051364395395/)微博，解决此问题，2句命令即可，亲测有效。

####首先退出Xcode并且关闭模拟器：

####然后在终端(Terminal)输入如下2行命令:

```
1、 sudo killall -9 com.apple.CoreSimulator.CoreSimulatorService
2、 rm -rf ~/Library/Developer/CoreSimulator/Devices
```

####重启Xcode，还你清爽的模拟器列表