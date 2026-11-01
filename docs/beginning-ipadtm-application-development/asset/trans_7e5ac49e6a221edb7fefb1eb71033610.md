

## 3 视图、输出口和动作

### 本章学习内容

- 如何声明和定义输出口
- 如何声明和定义动作
- 如何将输出口和动作连接到视图窗口中的视图
- 如何使用 `UIAlertView` 向用户显示警告视图
- 如何使用 `UIActionSheet` 向用户显示一些选项
- 如何使用 `UIPageControl` 控制分页
- 如何使用 `UIImageView` 显示图像
- 如何使用 `UIWebView` 在应用程序中显示 Web 内容
- 如何在运行时动态地向应用程序添加视图

在上一章中，你构建了一个简单的 Hello World! iPad 应用程序，但没有过多了解各个部分如何协同工作的底层细节。事实上，学习 iPad 编程的最大障碍之一是，在应用程序能够正常运行之前，需要学习大量细节。本书旨在让 iPad 编程体验既有趣又不那么难以承受。因此，本章从创建 iPad 应用程序用户界面（UI）的基础知识开始，并介绍你的代码如何与各种图形组件建立连接。

### 输出口和动作

在 iPad 编程中，你首先需要理解的就是输出口和动作。如果你熟悉传统编程语言（如 Java 或 C#），这个概念需要一些时间来适应——概念相似，只是做事的方式不同。在本节结束时，你将扎实理解什么是输出口和动作，以及如何创建它们，并可着手创建出色的 iPad 应用程序。

#### 试一试：创建输出口和动作

1. 使用 Xcode 创建一个基于视图的应用程序项目，并将其命名为 `OutletsAndActions`。

2. 双击 `OutletsAndActionsViewController.xib` 文件，在 Interface Builder 中打开它进行编辑。Interface Builder 加载后，双击 `OutletsAndActionsViewController.xib` 窗口中的 View 项，以可视化方式显示视图窗口（见图3-1）。将三种视图放到视图窗口上——标签（Label）、文本框（TextField）和按钮（Button）。双击标签视图，将文本设置为“Enter your name”。同时，将按钮设置为“OK”字符串。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_81_0.png)

**图3-1**

3. 在 Xcode 中，使用以下加粗语句修改 `OutletsAndActionsViewController.h` 文件：

```objc
#import <UIKit/UIKit.h>

@interface OutletsAndActionsViewController : UIViewController {
    //---declaring the outlet---
    IBOutlet UITextField *txtName;
}
```

`btnClicked:` 动作只是显示一个警告视图，其中包含包含用户姓名的消息。请注意，它有一个 `id` 类型的参数 `sender`。`sender` 参数允许你以编程方式找出究竟是谁调用了这个动作。当多个视图连接到一个动作时，这非常有用。在这种情况下，你通常需要知道是哪个视图调用了此方法，而 `sender` 参数将包含对调用视图的引用。

### 使用视图

到目前为止，你已经看到了相当多的视图在发挥作用——圆角矩形按钮（Round Rect Button）、文本框（TextField）和标签（Label）。所有这些视图都很简单，但它们为你提供了理解如何应用输出口和动作背后概念的绝佳机会。

要使用更多视图，你可以在 Interface Builder 的库窗口中找到它们（见图3-6）。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_87_0.png)

**图3-6**

库分为以下几个部分：

- **控制器（Controllers）** — 包含控制其他视图的视图，例如视图控制器（View Controller）、标签栏控制器（Tab Bar Controller）、导航控制器（Navigation Controller）等
- **数据视图（Data Views）** — 包含显示数据的视图，例如图像视图（Image View）、表视图（Table View）、日期选择器（Date Picker）、选择器视图（Picker View）等
- **输入和值（Inputs and Values）** — 包含接受用户输入以及显示值的视图，例如标签（Label）、圆角矩形按钮（Round Rect Button）、文本框（Text Field）等
- **窗口、视图和栏（Windows, Views and Bars）** — 包含显示其他各种视图的视图，例如视图（View）、搜索栏（Search Bar）、工具栏（Toolbar）等

