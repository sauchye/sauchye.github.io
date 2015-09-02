---
layout: post
title: 跳转到第三方地图导航的那些事
category: ios
description: 看似如此简单的需求，有可能会被大脸~
---

## 前言

这几天玩了玩跳转到第三方地图导航，刚好看到<a href="http://weibo.com/ljc1986">**adad184**</a>大大的介绍<a href="http://adad184.com/2015/08/11/practice-in-mapview-navigation-with-URI/">**URI跳转方式地图导航的代码实践**</a>刚好拿下了，有兴趣的童鞋可以参考参考，非常赞，在此感谢大大们的无私奉献，让我这小菜菜少走不少弯路~

## 遇到的一些问题

<a href="http://weibo.com/ljc1986">**adad184**</a>大大的介绍已经很清楚了还附带了呆萌(Demo)，所以我主要记录下我在实际开发中遇到的一些问题，或许你也会遇到哦，所以呢，可以一看哦！说说我们**项目需求**：通过讨论后确定了三种地图：*苹果地图*，*百度地图*，*高德地图*，可供用户选择，我发现一些导航到地图导航的第三方Apps，基本都是你的设备安装哪个地图应用就会显示出来，没安装的就不显示，确实这点自我感觉体验比较好点，但是和PM交流我的这一想法时，PM坚持了固定这三种地图，“安装了就跳转到该应用，没有安装就跳到App Store，提示用户下载，不过这样真的好么？”，也就是写死，o(╯□╰)o，只能写死啰！写死再简单不过，不过我还是实现了自动检测这一功能。



- #### 自动检测是否安装某应用：
  
  思路大概是这样，首先检测iOS设备是否安装了该应用，需要知道对应应用的urlScheme，如检测高德和百度地图是否被安装到iOS设备上：

``` objective-c
- (NSArray *)checkInstallMapApps{
 	NSArray *mapSchemeArr = @[@"iosamap://navi",@"baidumap://map/"];
	NSMutableArray *appListArr = [[NSMutableArray alloc] initWithObjects:@"苹果地图", nil];
	for (int i = 0; i < [mapSchemeArr count]; i++) {
    	if ([[UIApplication sharedApplication] canOpenURL:[NSURL URLWithString:[NSString stringWithFormat:@"%@",[mapSchemeArr objectAtIndex:i]]]]) {
        	if (i == 0){
            	[appListArr addObject:@"高德地图"];
        	}else if (i == 1){
            	[appListArr addObject:@"百度地图"];
        		}
    		}
		}
		return appListArr;
      }
```

这样就获取到了你的设备安装的地图应用，so easy吧，就是这样。我们应用是支持iOS7+，接下来自定义弹出的视图就好。

- #### 还有一个就是导航到终点的位置偏差很大
  
  导航到终点的位置偏差很大，这是一个比较dt的事，我们采用的是百度地图SDK，所以只需要这会误导用户。发现在苹果地图，高德地图，百度地图，导航到指定终点，偏差相同，于是第一时间检查，传参，发现传参没有问题，于是开始了抓狂的Search，得知在传参经纬度时需要将经纬度转换下，于是找到修改得到这样一份代码，导航位置貌似立刻变得精准了，俗称是**火星转码**，看传参应该很容易，所以传转码后的参数应该就好了，如果位置还是很偏，请舍弃这段代码，提issues到地图SDK，或者您有更好的方法，如果您也热爱分享，希望您能告诉我，或者直接<a href="https://github.com/sauchye/DemoNavigationURI/pulls">pull request</a>，感激不尽。



``` objective-c
- (CLLocationCoordinate2D)transformCoordinatesLatitude:(double)latitude 
  											 longitude:(double)longitude{  
                                               
  double x = longitude - 0.0065, y = latitude - 0.006;
  double z = sqrt(x * x + y * y) - 0.00002 * sin(y * M_PI);
  double theta = atan2(y, x) - 0.000003 * cos(x * M_PI);
  double gg_lng = z * cos(theta);
  double gg_lat = z * sin(theta);
  CLLocationCoordinate2D coor = CLLocationCoordinate2DMake(gg_lat, gg_lng);
  return coor;
  }
```

  		

  检测是否安装某应用以及导航位置偏差较大，放出呆萌(Demo)，有兴趣的童鞋看看:<a href="https://github.com/sauchye/DemoNavigationURI">基于DemoNavigationURI</a>

  最后，注意iOS9在urlScheme添加了白名单限制，所以在你的应用plist下一定添加这些urlScheme在如下截图位置，否则无法检测已安装的应用。

plist->LSApplicationQueriesSchemes

![add urlscheme](http://sauchye.com/images/dev/add_url_scheme.png)



## 参考

<a href="http://adad184.com/2015/08/11/practice-in-mapview-navigation-with-URI/">**URI跳转方式地图导航的代码实践**</a>

## 结语

或许是自己木有仔细查看百度地图SDK，所以需要自己耐心去发现，希望对同此需求的童鞋少走弯路，祝大家玩的开心！

*注：此博客如没有任何申明，皆属于原创，欢迎转载，转载请注明，不胜感激！*