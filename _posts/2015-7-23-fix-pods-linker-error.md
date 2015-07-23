---
layout: post
title: Fix Pods Linker error
description: 解决Xcode中Pods引用出错
---

这两天整理项目时发现，工程在**Release**模式下，能够正常运行，而在**Debug**下却运行失败，**Pods**出错，如下

error:*Apple Mach-O Linker Error "_OBJC_CLASS_$_MASConstraint",referenced from:*

![Pods linker_error](http://sauchye.com/images/dev/pod_linker_error.png)


纠结了好久，毕竟项目工程引入了不少pods类库。于是到处询问，搜索得知。

1.首先：先进入Pods->Architectures->Build Active Architecture Only将其全部设置成**NO**

![Pods linker_error](http://sauchye.com/images/dev/pod_modify.png)

2.然后，回到工程，Targets(选中工程名那个，非Tests)->Build Settings->Build Active Architecture Only->Debug设置成**YES**即可，PS:这里可能由于我手贱，所以出现Pods引用出错，o(╯□╰)o。
![Pods linker_error](http://sauchye.com/images/dev/modify.png)


参考：<a href="http://blog.csdn.net/sunyazhou13/article/details/10070063">http://blog.csdn.net/sunyazhou13/article/details/10070063</a>



*注：此博客如没有任何申明，皆属于原创，欢迎转载，转载请注明，不胜感激！*




