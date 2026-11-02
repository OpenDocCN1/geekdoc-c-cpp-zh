
## 调试你的应用程序

调试你的 iPhone 应用程序是你开发旅程中必不可少的一部分。Xcode 包含调试实用工具，可帮助你在执行应用程序时跟踪和检查代码。以下各节展示了一些在开发 iPhone 应用程序时可采用的技巧。

### 错误

当你尝试运行应用程序时，Xcode 首先尝试构建项目，然后才能将应用程序部署到真实设备或模拟器上。Xcode 检测到的任何语法错误都会立即以红色突出显示。图 B-10 显示了 Xcode 突出显示语法错误。代码块中的错误是 [[UIAlertView alloc] 语句缺少大括号符号 (})：

```objc
UIAlertView *alert = [[UIAlertView alloc]
                 initwithTitle:@"Hello World"
                 message:@"Hello, My World"
                 delegate:self
                 cancelButtonTitle:@"OK"
                 otherButtonTitles:nil];
[alert show];
[alert release];
}
[super viewDidLoad];
```

![](img/aab2d775c46f70cd606f2e58e2521324_460_0.png)

你能发现错误吗？从语法上看，前面的语句没有问题。然而，其中一个参数的大小写不正确。原来 initwithTitle: 必须拼写为 initWithTitle:。当你编译程序时，Xcode 不会将前面的代码标记为错误，而是会发出黄色显示的警告信息（见图 B-12）。

![](img/aab2d775c46f70cd606f2e58e2521324_462_0.png)

图 B-12

当你在 Xcode 中看到警告信息时，请特别注意它，并检查方法名称是否拼写正确，包括大小写。未能做到这一点可能会导致运行时异常。图 B-13 显示了运行时异常发生时 Xcode 显示的运行时异常消息。

![](img/aab2d775c46f70cd606f2e58e2521324_462_1.png)

图 B-13

> **NOTE** 你可以通过点击来切换断点的状态以启用或禁用它。以深蓝色显示的断点为启用状态；以浅蓝色显示的为禁用状态。

在应用程序中设置断点后，你需要按 Command-Y 来调试应用程序，以便在到达断点时停止。

> **NOTE** 按 Command-R 运行应用程序不会导致断点被停止。

当应用程序到达你设置的断点时，Xcode 会用红色箭头显示当前执行行（见图 B-16）。

![](img/aab2d775c46f70cd606f2e58e2521324_464_0.png)

图 B-16

在此阶段，你可以执行以下操作：

- 单步进入 (Shift-Command-I) — 进入函数/方法中的语句。
- 单步跳过 (Shift-Command-O) — 执行函数/方法中的所有语句并继续到下一条语句。
- 单步退出 (Shift-Command-T) — 完成函数或方法中所有语句的执行并继续到函数调用后的下一条语句。
- 如果你想恢复应用程序的执行，请按 Option-Command-P。
- 你还可以通过点击显示调试器按钮来检查变量和对象的值（见图 B-17）。你也可以将鼠标悬停在感兴趣的对象和变量上以查看其值。

![](img/aab2d775c46f70cd606f2e58e2521324_465_0.png)

图 B-17

### 使用 NSLog

除了设置断点来跟踪应用程序的流程外，你还可以使用 `NSLog()` 方法向调试器控制台窗口打印调试信息。以下 `NSLog()` 语句在应用程序更改方向时会向调试器控制台窗口打印一条消息：

```objc
- (void)willRotateToInterfaceOrientation:
    (UIInterfaceOrientation) toInterfaceOrientation
    duration: (NSTimeInterval) duration {

    NSLog(@"In the willRotateToInterfaceOrientation: event handler");

    UIInterfaceOrientation destOrientation = toInterfaceOrientation;
    if (destOrientation == UIInterfaceOrientationPortrait)
    {
        btn.frame = CGRectMake(20,20,280,37);
    }
    else
    {
        btn.frame = CGRectMake(180,243,280,37);
    }
}
```

图 B-18 显示了调试器控制台窗口中的输出（按 Shift-Command-R 显示它）。

![](img/aab2d775c46f70cd606f2e58e2521324_466_0.png)

图 B-18

### 文档

在开发过程中，你经常需要检查 iPhone SDK 中使用的各种方法、类和对象。最好的检查方法是参考文档。Xcode 允许你通过使用 Option 键快速轻松地浏览类、属性和方法定义。要查看项目的帮助文档，只需按 Option 键即可。光标变为十字准星。双击要检查的项目，开发者文档窗口就会出现（见图 B-19）。

![](img/aab2d775c46f70cd606f2e58e2521324_467_0.png)

图 B-19

### 研究助手

文档中一个非常有用的工具是研究助手（Help ⇧ Show Research Assistant）。研究助手是一个窗口，当你在 Xcode 中处理代码时，它会显示上下文相关的帮助。当你将光标定位在特定关键字/语句上时，研究助手将显示有关当前关键字/语句的以下信息（另见图 B-20）：

- 声明
- 摘要
- 可用性
- 相关 API
- 相关文档
- 示例代码

![](img/aab2d775c46f70cd606f2e58e2521324_468_0.png)

图 B-20

### 摘要

在本附录中，你对如何使用 Xcode 开发 iPhone 应用程序有了一个快速概述。你看到了如何使用调试器控制台窗口在应用程序运行时查看 Xcode 生成的输出，以及如何在应用程序中设置断点以便逐步执行代码。

## C 在 Interface Builder 中导航

Interface Builder 是随 iPhone SDK 提供的工具之一。它是一个可视化设计工具，可用于构建 iPhone 应用程序的用户界面。虽然对于 iPhone 应用程序的开发并非严格必需，但 Interface Builder 在你学习 iPhone 应用程序开发的旅程中发挥着不可或缺的作用。本附录涵盖了 Interface Builder 的一些重要功能。

### .XIB 窗口

启动 Interface Builder 的最直接方法是双击 Xcode 项目中的任何 .xib 文件。例如，如果你创建了一个基于视图的应用程序项目，Xcode 的 Resources 文件夹中会有两个 .xib 文件。双击其中任何一个即可启动 Interface Builder。

启动 Interface Builder 时，你看到的第一个窗口与你的 .xib 文件同名（见图 C-1）。

![](img/aab2d775c46f70cd606f2e58e2521324_470_0.png)

图 C-1

在此窗口中有多个项目，具体取决于你双击的内容，你应该会看到以下一些项目，例如：

- File's Owner
- First Responder
- View、Table View、Window 等
- 一些视图控制器和委托

默认情况下，.xib 窗口以图标模式显示。但你也可以切换到列表模式，在该模式下可以更详细地查看某些项目。例如，图 C-2 显示在列表模式下查看时，View 项目会显示其中包含的视图层次结构。

![](img/aab2d775c46f70cd606f2e58e2521324_471_0.png)

图 C-2

### 设计视图

为了设计应用程序的用户界面，你通常会双击 .xib 窗口上的 View（或 Table View 或其他）项目，以可视化显示窗口，以便你可以将视图拖放到 View 窗口上。

要在 View 窗口中填充视图，你可以拖放库窗口中列出的对象（有关库窗口的更多信息，请参阅库部分）。图 C-3 显示了 Label 视图被拖放到 View 窗口上。
