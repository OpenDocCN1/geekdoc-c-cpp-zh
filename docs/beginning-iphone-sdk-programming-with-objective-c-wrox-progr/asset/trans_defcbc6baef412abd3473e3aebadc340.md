

![](img/16991b58db5894715c4a443315e06a22_240_0.png)

## 实用应用程序

### 本章学习内容

-   如何使用 SDK 提供的模板开发实用应用程序
-   了解如何在实用应用程序中翻转视图
-   如何在翻转视图时应用不同的过渡样式
-   如何向实用应用程序添加更多视图

前面两章演示了使用 iPhone SDK 可以构建的几种应用程序类型：基于视图的应用程序、基于导航的应用程序和标签栏应用程序。在 iPhone 中另一种常见的应用程序类型是*实用应用程序*。实用应用程序是一种执行简单任务、需要最少用户输入的应用程序。iPhone 自带的“天气”和“股票”应用程序就是两个很好的实用应用程序示例。图9-1显示了天气应用程序展示特定城市天气的界面。当你触摸屏幕右下角的小 i 图标时，屏幕会翻转到另一个屏幕。视图翻转是实用应用程序的特征之一。

![](img/16991b58db5894715c4a443315e06a22_243_0.png)

### 图9-3

### 工作原理

实用应用程序所需的大部分工作已经为你完成。但了解其内部工作原理总是一件好事，这样你就可以扩展它以供自己使用。

正如你所看到的，该项目包含两个由两个视图控制器控制的主视图：MainViewController 和 FlipsideViewController。

首先，检查 FlipsideViewController.h 文件的内容：

```
@protocol FlipsideViewControllerDelegate;

@interface FlipsideViewController : UIViewController {
    id <FlipsideViewControllerDelegate> delegate;
}
@property (nonatomic, assign) id <FlipsideViewControllerDelegate> delegate;

- (IBAction)done;

@end

@protocol FlipsideViewControllerDelegate
- (void)flipsideViewControllerDidFinish:(FlipsideViewController *)controller;
@end
```

注意，在此控制器中，代码定义了一个名为 FlipsideViewControllerDelegate 的协议，其中包含一个名为 flipsideViewControllerDidFinish: 的方法。通过该协议，FlipsideViewController 然后暴露了一个类型为 FlipsideViewControllerDelegate 的名为 delegate 的属性。flipsideViewControllerDidFinish: 的实际实现：

现在你可以检查 MainViewController.h 文件：

```
#import "FlipsideViewController.h"

@interface MainViewController : UIViewController <FlipsideViewControllerDelegate> {
}
- (IBAction)showInfo;

@end
```

注意，MainViewController 实现了 FlipsideViewControllerDelegate 协议。换句话说，它必须实现在协议中定义的方法（在本例中为 flipsideViewControllerDidFinish: 方法）。

在 MainViewController.m 文件中，定义了一个名为 flipsideViewControllerDidFinish: 的方法。它的作用是在完成后关闭 FlipsideView：

```
- (void)flipsideViewControllerDidFinish:(FlipsideViewController *)controller {
    [self dismissModalViewControllerAnimated:YES];
}
```

MainViewController.m 文件还包含一个名为 showInfo() 的操作。当用户按下 Info 按钮时，会调用该操作。showInfo() 操作以模态方式加载 FlipsideView：

```
- (IBAction)showInfo {

    FlipsideViewController *controller = [[FlipsideViewController alloc]
    initWithNibName:@"FlipsideView"
    bundle:nil];

    controller.delegate = self;

    controller.modalTransitionStyle = UIModalTransitionStyleFlipHorizontal;
    [self presentModalViewController:controller animated:YES];

    [controller release];
}
```

如果你双击 MainView.xib 在 Interface Builder 中编辑它，可以右键单击 Info 按钮，确认其 Touch Up Inside 事件已连接到 showInfo() 操作（参见图9-5）。

![](img/16991b58db5894715c4a443315e06a22_246_0.png)

### 图9-5

就是这样——一个无需编写任何代码就能神奇运行的实用应用程序！

### 过渡样式

在上一节中，你看到当按下 i 信息按钮时，视图翻转以显示另一个视图。这是由 ViewController 类的 modalTransitionStyle 属性控制的：

```
- (IBAction)showInfo {

    FlipsideViewController *controller = [[FlipsideViewController alloc]
        initWithNibName:@"FlipsideView"
        bundle:nil];

    controller.delegate = self;

    controller.modalTransitionStyle = UIModalTransitionStyleFlipHorizontal;
    [self presentModalViewController:controller animated:YES];
    [controller release];
}
```

> 注意：modalTransitionStyle 属性仅在 iPhone SDK 3.0 中可用。如果你尝试使用旧版本的 SDK 运行应用程序，它将无法工作。

默认的过渡是水平翻转，即主视图水平翻转（参见图9-6）以显示 FlipsideView。

除了水平翻转外，你还可以垂直翻转视图或使其缓慢溶解。这些功能由以下常量控制（以粗体显示）：

```
//---flip vertically---
controller.modalTransitionStyle =
UIModalTransitionStyleCoverVertical;

//---dissolves slowly to reveal another view---
controller.modalTransitionStyle =
UIModalTransitionStyleCrossDissolve;
```

作为练习，你应该尝试修改过渡样式，亲自看看它们之间的区别。

![](img/16991b58db5894715c4a443315e06a22_247_0.png)

### 向实用应用程序添加另一个视图

现在你已经了解了如何使用 SDK 提供的模板创建实用应用程序，你可能希望向应用程序添加更多视图，使其具有更多功能。回到 iPhone 上的天气应用程序，注意翻转后的视图中有一个额外的加号（+）按钮，允许你添加更多天气信息（参见图9-7）。

![](img/16991b58db5894715c4a443315e06a22_247_1.png)

16. 在 FlipsideViewController.m 文件中，插入以下以粗体显示的代码：

```
//---defines the addCountryViewControllerDidFinish: method---
- (void)addCountryViewControllerDidFinish:(AddCountryViewController *)controller {
    [self dismissModalViewControllerAnimated:YES];
}

//---defines the add: action---
- (IBAction)add {
    AddCountryViewController *controller = [[AddCountryViewController alloc]
                                            initWithNibName:@"AddCountryView"
                                            bundle:nil];
    controller.delegate = self;
    //---use the vertical transition---
    controller.modalTransitionStyle =
    UIModalTransitionStyleCoverVertical;
    [self presentModalViewController:controller
           animated:YES];
    [controller release];
}
```

17. 就这样！按 Command-R 将应用程序部署到 iPhone 模拟器上。图9-13显示了当你按下 + 按钮时，AddCountryView 垂直向上移动。

18. 按下 Done 按钮将隐藏 AddCountryView。

### 工作原理

本示例说明了向实用应用程序添加更多视图所需的步骤。你首先创建附加视图的 XIB 文件及其对应的 UIViewController 类。在此控制器中，你定义一个协议：

```
//---defines the protocol---
@protocol AddCountryViewControllerDelegate
- (void)addCountryViewControllerDidFinish:(AddCountryViewController *)controller;
@end
```

然后你暴露一个该协议类型的属性：

```
@interface AddCountryViewController : UIViewController {
    //---delegate---
    id <AddCountryViewControllerDelegate> delegate;
}

//---exposes the delegate as a property---
@property (nonatomic, assign) id <AddCountryViewControllerDelegate> delegate;
```

将调用此新视图的视图需要实现此协议中定义的方法，如下所示：

![](img/16991b58db5894715c4a443315e06a22_252_0.png)