在接下来的小节中，你将学习如何使用库中可用的部分视图。虽然本书的范围不包括展示每个视图的用法，但你将有机会在全书看到许多视图的实际应用。在本章中，你将学习处理视图的一些基本概念，以便可以毫无问题地使用其他视图。

#### 使用警告视图

库中未列出的视图之一是 `UIAlertView`。`UIAlertView` 向用户显示一个警告视图，通常是在运行时创建的。因此，你必须使用代码来创建它。

> **注意** 你实际上在第2章中见过 `UIAlertView`。在本节中，你将看到它实际是如何工作的。

当你需要向用户显示消息时，`UIAlertView` 非常有用。此外，当你想在运行时观察变量的值时，它还可以作为快速调试工具。

下面的练习将更详细地探讨 `UIAlertView`。请按指示下载代码。

#### 试一试：使用警告视图

*代码文件 UsingViews.zip 可在 Wrox.com 下载*

1. 使用 Xcode 创建一个新的基于视图的应用程序项目，并将其命名为 `UsingViews`。

2. 在 `UsingViewsViewController.m` 文件中，将以下加粗代码添加到 `viewDidLoad` 方法中：

```objc
- (void)viewDidLoad {

    UIAlertView *alert = [[UIAlertView alloc]
        initWithTitle:@"Hello"
        message:@"This is an alert view"
        delegate:self
        cancelButtonTitle:@"OK"
        otherButtonTitles:nil];

    [alert show];
    [alert release];
    [super viewDidLoad];
}
```

#### 工作原理

要使用 `UIAlertView`，首先要实例化它并使用各种参数对其进行初始化：

```objc
UIAlertView *alert = [[UIAlertView alloc]
    initWithTitle:@"Hello"
    message:@"This is an alert view"
    delegate:self
    cancelButtonTitle:@"OK"
    otherButtonTitles:nil];
```

第一个参数是警告视图的标题，你将其设置为“Hello”。第二个是消息，你将其设置为“This is an alert view”。第三个是代理，你需要将其设置为一个将处理 `UIAlertView` 对象触发事件的对象。在这种情况下，你将其设置为 `self`，这意味着事件处理程序将在当前类（即视图控制器）中实现。`cancelButtonTitle` 参数显示一个按钮，用于关闭警告视图。最后，`otherButtonTitles` 参数允许你在需要时显示其他按钮。如果不需要其他按钮，只需将其设置为 `nil`。

要以模态方式显示警告视图，请使用 `show` 方法：

```objc
[alert show];
```

> **常见错误** 需要注意的是，使用 `show` 方法以模态方式显示警告视图并不会使程序在该语句处暂停执行。即使你可能尚未关闭警告视图，该行之后的后续语句仍会继续执行。

对于警告视图的简单用途，你实际上不需要处理它触发的事件。点击“OK”按钮（如 `cancelButtonTitle` 参数中所设置）即可关闭警告视图。

如果你需要多个按钮，则需要设置 `otherButtonTitles` 参数，如下所示：

```objc
UIAlertView *alert = [[UIAlertView alloc]
    initWithTitle:@"Hello"
    message:@"This is an alert view"
    delegate:self
    cancelButtonTitle:@"OK"
    otherButtonTitles:@"Option 1", @"Option 2", nil];
```

请注意，你需要在 `otherButtonTitles` 参数末尾加上 `nil`，否则会发生运行时错误。

现在你有了三个按钮，你需要能够知道用户按下了哪个按钮——特别是按下了选项1还是选项2。为此，你需要处理 `UIAlertView` 类触发的事件。你可以通过确保视图控制器实现 `UIAlertViewDelegate` 协议来实现这一点：

```objc
@interface UsingViewsViewController : UIViewController
<UIAlertViewDelegate> {
    //...
```

