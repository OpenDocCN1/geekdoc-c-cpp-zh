
![](img/aab2d775c46f70cd606f2e58e2521324_180_0.png)

2. 通过查看 Size Inspector 窗口来观察其大小和定位。这里，其位置为 (20,20)，大小为 280 x 37。

3. 通过点击窗口右上角的箭头图标来旋转 View 的方向（见图 6-8）。

4. 通过将其重新定位到 View 窗口的右下角来重新定位 Round Rect Button 视图。也请观察并记录其位置。

![](img/aab2d775c46f70cd606f2e58e2521324_180_1.png)

![](img/aab2d775c46f70cd606f2e58e2521324_180_2.png)

7. 在 Interface Builder 中保存项目。

8. 返回 Xcode，将以下代码插入 ScreenRotationsViewController.h 文件中：

```objc
#import <UIKit/UIKit.h>

@interface ScreenRotationsViewController : UIViewController {
    IBOutlet UIButton *btn;
}
@property (nonatomic, retain) UIButton *btn;
@end
```

9. 在 ScreenRotationsViewController.m 文件中，添加以下代码：

```objc
@implementation ScreenRotationsViewController

@synthesize btn;

...
- (void)willAnimateSecondHalfOfRotationFromInterfaceOrientation:(UIInterfaceOrientation)fromInterfaceOrientation duration:(NSTimeInterval)duration {
    UIInterfaceOrientation destOrientation = self.interfaceOrientation;
    if (destOrientation == UIInterfaceOrientationPortrait) {
        //---if rotating to portrait mode---
        btn.frame = CGRectMake(20,20,280,37);
    }
    else {
        //---if rotating to landscape mode---
        btn.frame = CGRectMake(180,243,280,37);
    }
}
- (void)dealloc {
    [btn release];
    [super dealloc];
}
```

10. 保存项目并在 Xcode 中按 Command-R 将应用程序部署到 iPhone Simulator 上。

11. 观察到当 iPhone Simulator 处于竖屏模式时，Round Rect Button 视图显示在左上角。但当你将方向更改为横屏模式时，它会被重新定位到右下角（见图 6-12）。

![](img/aab2d775c46f70cd606f2e58e2521324_183_0.png)

**图 6-12**

## 工作原理

本项目说明了当设备方向改变时，你如何重新定位应用程序上的视图。你首先创建一个 outlet 并将其连接到 View 窗口上的 Round Rect Button 视图。

当设备正在旋转时，你处理 `willAnimateSecondHalfOfRotationFromInterfaceOrientation:` 事件，因为这样可以让你知道设备正在改变到的目标方向。在此方法中，你可以使用 `fromInterfaceOrientation` 参数获取目标方向，或者可以通过当前 View（self）的 `interfaceOrientation` 属性获取，如下所示：

```objc
UIInterfaceOrientation destOrientation = self.interfaceOrientation;
```

利用这些信息，你通过更改其 frame 属性根据目标方向定位视图：

```objc
if (destOrientation == UIInterfaceOrientationPortrait)
{
    btn.frame = CGRectMake(20,20,280,37);
}
else
{
    btn.frame = CGRectMake(180,243,280,37);
}
```

## 处理视图定位的属性

在前面的示例中，你使用了 `frame` 属性在运行时更改视图的位置。`frame` 属性定义了视图相对于其 superview（包含它的视图）所占的矩形。使用 `frame` 属性可以设置视图的定位和大小。除了使用 `frame` 属性外，你还可以使用 `center` 属性，它设置视图的中心，也相对于其 superview。你通常在执行某些动画并且只想更改视图位置时使用 `center` 属性。

## 以编程方式旋转屏幕

在上一节中，你看到了当用户旋转设备时你的应用程序如何处理设备方向的变化。然而，有时（例如当你开发游戏时），你希望强制应用程序在特定方向显示，而与设备如何握持无关。

有两种情况需要考虑：

- 在应用程序运行时以编程方式旋转屏幕方向；或
- 在 View 加载时以特定方向显示屏幕。

### 运行时旋转

在运行时，你可以通过在 `UIDevice` 类的实例上使用 `setOrientation:` 方法以编程方式旋转屏幕。使用前面创建的项目，假设你希望用户在按下 Round Rect Button 视图时更改屏幕方向。你可以按如下方式编码：

```objc
- (IBAction)btnClicked:(id)sender
{
    [[UIDevice currentDevice] setOrientation:UIInterfaceOrientationLandscapeLeft];
}
```

`setOrientation:` 方法接受一个单一参数，指定你想要更改到的方向。

> **注意：** 在以编程方式切换应用程序的方向后，当你物理旋转设备时，应用程序的旋转仍可能发生变化。可以更改到的方向取决于你在 `shouldAutorotateToInterfaceOrientation:` 方法中设置的设置。

### 在加载时以特定方向显示视图

当 View 加载时，默认情况下它始终以竖屏模式显示。如果你的应用程序要求在加载时以特定方向显示 View，你可以通过设置状态栏的方向来做到这一点，如下所示：

```objc
- (void)viewDidLoad {
    [UIApplication sharedApplication].statusBarOrientation
        = UIInterfaceOrientationLandscapeRight;
    [super viewDidLoad];
}
```

值得注意的是，上一节中描述的 `setOrientation:` 方法不能用于在加载时更改 View 的方向：

```objc
//—does not work during View loading time—
[[UIDevice currentDevice] setOrientation:UIInterfaceOrientationLandscapeLeft];
```

同样，在运行时（View 加载后）设置状态栏方向不起作用：

```objc
//—does not work during run time—
[[UIApplication sharedApplication] setStatusBarOrientation:
    UIInterfaceOrientationLandscapeLeft];
```

> **注意：** 你要更改到的方向必须首先在 `shouldAutorotateToInterfaceOrientation:` 事件中指定。这也可以在应用程序的 `Info.plist` 文件中指定，通过将 `InitialInterfaceOrientation` 键设置为所需方向。

## 摘要

在本章中，你已经看到了屏幕方向的变化如何由视图控制器类中的各种事件处理。正确处理屏幕方向将使你的应用程序更易用并改善用户体验。

## 练习

1. 假设你希望你的应用程序仅支持横屏右和横屏左方向。你应该如何修改你的代码？

2. 视图的 frame 和 center 属性之间有什么区别？

## 本章学到的内容

| 主题 | 关键概念 |
|---|---|
| 处理设备旋转 | 实现 `shouldAutorotateToInterfaceOrientation:` 方法 |
| 支持的四种方向 | `UIInterfaceOrientationPortrait`<br>`UIInterfaceOrientationLandscapeLeft`<br>`UIInterfaceOrientationLandscapeRight`<br>`UIInterfaceOrientationPortraitUpsideDown` |
| 设备旋转时触发的事件 | `willAnimateFirstHalfOfRotationToInterfaceOrientation:`<br>`willAnimateSecondHalfOfRotationFromInterfaceOrientation:`<br>`willRotateToInterfaceOrientation:`<br>`willAnimateRotationToInterfaceOrientation:` |
| 用于更改视图位置的属性 | 使用 `frame` 属性更改视图的定位和大小<br>使用 `center` 属性更改视图的定位 |

## 第二部分

## 构建不同类型的 iPhone 应用程序

- 第 7 章：视图控制器
- 第 8 章：标签栏和导航应用程序
- 第 9 章：实用工具应用程序

