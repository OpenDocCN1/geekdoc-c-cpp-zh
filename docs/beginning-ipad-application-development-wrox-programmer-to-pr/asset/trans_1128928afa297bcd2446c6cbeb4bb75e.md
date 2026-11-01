
![](img/744c5ec15e15ca7891c98be71dc25d13_77_0.png)

图 2-25

![](img/744c5ec15e15ca7891c98be71dc25d13_77_1.png)

图 2-26

## 3 视图、出口和动作

### 本章你将学到：

- 如何声明和定义 outlet
- 如何声明和定义 action
- 如何将 outlet 和 action 连接到 View 窗口中的视图
- 如何使用 UIAlertView 向用户显示警告视图
- 如何使用 UIActionSheet 向用户显示一些选项
- 如何使用 UIPageControl 控制分页
- 如何使用 UIImageView 显示图像
- 如何使用 UIWebView 在应用程序中显示 Web 内容
- 如何在运行时动态地向应用程序添加视图

在上一章中，你构建了一个简单的 Hello World! iPad 应用程序，而没有理解太多关于事物如何协同工作的底层细节。事实上，学习 iPad 编程的最大障碍之一是在你能够运行应用程序之前需要学习的大量细节。本书旨在使 iPad 编程体验既有趣又可承受。因此，本章从创建 iPad 应用程序用户界面（UI）的基础知识开始，以及你的代码如何与各种图形小部件连接。

## 出口和动作

在 iPad 编程中，你需要理解的第一件事之一就是 outlet 和 action。如果你熟悉 Java 或 C# 等传统编程语言，这是一个需要一些时间来适应的概念——概念相似，只是做事的方式不同。在本节结束时，你将对 outlet 和 action 是什么以及如何创建它们有坚实的理解，并开始创建出色的 iPad 应用程序。

6. Control-click 并拖动 OK Button 视图到 File's Owner 项（参见图 3-3）。选择名为 `btnClicked:` 的 action。

![](img/744c5ec15e15ca7891c98be71dc25d13_83_0.png)

图 3-3

7. 右键单击 OK Button 视图以显示其事件（参见图 3-4）。请注意，Button 视图有多个事件，但其中一个特定事件——Touch Up Inside——现在已连接到你指定的 action（`btnClicked:`）。由于 Touch Up Inside 事件使用非常频繁，当你 control-click 并将其拖动到 File's Owner 项时，它会自动连接到 action。要将其他事件连接到 action，只需单击每个事件旁边显示的圆圈，然后将其拖动到 File's Owner 项即可。

8. 就这样！按 Command-R 在 iPhone Simulator 上测试应用程序。输入一个名称在 TextField 中并点击 OK 按钮。警告视图会显示欢迎消息（参见图 3-5）。

![](img/744c5ec15e15ca7891c98be71dc25d13_83_1.png)

图 3-4

![](img/744c5ec15e15ca7891c98be71dc25d13_84_0.png)

图 3-5

### 工作原理

在 iPad 中，你使用 action 和 outlet 将代码连接到 UI 中的各种视图。将 action 视为传统面向对象编程世界中的方法，而 outlet 视为对象引用。Action 使用 IBAction 关键字表示，而 outlet 使用 IBOutlet 关键字：

```
#import <UIKit/UIKit.h>

@interface OutletsAndActionsViewController : UIViewController {
```

```
//---declaring the outlet---
IBOutlet UITextField *txtName;
}

//---expose the outlet as a property---
@property (nonatomic, retain) UITextView *txtName;

//---declaring the action---
-(IBAction) btnClicked: (id) sender;

@end
```

IBOutlet 标识符用于为变量添加前缀，以便 Interface Builder 可以与 Xcode 同步显示和连接 outlet。@property 关键字指示编译器你希望 txtName outlet 作为属性公开。nonatomic 关键字表示无需确保属性以线程安全的方式使用，因为它不会在多个线程中使用。默认行为是 atomic，指定 nonatomic 实际上提高了应用程序的性能。

> 注意 IBOutlet 标签也可以添加到 @property 标识符中。这种语法在 Apple 文档中很常见：
> 
> @property (nonatomic, retain) IBOutlet UITextField *txtName;

> 注意 有关 nonatomic 和 retain 标识符的使用，请参阅附录 D，在那里你可以找到 Objective-C 的介绍，Objective-C 是用于 iPad 编程的语言。此外，稍后讨论的 @synthesize 关键字也在那里有更详细的解释。

IBAction 标识符用于同步 action 方法。Action 是可以处理 View 窗口中视图引发的事件的方法（例如，当按钮被点击时）。另一方面，outlet 允许你的代码以编程方式引用 View 窗口上的视图。

一旦你在 View Controller 的头文件（.h）中添加了 action 和 outlet，你就需要将它们连接到 Interface Builder 中的视图。

当你 control-click 并拖动 File's Owner 项到 TextField 视图并选择 txtName 时，你本质上是将你创建的 outlet（txtName）与 View 窗口上的 TextField 视图连接起来。一般来说，要连接 outlet，你需要 control-click 并拖动 File's Owner 项到 View 窗口上的视图。

> 警告 一个快速提示：要将 outlet 连接到视图，你将 File's Owner 项拖到 View 窗口中所需的视图上。

要连接 action，你需要 control-click 并拖动一个视图到 File's Owner 项。因此，对于 OK Button 视图，你需要 control-click 并拖动 OK Button 视图到 File's Owner 项，然后选择名为 btnClicked 的 action。

> **警告** 一个快速提示：要连接 action，你从 View 窗口中的视图拖动到 File's Owner 项。

在实现文件（.m）中，你使用 @synthesize 关键字指示编译器为指定的属性创建 getter 和 setter：

> **常见错误** 忘记添加 @synthesize 关键字是开发人员最常犯的错误之一。请记住添加此语句，否则在应用程序执行时你将遇到运行时错误。附录 D 更详细地介绍了 getter/setter。

```objc
#import "OutletsAndActionsViewController.h"

@implementation OutletsAndActionsViewController

//---synthesize the property---
@synthesize txtName;

//---displays an alert view when the button is clicked---
-(IBAction) btnClicked:(id) sender {
    NSString *str = [[NSString alloc]
        initWithFormat:@"Hello, %@", txtName.text];
    UIAlertView *alert = [[UIAlertView alloc]
        initWithTitle:@"Hello!"
        message:str
        delegate:self
        cancelButtonTitle:@"Done"
        otherButtonTitles:nil];
    
    [alert show];
    [str release];
    [alert release];
}

- (void)dealloc {
    //---release the outlet---
    [txtName release];
    [super dealloc];
}
```

btnClicked: action 只显示一个包含用户姓名的消息的警告视图。请注意它有一个类型为 id 的参数 sender。sender 参数允许你以编程方式找出实际调用此 action 的对象。这在你有多个视图连接到单个 action 时很有用。对于这种情况，你通常需要知道哪个视图调用了此方法，而 sender 参数将包含对调用视图的引用。

## 使用视图

到目前为止，你已经看到了许多视图在运行——Round Rect Button、TextField 和 Label。所有这些视图都非常简单，但它们为你提供了理解 outlet 和 action 背后概念的好机会。

要使用更多视图，你可以从 Interface Builder 中的 Library 窗口中定位它们（参见图 3-6）。

![](img/744c5ec15e15ca7891c98be71dc25d13_87_0.png)

图 3-6

库分为以下几个部分：

- Controllers — 包含控制其他视图的视图，例如 View Controller、Tab Bar Controller、Navigation Controller 等
- Data Views — 包含显示数据的视图，例如 Image View、Table View、Data Picker、Picker View 等

