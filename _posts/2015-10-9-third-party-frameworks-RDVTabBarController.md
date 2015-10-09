### RDVTabBarController

- RDVTabBarController：一个十分完善的tabBarController，可以自定义角标个数，爽的停不下来。
- RDVTabBarController地址：<a href ="https://github.com/robbdimitrov/RDVTabBarController">RDVTabBarController</a>
- Demo地址：<a href ="https://github.com/sauchye/SYTipsDemo">欢迎Star</a>

---

### 说明

- 此教程是旨在让你快速入手，如需更加深层次的了解，请直接RDVTabBarController地址分析即可；

### 使用

``` objective-c
pod 'RDVTabBarController'
```

建议直接CocoaPods管理，对CocoaPods有兴趣的童鞋可以戳<a href="http://code4app.com/article/cocoapods-install-usage">cocoapods-install-usage</a>

### 结构

``` objective-c
RDVTabBar 
@interface RDVTabBar : UIView
```

``` objective-c
RDVTabBarController
@interface RDVTabBarController : UIViewController 
```

``` objective-c
RDVTabBarItem
@interface RDVTabBarItem : UIControl
```



RDVTabBarController Example Usage其实已经很详细了，接下来看初始化

``` objective-c
 //VString宏定义，为了就是更好的国际化语言，适配多语言，刚好此Demo也国际化了，可以参看https://github.com/sauchye/dev_notes/issues/4 🙈
#define VString(x)      NSLocalizedString(x, nil)
```

``` objective-c
- (void)setupViewControllers{
    SYFirstViewController *firstVC = [[SYFirstViewController alloc] init];
    SYSecondViewController *secondVC = [[SYSecondViewController alloc] init];
    SYThirdViewController *thirdVC = [[SYThirdViewController alloc] init];
    firstVC.title = VString(@"Home");
    secondVC.title = VString(@"Found");
    thirdVC.title = VString(@"Me");
    self.firstNav = [[SYBaseNavigationController alloc] initWithRootViewController:firstVC];
    self.secondNav = [[SYBaseNavigationController alloc] initWithRootViewController:secondVC];
    self.thirdNav = [[SYBaseNavigationController alloc] initWithRootViewController:thirdVC];
    [self setViewControllers:@[self.firstNav, self.secondNav, self.thirdNav]];
    [self customizeTabBarForController];
}
```

``` objective-c
- (void)customizeTabBarForController{

    //tabbar 背景图片 tabbar_background
    UIImage *backgroundImage = [UIImage imageNamed:@"tabbar_background"];
    //选项卡图片
    NSArray *tabBarItemImages;
  	//这里添加tabBar icon图片
    //= @[VString(@"First"), VString(@"Second"),VString(@"Third")];

    NSArray *tabBarItemTitles = @[VString(@"Home"), VString(@"Found"), VString(@"Me")];
    NSInteger index = 0;
    for (RDVTabBarItem *item in [[self tabBar] items])
    {
        item.titlePositionAdjustment = UIOffsetMake(0, 2.0);
        [item setBackgroundSelectedImage:backgroundImage withUnselectedImage:backgroundImage];
        UIImage *selectedimage = [UIImage imageNamed:[NSString stringWithFormat:@"%@_selected",[tabBarItemImages objectAtIndex:index]]];

        UIImage *unselectedimage = [UIImage imageNamed:[NSString stringWithFormat:@"%@_normal",[tabBarItemImages objectAtIndex:index]]];

        [item setFinishedSelectedImage:selectedimage withFinishedUnselectedImage:unselectedimage];

        [item setTitle:[tabBarItemTitles objectAtIndex:index]];
        item.selectedTitleAttributes = @{
                                         NSFontAttributeName: [UIFont boldSystemFontOfSize:12],
                                         NSForegroundColorAttributeName:kNAVIGATION_BAR_COLOR,
                                         };
        item.unselectedTitleAttributes = @{
                                           NSFontAttributeName: [UIFont boldSystemFontOfSize:12],
                                           NSForegroundColorAttributeName:RGB(217, 217, 217),
                                           };

        [item setTitle:[tabBarItemTitles objectAtIndex:index]];
        index++;

    }
}
```



### 这样你的tabBar基本搭建好了，但是还需要完善一些，比如，角标设置，push隐藏等。

- Push隐藏tabBar，你只需要这样即可
  
  ``` objective-c
  - (void)viewWillAppear:(BOOL)animated{
      [super viewWillAppear:animated];
      [[self rdv_tabBarController] setTabBarHidden:YES animated:YES];
  }
  ```
  
- 设置角标数
  
  ``` objective-c
   [[self rdv_tabBarItem] setBadgeValue:@"3"];
  ```
  
- RDVTabBarControllerDelegate，相信你看就会明白，好的方法命名很重要啊~
  
  ``` objective-c
  /**
   * Asks the delegate whether the specified view controller should be made active.
   */
  - (BOOL)tabBarController:(RDVTabBarController *)tabBarController shouldSelectViewController:(UIViewController *)viewController;
  
  /**
   * Tells the delegate that the user selected an item in the tab bar.
   */
  - (void)tabBarController:(RDVTabBarController *)tabBarController didSelectViewController:(UIViewController *)viewController;
  ```
  
- 还有需要多等待你去发现...

  ----

### 结语

  RDVTabBarController是一个很棒的第三方tabBarController，值得我们学习和思考。

- 相比传统第三方，你会发现可以很好的定制角标，这是极好的，当然你也可以自定义；
- 但是不能定义中间凸起的tabBar，好早之前去哪儿就是中间凸起一个tabBar，不过现在去哪儿也改成传统的tabBar了；​