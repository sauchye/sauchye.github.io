---
layout: post
title: Submit App to App Store
description: 提交App到App Store的那些事
---

##前言

前几个月一直忙碌公司iOS端App开发，所以没时间管理自己博客，最近看到一篇文章，让我鼓足勇气开通自己的Blog，博客现在还不是很完善，有时候解析出错，这跑题了，进入正题~O(∩_∩)O~


##App前期准备工作
公司的开发者账号老大已注册好，So，我只需要配置好证书开发就好！我们使用的是git开发管理代码，虽然GitHub很赞，众所周知：国内访问和操作<a href="https://www.github.com">GitHub</a>都是很慢的，所以我们托管在<a href="https://git.oschina.net/">Git OSChina</a>，在此感谢他们提供的平台。其实git多人开发会出现很多问题，冲突啥的都会有，所以解决冲突也比较费劲，所以我们用<a href="https://github.com/sauchye/FixMergeConflict">FixMergeConflict</a>插件解决冲突，间接提高了开发效率，由于开发需要查看进度，测试BUG等，我们又将App内测发布到<a href="http://fir.im/">fir.im</a>上，方便测试，其实国内App内测还有<a href="http://www.pgyer.com/">蒲公英</a>，只是我习惯了fir，所以就选择了fir，那么问题又来了，每天打包，用Xcode Archive是不是很烦躁，所以你可以选择这个插件<a href="https://github.com/sauchye/DailyPackagedForiOS">DailyPackagedForiOS</a>，从此麻麻再也不用担心我打包烦躁的事啦，哈哈哈~

##使用到的第三框架
* 网络处理:<a href="https://github.com/AFNetworking/AFNetworking">AFNetworking</a>
* 图片加载:<a href="https://github.com/rs/SDWebImage">SDWebImage</a>
* 数据库管理:<a href="https://github.com/ccgus/fmdb">fmdb</a>
* 自动布局:<a href="https://github.com/SnapKit/Masonry">Masonry</a>
* 数据模型转换:<a href="https://github.com/Mantle/Mantle">Mantle</a>
* 富文本:<a href="https://github.com/TTTAttributedLabel/TTTAttributedLabel
">TTTAttributedLabel</a> 
* 视图加载提示框:<a href="https://github.com/jdg/MBProgressHUD
">MBProgressHUD</a>
* 图片选择器:<a href="https://github.com/chiunam/CTAssetsPickerController">CTAssetsPickerController</a>
* MJ刷新:<a href="https://github.com/CoderMJLee/MJRefresh">MJRefresh</a>
* MJ图片加载:<a href="https://github.com/azxfire/MJPhotoBrowser">MJPhotoBrowser</a>
* 很强大的tabBarController:<a href="https://github.com/robbdimitrov/RDVTabBarController">RDVTabBarController</a>
* 输入框键盘遮挡:<a href="https://github.com/michaeltyson/TPKeyboardAvoiding">TPKeyboardAvoiding</a>

以上都是Cocoapods管理第三方类库，如需安装<a href="http://code4app.com/article/cocoapods-install-usage">Cocoapods</a>教程。排名不分先后，感谢他们的开源精神，使得我们有更多的时间去优化我们的App,还有其它暂未列出。同时感谢我之前的老大<a href="http://www.heyuan110.com/">Bruce</a>在他身上让我学到了很多，感谢他的指导，还有我的另一位伙伴<a href="https://github.com/chenrenjie">chenrenjie</a>；同时感谢<a href="https://coding.net/u/coding/p/Coding-iOS/git">Coding-iOS</a>的开源，感觉学到许多，很赞的源代码。

##推送
经过和老大的讨论，最终选择腾讯信鸽推送<a href="http://xg.qq.com/">信鸽推送</a>

##短信验证码
采用<a href="http://mob.com">mob</a>（原ShareSdk）短信验证。

##第三方社交与社交分享
采用<a href="http://www.umeng.com/">友盟</a>的第三方授权登录：腾讯QQ，微信，微博以及分享，自我感觉友盟的技术客服妹纸服务态度很赞哦！

##Crashlytics BUG追踪神器
使用Crashlytics bug追踪，不懂的童鞋可以参看<a href="http://www.devtang.com/blog/2013/07/24/use-crashlytics/">巧哥博客介绍Crashlytics</a>，Crashlytics太强大了，让你的BUG无处存在，你的项目集成了他，可以定位到哪一行Crash，接下来就看你的了。



##iOS App上架那些事
终于到了可以Release App发布到App Store，此时无比开森，有木有。毕竟可以不再那么的赶进度，那些日子确实是煎熬，但是现在看来一切都是值得的。但是我们发布到App Store时需要注意很多，毕竟Apple的审核是相当严的，一不小心就被reject了，这种感觉真差劲，其实被拒也木有那么好纠结的，只要弄清问题所在更改就好。我们App被reject2次，幸运的是第三次审核通过，刚好今早在App Store搜索，奇迹般App出现在App Store上，内心无比激动，其实预计这2天会出结果，说实话每天凌晨和早上都会第一时间在App Store搜索我们的App。

##第一次被拒
等待漫长的2周，最后老大收到Review的邮件截图给我，当时我还在琢磨Review，有道一查，才明白App可能被reject了，那时候老大不知道权当App开始审核了，上<a href="https://itunesconnect.apple.com">itunesconnect.apple.com</a>，果真被拒了，如需要App加急审核<a href="https://developer.apple.com/contact/app-store/?topic=expedite">戳</a>。

>"Multitasking Apps may only use background services for their intended purposes: VoIP, audio playback, location, task completion, local notifications, etc"   
</br>
     
>"Apple and our customers place a high value on simple, refined, creative, well thought through interfaces. They take more work but are worth it. Apple sets a high bar. If your user interface is complex or less than very good, it may be rejected"

以上2点是第一次提交App时Apple被拒的主要原因，其实还有一个就是我们第一版本就添加"检查更新按钮"，Apple也截图给我们了，我们只能修改了，将检查更新去掉了，更改了Apple列举的问题。很纳闷，为啥Apple审核不把App出现的问题都列举出来，导致我们第二次也被拒，Apple审核人员太坏了，没办法我们只能尽量避免。

##第二次被拒
又等待一周的时间，审核结果出来了，App再次被拒原因主要有两点：
###登录有问题
###活动页面没有添加"本活动与苹果无关"
被无情的拒绝后，丧心肠断剑，过儿的黯然销魂掌，伤心太平洋...此时感觉有点无力了，呵呵呵呵~再怎么无力也要发布App啊，我特么怀疑Apple审核人员用模拟器测试App，再想想根据我们登录时的字段加入了DeviceToken所以没有Token是登录不了的，但是再想想有时候会获取不到Token，此时自己又狠狠的呵呵了一把自己，既然出问题了，那就改改改，改完再提交。经过大概9天App出现在App Store了，无比激动了。

##结语
希望以上被拒对准备上架App的童鞋有所帮助，在此感谢他们的开源精神，感谢共患难的队友，感谢！

注：此博客如没有任何申明，皆属于原创，欢迎转载，转载请注明:<a href="http://sauchye.com/2015/06/28/submit-app-to-app-store.html">http://sauchye.com/2015/06/28/submit-app-to-app-store.html</a>不胜感激。


